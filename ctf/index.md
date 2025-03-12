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

<details><summary>**Technical Breakdown (2015)** – *Click to expand*</summary>  
Interested in the detailed tech details? [[../ctf/sans-holiday-hack]]
  
**Challenge Synopsis:** The 2015 challenge involved an IoT elf gnome (“Gnome in Your Home”) that players had to investigate. I reverse-engineered firmware to uncover hidden features and analyzed network packets between the gnome and Santa’s servers.  
  
**Key Techniques Used:**  
- *Firmware Analysis:* Extracted and decompiled the gnome’s firmware to find hardcoded credentials and backdoor functions.  
- *Network Traffic Forensics:* Captured and inspected network packets. For example, I discovered an encrypted DNS tunnel. I wrote a custom Python script to decode the DNS exfiltration channel.  
  
**Notable Findings:** I creatively repurposed a firmware update mechanism to inject my own code, effectively turning the gnome against the challenge infrastructure (harmlessly, as part of the game). This novel method impressed the judges and demonstrated a real-world attack scenario.  
  
</details>

## SANS Holiday Hack Challenge 2014 – *Most Creative Winner*  
The 2014 challenge had a story centered around Charles Dickens’ **A Christmas Carol**, with a cyber twist. I won the **Most Creative Technical** category for this competition by crafting an imaginative narrative-style report and solving challenges in unique ways.

<details><summary>**Technical & Creative Highlights (2014)** – *Click to expand*</summary>  
  
**Challenge Synopsis:** The 2014 Holiday Hack featured scenarios where I had to help “Ebenezer Scrooge” secure his network after encounters with various holiday ghosts (each ghost presented a security challenge). I solved puzzles ranging from cryptography to web exploitation.  
  
**Creative Approach:** My submission was presented as a story—writing my report as if I were narrating Scrooge’s overnight adventure in a novella format. Within the story, I embedded the technical solutions (e.g., decoding a malicious ELF file from “Ghost of Christmas Yet-to-Come” as part of the plot). This storytelling approach stood out.  
  
**Technical Tricks:**  
- *Malware Analysis:* Disassembled a binary that played the role of “Ghost malware,” uncovering hardcoded secrets.  
- *Steganography:* One challenge hid a message in an image; I wrote a script to extract and decode the hidden flag.  
- *Pivoting Techniques:* Demonstrated an alternative method to pivot through a compromised system that other participants hadn’t used (earning creativity points).  
  
**Outcome:** By blending a fictional narrative with solid technical execution, I impressed the judges and secured the Most Creative award in 2014.  
  
</details>


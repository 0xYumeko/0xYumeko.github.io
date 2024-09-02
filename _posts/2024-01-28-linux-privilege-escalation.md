---
title: 𝕋𝕣𝕪ℍ𝕒𝕔𝕜𝕄𝕖 𝕎𝕒𝕝𝕜𝕋𝕙𝕣𝕠𝕦𝕘𝕙 𝕃𝟛𝕒𝕜_ℂ𝕋𝔽
author: 0xYumeko
date: 2024-01-28 11:33:00 +0700
categories: [𝕋𝕣𝕪ℍ𝕒𝕔𝕜𝕄𝕖 𝕎𝕒𝕝𝕜𝕋𝕙𝕣𝕠𝕦𝕘𝕙 𝕃𝟛𝕒𝕜_ℂ𝕋𝔽]
tags: [Linux, PHP Code Analysis]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/posts/L3ak-CTF/privesc_linux.png
---

The L3ak_CTF on TryHackMe is a Capture the Flag (CTF) challenge that focuses on testing a participant’s skills in identifying and exploiting information leaks, basic web vulnerabilities, and other security issues. Here’s a walkthrough of the key steps to solve the challenge.

<h1>Step 1: Enumeration</h1>
. Adding registries to your /etc/hosts file makes it easier for machines to remember and learn by their unique names rather than their IP addresses. It also helps in cases where a DNS resolution may not be available or reliable



```bash
echo "$IP l3ak.thm" | sudo tee -a  /etc/hosts
```
![1](https://github.com/user-attachments/assets/ea113392-284d-47d6-b65c-d41251d07e06)



<h1>1 Start with an Nmap Scan:</h1>

Use Nmap to scan the target for open ports and services.

```bash
nmap -sC -sV -oN nmap_scan <target_ip>
```

![2](https://github.com/user-attachments/assets/3233d41f-880b-435f-8cd5-a5860e5f3e57)


The output will show you which ports are open and the services running on those ports.

<h1>Examine the Web Server:</h1>

If HTTP/HTTPS ports (80/443) are open, open the website in a browser.
Use tools like gobuster or dirb to find hidden directories.

```bash
gobuster dir -u http://<target_ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![3](https://github.com/user-attachments/assets/f1e61e4b-0373-4e53-a089-b59b063efa7b)


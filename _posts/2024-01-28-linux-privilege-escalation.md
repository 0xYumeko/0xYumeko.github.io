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



```
echo "$IP l3ak.thm" | sudo tee -a  /etc/hosts

```


<h1>1 Start with an Nmap Scan:</h1>

Use Nmap to scan the target for open ports and services.

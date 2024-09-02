---
title: vault-door-training [ Darija ]
author: 0xYumeko
date: 2024-01-30 11:33:00 +0700
categories: [vault-door-training]
tags: [VaultDoorTraining.java, PicoCtf, Darija,]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/untitled%20folder/banner.jpg
---

Lcode lli drt hwa wa7d limplementation dyal wa7d lprogram b Java lli kaycheck password l iuser, bach idir “access granted” ila password s7i7a.

Hada l program mkatmchi password f source code  w hadchi kaykhdm bach tchouf ila user dakhal password s7i7a.

<h1>Walkthrough :</h1>

<h1>1. User Input : </h1> L program kaytleb men user yedkhel password  Password khas ykoun f lformat : picoCTF{password}.

<h1>Extracting Password :</h1> L program kay7yid picoCTF{ mn l 9dam w } mn l akhr dial input w khassu ykhli password s7i7i.

<h1>Password Check :</h1> L program kayqarn password l iuser dkhalha m3 wa7da mokhtabiya f source code lli hya "w4rm1ng_Up_w1tH_jAv4_3808d338b46".

<h1>Result :</h1> Ila dakhal user password s7i7a, y9oul l program “Access granted”. Ila la, y9oul “Access denied!”.

<h1>Potential Issues :</h1>

L password mkatmiya f source code  hna lproblem dial security hadi  7it ila chi 7ad akhadh l source code  yqder ykoun 3la 3ilm b password.
Wa7d l ihtiyatiya qder ta3mlha hya encrypti l password wla tist3ml hashing techniques bach t7sen l security.

<h1>Test :</h1> Ila bghiti ttesti l program  dakhal picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46} f prompt bash tchouf ach ghadi ykhdm.

![2024-09-02_14-49](https://github.com/user-attachments/assets/fb03ba2f-649f-412b-94d0-df0c906716be)



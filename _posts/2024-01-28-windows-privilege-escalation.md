---
title: vault-door-training [ Darija 🇲🇦 ]
author: 0xYumeko
date: 2024-01-30 11:33:00 +0700
categories: [vault-door-training 🇲🇦 ]
tags: [VaultDoorTraining.java, PicoCtf, Darija,]
pin: false
math: true
mermaid: true
image:
  path: assets/img/untitled%20folder/banner.png
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


Kayn bzzaf dyal tori9 bach tmodifi l'program wla tkhaddam chi technique bach tsayb wla tkhallath b chi 7aja 
<h1>examples : </h1>

<h1>Changement dyal password storage :</h1> T9der tghattay l password lli mkhbay f source code bach matbanach directly  Example: t7awal tpartajiha 3la bytes mn b3d tjoinhom bach t9arnha m3 l input.

```java
public boolean checkPassword(String password) {
    char[] pass = { 'w', '4', 'r', 'm', '1', 'n', 'g', '_', 'U', 'p', '_', 'w', '1', 't', 'H', '_', 'j', 'A', 'v', '4', '_', '3', '8', '0', '8', 'd', '3', '3', '8', 'b', '4', '6' };
    return password.equals(new String(pass));
}
```

<h1>Encoding :</h1>  T9der tktb password f encoded format  b7al Base64  o mn b3d tdecodeha bash tchouf ila s7i7a.

```java
import java.util.Base64;

public boolean checkPassword(String password) {
    String encodedPass = "dzRybTFuZ19VcF93MXRIX2pBdjRfMzgwOGQzMzhiNDY=";
    byte[] decodedBytes = Base64.getDecoder().decode(encodedPass);
    String decodedPass = new String(decodedBytes);
    return password.equals(decodedPass);
}
```

<h1>2. Adding a Fake Password :</h1>


<h1>Distracting attackers :</h1> T9der tzd l password mokhtalfa bash la7d mn akhadh l source code ythayeb  y3ni y7ssb ra dkhal password s7i7a wma kanch. 

<h1>Example :</h1>

```java
public boolean checkPassword(String password) {
    String fakePassword = "fakePassword";
    if (password.equals(fakePassword)) {
        System.out.println("Access denied! (Fake)");
        return false;
    }
    return password.equals("w4rm1ng_Up_w1tH_jAv4_3808d338b46");
}
```

<h1>3. Change the Access Logic :</h1>
Reversing the condition: Ila bghiti tdrab chi wahd l3moq  t9der tkhrba9 l logic b7al t9ul password li mahya s7i7a hiya lli t3tih access. 

<h1>Example :</h1>

```java
public boolean checkPassword(String password) {
    return !password.equals("w4rm1ng_Up_w1tH_jAv4_3808d338b46");
}
```
Hadi t9der tfidk fi chi context lli bghiti t7ammi code mn attackers.


<h1>4. Multiple Passwords :</h1>
Dynamic or Multiple Passwords: T9der tkhdam 3la l program lli ykhdam m3 passwords mokhtalfa wla tbda password m3 kol session wla dayman.


```java
public boolean checkPassword(String password) {
    List<String> validPasswords = Arrays.asList("w4rm1ng_Up_w1tH_jAv4_3808d338b46", "an0ther_Val1d_Pass");
    return validPasswords.contains(password);
}
```





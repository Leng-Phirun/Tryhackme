**[Room](https://tryhackme.com/room/hackervshacker)**

**IP: 10.10.162.146**

---

## Enumeration
---
    nmap -sC -sV 10.10.162.146
```
PORT      STATE    SERVICE         VERSION
  
22/tcp    open     ssh             OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
  
  | ssh-hostkey: 
  
  |   3072 9f:a6:01:53:92:3a:1d:ba:d7:18:18:5c:0d:8e:92:2c (RSA)
  
  |   256 4b:60:dc:fb:92:a8:6f:fc:74:53:64:c1:8c:bd:de:7c (ECDSA)
  
  |_  256 83:d4:9c:d0:90:36:ce:83:f7:c7:53:30:28:df:c3:d5 (ED25519)
  
80/tcp    open     http            Apache httpd 2.4.41 ((Ubuntu))
  
  |_http-server-header: Apache/2.4.41 (Ubuntu)
  
  |_http-title: RecruitSec: Industry Leading Infosec Recruitment
```
## PORT 80
---
![image](https://user-images.githubusercontent.com/100512862/186632835-e07f11e1-3bcb-483d-be48-71879f2a91cd.png)

When we scroll down, there is an upload form which is for uploading CV. At first I try to upload my own php reverse shell file `shell.php` and it successes.

It redirect us to `/upload.php`

![image](https://user-images.githubusercontent.com/100512862/186634990-71f9fca0-0bc2-4bb9-b4bd-8b26754f797b.png)

By viewing the source code we can see the contents of *upload.php*
![image](https://user-images.githubusercontent.com/100512862/186635253-47c60282-c223-44e0-a91b-21327a579bf8.png)

The file goes to `/cvs` and it accepts `pdf` file. Sweet now I can try to upload my reverse shell again with the name of shell.pdf.php. But the message is still the same as before so I assume we can go to `/cvs` and check if our file is there.

So the first file `shell.php` that I uploaded is not there but the second file `shell.pdf.php` is there. Weird, huh?

To my surprise `shell.pdf.php` was already in there by default. By browsing the page, we got this message.
![image](https://user-images.githubusercontent.com/100512862/186636559-c27bdfb0-8e0f-46c1-baf4-abaae6a300f1.png)

If this is not a php reserver shell, I think that it is for **Command Injection**

Let's bruteforce the parameter.
```
ffuf -c -s -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.162.146/cvs/shell.pdf.php?FUZZ=id
```
Sad to tell you but this just spits out random words, but there are some command parameter for **Command Injection**

We can try `?c` or `?cmd`

And `?cmd` works. 

![image](https://user-images.githubusercontent.com/100512862/186638471-f6d83a23-7e7f-42ee-8712-45ed2d70ecfc.png)

Let's get a reverse shell.


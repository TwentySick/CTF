# **MonitorsTwo - Machine - HTB**

*Sorry because of my broken english*

First thing, I ran nmap to scan open port of this server (port 22 and 80 opened as default of ssh and http port)

```
Nmap scan report for 10.10.11.211
Host is up (0.65s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48add5b83a9fbcbef7e8201ef6bfdeae (RSA)
|   256 b7896c0b20ed49b2c1867c2992741c1f (ECDSA)
|_  256 18cd9d08a621a8b8b6f79f8d405154fb (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Login to Cacti
|_http-server-header: nginx/1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

And then, I just check this what happend on this website. Ok this machine use **Cacti version 1.2.22**

![website](/hackthebox/MonitorsTwo/images/website.png)

After a little bit time I spend to search, I found CVE for this version of Cacti on **exploit-db**

![found the cve](/hackthebox/MonitorsTwo/images/found_the_cve.png)

In summary, we can remote to this server by magic way (to understand how, you should read the code). But I can't run on my machine so I found [another PoC of this CVE](https://github.com/ariyaadinatha/cacti-cve-2022-46169-exploit/) and I completely remoted this server

![RCE](/hackthebox/MonitorsTwo/images/RCE.png)

I saw the file "cacti.sql" here

![sql](/hackthebox/MonitorsTwo/images/sql.png)

Read it, I recognized the database contain *user_auth* table. Ok, I spend a bit time to find thing and I found user with password of the database used on this machine.

![found username and password sql](/hackthebox/MonitorsTwo/images/username_password_mysql.png)

With user root and password root, I checked the database and found another user in table *user_auth* from database *cacti*

![found user marcus](/hackthebox/MonitorsTwo/images/found_user_marcus.png)

Beside that, the website just run on a docker container, I can see the file *.dockerenv*

![in the docker](/hackthebox/MonitorsTwo/images/inthedocker.png)

Cracking time, I've cracked password of user marcus, it's *funkymonkey*

![crack password marcus](/hackthebox/MonitorsTwo/images/crack_marcus_password.png)

SSH now :3 with username *marcus* and password *funkymonkey*. Successfully, I spend a lot of time to find thing that helpful. And I found mail for marcus from */var/mail/marcus*. Read that file, I can see the CVE that I can use for this machine. It's a CVE about Docker 

![mail](/hackthebox/MonitorsTwo/images/mail.png)

Reading this CVE on the internet to understand it, I swear it should be easy. Turn back to shell on the docker, I ran *head -1 /etc/mtab* to find the upperdir and workdir of this container. But I need to get the root user in docker. By using linpeas in docker, I easily get root by *capsh*

![linpeas](/hackthebox/MonitorsTwo/images/linpeas.png)

![get root in container](/hackthebox/MonitorsTwo/images/get_root_in_container.png)

I just created file inside container to check. Turn back to ssh terminal, I found this file on upperdir. So the upperdir is the share folder between host and container.

![test in container](/hackthebox/MonitorsTwo/images/test_in_container.png)

![found test inside container](/hackthebox/MonitorsTwo/images/found_test_inside_container.png)

Marcus user has no permission to Write file to this container but also can execute file on that (I don't know why I can list file from it when marcus user has no permission to read, just can execute file in this folder 😁). So I download the bash of this machine and push to container.

![download bash](/hackthebox/MonitorsTwo/images/download_bash.png)

![push bash to container](/hackthebox/MonitorsTwo/images/push_bash_to_container.png)

To get root, I give this file bash permission that can run by any users on this machine and run it with option `-p`.

![give permission](/hackthebox/MonitorsTwo/images/give_perrmission_to_file_bash.png)

![get root](/hackthebox/MonitorsTwo/images/get_root_in_host.png)


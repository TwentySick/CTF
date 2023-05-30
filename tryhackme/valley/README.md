# **Valley - Room - TryHackMe**

*Because of my broken english, I wrote this writeup by my mom language*

Đầu tiên, mình chạy nmap để scan xem có port nào mở ở cái máy này

```bash
Nmap scan report for 10.10.89.185 (10.10.89.185)
Host is up (0.41s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c2842ac1225a10f16616dda0f6046295 (RSA)
|   256 429e2ff63e5adb51996271c48c223ebb (ECDSA)
|_  256 2ea0a56cd983e0016cb98a609b638672 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Mình thấy có công 80 được mở với service httpd, nên mình đã vào trang đó xem có những gì

![website](/tryhackme/valley/images/website.png)

Sau đó mình dùng gobuster để discover cái con web này

```bash
└─$ gobuster dir -u http://10.10.89.185/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.89.185/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.5
[+] Timeout:                 10s
===============================================================
2023/05/31 01:15:44 Starting gobuster in directory enumeration mode
===============================================================
/gallery              (Status: 301) [Size: 314] [--> http://10.10.89.185/gallery/]
/static               (Status: 301) [Size: 313] [--> http://10.10.89.185/static/]
/pricing              (Status: 301) [Size: 314] [--> http://10.10.89.185/pricing/]
```

Nó tìm thấy 3 cái trên (thật ra có 3 cái thôi nên không cần chạy hết cái wordlist đâu), mình check từng cái 1. Mình tìm thấy 1 cái note ở *pricing*

![found note](/tryhackme/valley/images/found_note.png)

Nội dung file note.txt

```
J,
Please stop leaving notes randomly on the website
-RP
```

Vậy là ở đâu đó tại con web này, vẫn còn 1 cái note khác, check *gallery* thấy có 1 file html. Mình có xem nội dung file và thấy nó bốc ảnh từ bên *static* và không có 1 cái note nào ở đây cả. Cơ mà cái *static* lại không xem được, nên mình đã lại gobuster và tìm thấy 1 file 00.

![other notes](/tryhackme/valley/images/other_notes.png)

Thấy được cái */dev1243224123123*, mình truy cập thử và có 1 trang web khác

![other page](/tryhackme/valley/images/login_page.png)

Mình có đọc source của cái page này, thấy có gọi 1 file là dev.js nên đã kiểm tra file này và thành công lấy được username và password để login page

![website login cracked](/tryhackme/valley/images/website_login_cracked.png)

Biết được thứ mà nó sẽ redirect đến sau khi login nên mình truy cập vào đó, lại có thêm 1 cái note nữa

![note from login page](/tryhackme/valley/images/note_from_login_page.png)

Vậy là có 1 cổng chạy service ftp mà lúc nãy mình không scan ra, nên mình đã scan lại tất cả các port (option default của nmap sẽ chỉ scan những port hay gặp thôi). Mình đã tìm ra port chạy service ftp là port *37310*

```bash
37370/tcp open  ftp     vsftpd 3.0.3
Service Info: OS: Unix
```

Login vào với username với password mình tìm được ở login page, mình có thấy 3 file pcapng của wireshark ở đây

![ftp](/tryhackme/valley/images/ftp.png)

Lấy cả 3 file về đọc, tại file *siemHTTP2.pcapng* ở stream 31, có 1 cái username và password nữa

![pcap](/tryhackme/valley/images/pcap.png)

Lấy được cái này, nên mình đã sử dụng ssh để kết nối vào server và thành công

![ssh](/tryhackme/valley/images/ssh_valleyDev.png)

Mình có kiểm tra xem máy này và thấy có 4 user tính cả root

```bash
valleyDev@valley:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
...
valley:x:1000:1000:,,,:/home/valley:/bin/bash
siemDev:x:1001:1001::/home/siemDev/ftp:/bin/sh
valleyDev:x:1002:1002::/home/valleyDev:/bin/bash
...
```

Sau đó, mình check cronjob xem có gì và thấy root chạy file tên là *photosEncrypt.py*

```bash
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
1  *    * * *   root    python3 /photos/script/photosEncrypt.py
```

Kiểm tra permission cũng như nội dung file, mình thấy nó sẽ sử dụng base64 để encode 1 số ảnh và lưu lại vào thư mực *photoVault*

```bash
valleyDev@valley:~$ ls -la /photos
total 20872
drwxr-xr-x  4 root   root      4096 Mar  6 15:41 .
drwxr-xr-x 21 root   root      4096 Mar  6 15:40 ..
-rw-rw-r--  1 valley valley 1989312 Mar  6 13:38 p1.jpg
-rw-rw-r--  1 valley valley 7939986 Mar  6 13:38 p2.jpg
-rw-rw-r--  1 valley valley 2944190 Mar  6 13:38 p3.jpg
-rw-rw-r--  1 valley valley 2302840 Mar  6 13:38 p4.jpg
-rw-rw-r--  1 valley valley 1749699 Mar  6 13:38 p5.jpg
-rw-rw-r--  1 valley valley 4418823 Mar  6 13:38 p6.jpg
drwxr-xr-x  2 root   root      4096 Mar  6 15:43 photoVault
drwxr-xr-x  2 root   root      4096 Mar  6 19:46 script
valleyDev@valley:~$ ls -la /photos/script
total 12
drwxr-xr-x 2 root root 4096 Mar  6 19:46 .
drwxr-xr-x 4 root root 4096 Mar  6 15:41 ..
-rwxr-xr-x 1 root root  621 Mar  6 15:43 photosEncrypt.py
valleyDev@valley:~$ cat /photos/script/photosEncrypt.py
#!/usr/bin/python3
import base64
for i in range(1,7):
# specify the path to the image file you want to encode
        image_path = "/photos/p" + str(i) + ".jpg"

# open the image file and read its contents
        with open(image_path, "rb") as image_file:
          image_data = image_file.read()

# encode the image data in Base64 format
        encoded_image_data = base64.b64encode(image_data)

# specify the path to the output file
        output_path = "/photos/photoVault/p" + str(i) + ".enc"

# write the Base64-encoded image data to the output file
        with open(output_path, "wb") as output_file:
          output_file.write(encoded_image_data)
```

Do thấy các file ảnh là của user *valley* nên mình tìm cách để đăng nhập vào user này. Và sau 1 hồi lục lọi, mình có tìm được 1 binary file tên là *valleyAuthenticator*, mình đã thử chạy file với user valleyDev nhưng lại báo là Wrong Password or Username

![binary file](/tryhackme/valley/images/binary_file.png)

Rất có thể file này sẽ chứa password của user valley, nên mình đã lấy về để chọc ngoáy xem file có gì, vì file này bị *compress* với *upx* nên cần *decompress* trước, và đây là kết quả sau khi decompile (file này được viết bằng C++ và dùng static link, thêm nữa là do thấy nó dùng md5 nên mình cũng không đào sâu hơn)

![check binary file](/tryhackme/valley/images/check_binary_file.png)

Sử dụng *crackstation*, mình lấy được username và password cho cái file *valleyAuthenticator* đó

![crack username](/tryhackme/valley/images/get_user_valley.png)

Mình thử lại với file mình vừa lấy được và thành công login vào user *valley*

![Authenticated](/tryhackme/valley/images/Authenticated.png)

Check id của user này, mình thấy user ở trong group khác là *valleyAdmin*

```bash
valley@valley:/home/valleyDev$ id
uid=1000(valley) gid=1000(valley) groups=1000(valley),1003(valleyAdmin)
```

Tìm các file mà group được phân quyền, mình có tìm thấy 1 file là *base64.py*

```bash
valley@valley:~$ find / -group valleyAdmin -type f 2>/dev/null
/usr/lib/python3.8/base64.py
valley@valley:~$ ls -l /usr/lib/python3.8/base64.py
-rwxrwxr-x 1 root valleyAdmin 20382 Mar 13 03:26 /usr/lib/python3.8/base64.py
```

File này được dùng trong cái file *photosEncrypt.py* mình tìm thấy bên trên và mình có quyền đọc ghi, thực thi, nên mình đã tạo 1 cái reverse shell ngay cái hàm *encrypt* của nó, bên cạnh đó mình cũng bật cổng để nghe. Việc của mình là ngồi đợi cái cronjob chạy và mình thành công chiếm quyền root

![get root](/tryhackme/valley/images/get_root.png)
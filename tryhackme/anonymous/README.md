# **Anonymous**

*Tóm tắt thì room này khá là dễ, phù hợp cho người mới chơi thể loại này. (b2r)*

Sau khi *Start machine*, mình có dùng nmap để quét các port của server cũng như các service chạy trong đó, và mình nhận được kết quả

```
...
Nmap scan report for 10.10.19.42 (10.10.19.42)
Host is up (0.43s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.0.8 or later
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.4.1.98
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts [NSE: writeable]
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8bca21621c2b23fa6bc61fa813fe1c68 (RSA)
|   256 9589a412e2e6ab905d4519ff415f74ce (ECDSA)
|_  256 e12a96a4ea8f688fcc74b8f0287270cd (ED25519)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 0s, deviation: 1s, median: 0s
|_nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2023-05-15T09:58:46
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: anonymous
|   NetBIOS computer name: ANONYMOUS\x00
|   Domain name: \x00
|   FQDN: anonymous
|_  System time: 2023-05-15T09:58:46+00:00
...
```

Mình có thấy service smb được mở trong server này, nên đã sử dụng enum4linux để check xem nó có những gì, và có được cái directory **pics** được share cũng như username của user đó là namelessone

![smb share](/tryhackme/anonymous/images/smb_share.png)

![smb local user](/tryhackme/anonymous/images/smb_local_user.png)

Mount cái directory pics đó ra, mình có thấy trong này có 2 bức ảnh (Mình ngồi mày mò, ve vãn 2 bức ảnh này 1 hồi và nhận ra nó không chứa gì đặc biệt cả)

![smb_mount](/tryhackme/anonymous/images/smb_mount.png)

Sau đó mình có thấy ftp cho phép anonymous login, tức là ai cũng login được mà không cần xác thực (tức là username là anonymous và không cần password), sau khi login thành công, mình có thấy 1 folder tên là scripts, check bên trong đó thì có 3 files

![ftp](/tryhackme/anonymous/images/ftp.png)

Đọc nội dung 3 file này, mình cảm giác như file **clean.sh** được set trong cronjob của user, nên mình đã tạo 1 **clean.sh** khác để có thể remote vào server (Này gọi là Reverse Shell, Google đi vì nó nhiều lắm)

![file_get_from_ftp](/tryhackme/anonymous/images/file_get_from_ftp.png)

Và đúng là nó trong cronjob của user thật, mình đã kết nối thành công

![RCE](/tryhackme/anonymous/images/nc.png)

Sau một hồi mày mò, lục tung lên, mình thấy user **namelessone** ở trong group **lxd**.

```bash
namelessone@anonymous:~$ id
uid=1000(namelessone) gid=1000(namelessone) groups=1000(namelessone),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd)
```

Mình có tìm thấy bài viết về cái group **lxd** này trên mạng và thành công "get root". (Google cái ra ngay)

![exploit](/tryhackme/anonymous/images/exploit1.png)

![exploit](/tryhackme/anonymous/images/exploit1_2.png)

![get root](/tryhackme/anonymous/images/get_root.png)




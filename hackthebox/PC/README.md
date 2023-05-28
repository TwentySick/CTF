# **PC - Machine - HTB**

*Because my English is dump, so I wrote it by my mom language*

Sau khi dùng nmap scan, mình có thấy ở đây có 2 port là 22, 50051 (Do scan bình thường nhìn thấy mỗi port 22 nên mình đã dùng option -p- để quét toàn bộ các port có thể, không khác brute force lắm)

```
# Nmap 7.93 scan initiated Sun May 21 11:05:02 2023 as: nmap -sC -sV -p- -oN nmap.out -Pn 10.10.11.214
Nmap scan report for 10.129.38.213 (10.129.38.213)
Host is up (0.25s latency).

PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 91bf44edea1e3224301f532cea71e5ef (RSA)
|   256 8486a6e204abdff71d456ccf395809de (ECDSA)
|_  256 1aa89572515e8e3cf180f542fd0a281c (ED25519)
50051/tcp open  unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port50051-TCP:V=7.93%I=7%D=5/21%Time=64699875%P=x86_64-pc-linux-gnu%r(N
SF:ULL,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\0\x0
SF:6\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(Generic
SF:Lines,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\0\
SF:x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(GetRe
SF:quest,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\0\
SF:x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(HTTPO
SF:ptions,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\0
SF:\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(RTSP
SF:Request,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\
SF:0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(RPC
SF:Check,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\xff\xff\0\
SF:x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0")%r(DNSVe
SF:rsionBindReqTCP,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0\?\
SF:xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\0\0
SF:")%r(DNSStatusRequestTCP,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0
SF:\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\
SF:0\0\?\0\0")%r(Help,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x05\0
SF:\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0\?\
SF:0\0")%r(SSLSessionReq,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff\xff\0\x0
SF:5\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\0\0\0\0\0
SF:\?\0\0")%r(TerminalServerCookie,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xf
SF:f\xff\0\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0
SF:\0\0\0\0\0\?\0\0")%r(TLSSessionReq,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?
SF:\xff\xff\0\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x0
SF:8\0\0\0\0\0\0\?\0\0")%r(Kerberos,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\x
SF:ff\xff\0\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\
SF:0\0\0\0\0\0\?\0\0")%r(SMBProgNeg,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\x
SF:ff\xff\0\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\
SF:0\0\0\0\0\0\?\0\0")%r(X11Probe,2E,"\0\0\x18\x04\0\0\0\0\0\0\x04\0\?\xff
SF:\xff\0\x05\0\?\xff\xff\0\x06\0\0\x20\0\xfe\x03\0\0\0\x01\0\0\x04\x08\0\
SF:0\0\0\0\0\?\0\0");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Do port 50051 khá lạ, nên mình đã mất một chút thời gian để tìm hiểu về service thường được dùng trên port này là gì (giống ssh thì thường là port 22). Thì port 50051 thường dùng cho **gRPC** (theo thông tin mình đọc được thì giao thức này khá an toàn, nhưng nó lại không an toàn khi dùng ở port 50051, kiểu http thì 80 nhưng secure lại port 443 default ấy). Nên mình đã tìm 1 số tool để có thể giao tiếp với port này, mình có tìm thấy *evans*, *grpcui*, *grpcurl*. 

![evans](/hackthebox/PC/images/evans.png)

Mình chạy service login với username *admin* password *admin* như mình thường làm.

![login_and_getInfo](/hackthebox/PC/images/login_and_getInfo.png)

Login thành công, nhưng khi getInfo thì lại thiếu token header, mà giá trị nó trả lại lại không hiện token, nên mình đã bật wireshark lên để bắt xem dữ liệu nhận được là gì. Do port này là insecure của gRPC nên mình đọc khá rõ được thông tin của package ở trên wireshark

![got token](/hackthebox/PC/images/login_and_have_token.png)

Mình đã thêm header và getInfo thử xem nó có gì, và đây là kết quả

![getInfo success](/hackthebox/PC/images/getInfo_default.png)

Do vậy, mình đã nhập linh tinh vào *id* xem nó trả kết quả như nào.

![error](/hackthebox/PC/images/error_getInfo.png)

Mình khá chắc chắn cái gRPC của con server này dùng ngôn ngữ *Python*, mà *Python* thì mình nghĩ đến *sqlite3*, nên mình đã thử Injection nó (xin lỗi vì thuật ngữ chuyên ngành mình khá yếu)

![union test](/hackthebox/PC/images/Union_test.png)

OMG, it's worked !!!

Vậy nên mình sẽ sử dụng nghiệp vụ để check xem cái *sqlite3* này có những gì. Mình đã thử khá nhiều lần và thành công lấy được *username* và *password* cho 1 thứ gì đó.

![got username and password](/hackthebox/PC/images/got_username_and_password.png)

Mình đã thử sử dụng *username* với *password* mới lấy được để kết nối đến server bằng ssh. Và mình kết nối thành công.

![ssh](/hackthebox/PC/images/ssh.png)

Sau một khoảng thời gian ngồi lục lọi, mình có thấy rằng server này có cài *[PyLoad](https://github.com/pyload/pyload)*

![found pyload](/hackthebox/PC/images/found_pyload.png)

Mình khá chắc nó chạy 1 con web nào đó nên đã forward port 8000 về máy và xem cái web nó đang chạy là gì. Đây là kết quả

![forward port](/hackthebox/PC/images/forward_port_ssh.png)

Nhưng mình không có ý tưởng gì về cái này, nhưng mình lại tìm được 1 cái [CVE của pyLoad](https://github.com/bAuh0lz/CVE-2023-0297_Pre-auth_RCE_in_pyLoad) này, nó khá mới. Mình test thử, một lần nữa, nó hoạt động 😁

![test CVE](/hackthebox/PC/images/test_CVE.png)

Thấy vậy, mình đã RCE để chiếm quyền root (ditme thuat ngu chuyen nganh, khong biet noi the nao cho dung thuat ngu)

![get root](/hackthebox/PC/images/get_root.png)
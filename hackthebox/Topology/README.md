![Topology](/hackthebox/Topology/images/Topology.png)

# **Topology - Machine - Hack The Box**

*Notes: Đây là máy chung, trong quá trình mình viết writeup đã bị phá khá nhiều nên là nếu bạn làm theo mà không được thì bạn đen thôi*

Mình đã scan IP này với công cụ nmap và đây là kết quả

```
Nmap scan report for 10.10.11.217 (10.10.11.217)
Host is up (0.14s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 dcbc3286e8e8457810bc2b5dbf0f55c6 (RSA)
|   256 d9f339692c6c27f1a92d506ca79f1c33 (ECDSA)
|_  256 4ca65075d0934f9c4a1b890a7a2708d7 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Miskatonic University | Topology Group
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Thấy có mở port 80 chạy http, nên mình đã vào để xem có gì không và thấy có 1 trang khác từ IP này là *http://latex.topology.htb/equation.php*

![Latex](/hackthebox/Topology/images/Latex.png)

Mình đã có check xem nó có gì và tìm thấy *header.tex* cùng với *equationtest.tex*

![found_header_and_sample](/hackthebox/Topology/images/found_header_and_sample.png)

Tại file *header.tex*, đây trông như các package được sử dụng

![header_tex](/hackthebox/Topology/images/header_tex.png)

Còn file *equationtest.tex* trông giống như sample được sử dụng

![equationtest_tex](/hackthebox/Topology/images/equationtest_tex.png)

Sau 1 khoảng thời gian research và thử, mình có thấy header có sử dụng package *listing* nên mình đã sử dụng *\lstinputlisting{/etc/passwd}* để đọc thử file passwd trong etc. Nhưng nó lại bị lỗi

![test_listing](/hackthebox/Topology/images/test_listing_package.png)

Nhìn lại file *equationtest.tex*, mình đã thêm ký tự '$' vào 2 đầu và thử lại lần 2. Lần này lại thành công đọc được file passwd, tuy nhiên nó lại để dưới dạng file

![success read file passwd](/hackthebox/Topology/images/success_test_package_listing.png)

Dựa vào FHS của Linux, cùng với hệ thống sử dụng Apache2, mình đã mò vào đọc config của Apache tại machine và tìm thấy *Document Root* của latex

![found document root](/hackthebox/Topology/images/found_document_root_latex.png)

Khi biết được *Document Root*, mình đã dùng nó để đọc file *equation.php* để xem file này làm những gì. File sẽ nhận input từ *eqn* và qua hàm check, có sẵn 1 list ở đây và nó filter bằng sạch các cách có thể dễ dàng tìm trên mạng. Vậy là mình sẽ cần tìm 1 cách nào đó khác để có thể chui vào máy này

![equation php](/hackthebox/Topology/images/equation_php.png)

Và sau 1 hồi tìm kiếm, mình đã tìm thấy *filecontents* và có thể dùng để ghi file cũng như không dính filter, mình đã sử dụng ```$\begin{filecontents}[force]{temp.txt} asdf \end{filecontents}$``` để ghi file và thành công, nhưng lại không ghi được nội dung file

![write file with filecontent](/hackthebox/Topology/images/write_file_using_filecontent.png)

Sau một hồi ngồi tìm hiểu, mình thấy rằng cái thứ mình nhập vào bị sai format, bên cạnh đó do file php này nhận đường dẫn nên mình đã sử dụng URL Encode để có thể nhập đúng format

![URL Encode](/hackthebox/Topology/images/URL_encode.png)

Và mình đã thành công chui vào trong machine này

![remote to machine](/hackthebox/Topology/images/remote_to_machine.png)

Sau một hồi tìm kiếm, mình có đọc được trong file *.htpasswd* trong folder /var/www/dev là creds của user trong machine, crack nó và mình thành công lấy được user trong machine

![get user](/hackthebox/Topology/images/get_user.png)

Mình có thấy user root có chạy 1 cái cronjob ở đây, cứ 1 phút là sẽ thực hiện việc này, sẽ chạy gnuplot với tất cả các file đuôi *plt* trong thư mục */opt/gnuplot*

![cronjob](/hackthebox/Topology/images/cronjob_root.png)

Thật trùng hợp khi mình check thư mục này, mình có quyền ghi nhưng lại không có quyền đọc

![gnuplot](/hackthebox//Topology/images/gnuplot.png)

Tuy vậy vẫn không cản trở được lắm vì có quyền ghi, nên mình đã ghi 1 file plt vào đó và thành công get root

![get root](/hackthebox/Topology/images/get_root.png)
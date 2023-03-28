# **who is it**

## **Description**

![description](/2023/picoctf2023/forensics/who_is_it/images/description.png)

## **Solution**

Mở file eml lên đọc, mình có nhận thấy ở đây có địa chỉ IP ở phần *Received*

![getIP](/2023/picoctf2023/forensics/who_is_it/images/getIP.png)

Dùng trang web [whois](https://www.whois.com/) kiểm tra, mình đã có được tên cũng như các thông tin khác

![whois](/2023/picoctf2023/forensics/who_is_it/images/whois.png)

Flag: `picoCTF{WilhelmZwalina}`
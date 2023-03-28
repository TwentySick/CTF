# **hideme**

## **Description**

![description](/2023/picoctf2023/forensics/hideme/images/description.png)

## **Solution**

Sử dụng **binwalk**, mình có thấy ở trong file *flag.png* có giấu 1 file zip nào đó

![binwalk](/2023/picoctf2023/forensics/hideme/images/binwalk.png)

Sau khi extract và unzip, mình đã lấy được file *flag.png* khác và đây chính là flag

![getFlag](/2023/picoctf2023/forensics/hideme/images/getFlag.png)

Flag: `picoCTF{Hiddinng_An_imag3_within_@n_ima9e_5fbf3ff9}`
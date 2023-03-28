# **ReadMyCert**

## **Description**

![description](/2023/picoctf2023/cryptography/read_my_cert/images/description.png)

## **Solution**

Mình có dùng **file** để check và cat file

![cat](/2023/picoctf2023/cryptography/read_my_cert/images/cat.png)

Đây là 1 file PEM, và nội dung nó được encode bằng base64, mình đã dùng base64 decode nó và nhận được flag (Thật ra cách này stupid vl)

![decode](/2023/picoctf2023/cryptography/read_my_cert/images/decode.png)

Flag: `picoCTF{read_mycert_e675addc}`
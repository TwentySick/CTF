# **FindAndOpen**

## **Description**

![description](/2023/picoctf2023/forensics/find_and_open/images/description.png)

## **Solution**

Từ đề ta có 2 file: 1 file zip và 1 file pcap. Mình quyết định check file pcap trước, khi đang xem các package trong file này, mình có thấy 1 đoạn text đã được mã hóa base64

![found the secret](/2023/picoctf2023/forensics/find_and_open/images/found_the_secret.png)

Sau khi decode, mình đã lấy được đoạn secret

![getSecret](/2023/picoctf2023/forensics/find_and_open/images/getSecret.png)

Và mình đã mất 1 khoảng thời gian để nhận ra cái **Secret** mình tìm được chính là **password** cho **file zip** đi kèm (duma lừa vl). Mình unzip và lấy flag thôi

![unzip](/2023/picoctf2023/forensics/find_and_open/images/unzip.png)

Flag: `picoCTF{R34DING_LOKd_fil56_succ3ss_556434d1}`
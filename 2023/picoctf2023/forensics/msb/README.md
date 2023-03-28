# **MSB**

## **Description**

![description](/2023/picoctf2023/forensics/msb/images/description.png)

## **Solution**

Mình sử dụng **Stegsolve** để kiểm tra ảnh, mình có thấy rằng tại plane 7 của Red, Blue, Green nó rất lạ (Tự check đi, DIY thôi), mình đoán ra secret nó ở đây nên mình đã extract dữ liệu tại plane này ra bằng MSB

![get Data](/2023/picoctf2023/forensics/msb/images/getData.png)

Sau khi save vào 1 file text, mình có dùng grep để tìm

![grep pico](/2023/picoctf2023/forensics/msb/images/grepPico.png)

Sau đó mình lấy được flag

![getFlag](/2023/picoctf2023/forensics/msb/images/getFlag.png)

Flag: `picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_5acdd67c}`
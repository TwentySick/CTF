# **HideToSee**

## **Description**

![description](/2023/picoctf2023/cryptography/HideToSee/images/description.png)

## **Solution**

Dùng stegseek để crack, mình có nhận được 1 đoạn text sau

![firststep](/2023/picoctf2023/cryptography/HideToSee/images/steghide.png)

Cùng với hình ảnh được cho, mình đã tìm Atbash Cipher và decode

![decode](/2023/picoctf2023/cryptography/HideToSee/images/decode.png)

Flag: `picoCTF{atbash_crack_e7faa0e5}`
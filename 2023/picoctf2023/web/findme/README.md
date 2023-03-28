# **findme**

## **Description**

![description](/2023/picoctf2023/web/findme/images/description.png)

## **Solution**

Mình dùng **burpsuite** để theo dõi việc mình tương tác với trang web, và đây là kết quả mình nhận được

![firstpart](/2023/picoctf2023/web/findme/images/firstpart.png)

![secondpart](/2023/picoctf2023/web/findme/images/secondpart.png)

Ghép 2 đoạn đó vào, mình thu được string "cGljb0NURntwcm94aWVzX2FsbF90aGVfd2F5XzNkOWUzNjk3fQ==" và dùng base64 decode, mình lấy được flag

![solved](/2023/picoctf2023/web/findme/images/solved.png)

Flag: `picoCTF{proxies_all_the_way_3d9e3697}`
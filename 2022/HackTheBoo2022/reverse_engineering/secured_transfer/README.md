# Secured Transfer
## Challenge

![challenge](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/challenge.png)

[File Source](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/rev_securedtransfer.zip)

## Solution
Khi mở lên, đây là 1 file bị stripped nên khá mất thời gian nếu chưa quen với cái này cũng như chưa biết các cách để truy vết ra nhanh

![checkFile](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/checkFile.png)

Ngồi lục lọi một hồi, mình biết file này sẽ thực thi encrypt bằng AES CBC và gửi đi cũng như sẽ dùng AES CBC để decrypt khi nhận file về

![foundEncrypt](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/foundEncrypt.png)

![foundDecrypt](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/foundDecrypt.png)

Vậy data encrypt được gửi đi nó đang ở đâu ? Có thể dễ tìm thấy nếu đọc theo luồng TCP từ file pcap đính kèm trong challenge

![getEncryptData](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/getEncryptData.png)

Có đầy đủ mọi thứ trong tay, mình dễ dàng decrypt phần data đó và lấy được flag (Xin lỗi vì code yếu nên dùng tool trên mạng được chưa :< )

![getFlag](/2022/HackTheBoo2022/reverse_engineering/secured_transfer/images/getFlag.png)

Flag: `HTB{vryS3CuR3_F1L3_TR4nsf3r}`
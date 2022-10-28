# Trick or Breach
## Challenge

![challenge](/2022/HackTheBoo2022/forensics/trick_or_breach/images/challenge.png)

[File Source](/2022/HackTheBoo2022/forensics/trick_or_breach/forensics_trick_or_breach.zip)

## Solution

Sau khi mở file pcap mà challenge cho, mình có để ý ở phần data của mỗi package, nó đều chứa 1 đoạn hex + domain của 1 trang web nào đó

![readPcap](/2022/HackTheBoo2022/forensics/trick_or_breach/images/readPcap.png)

Mình đã sử dụng trình độ edit plain text thông thạo 7 của mình để lấy ra đống hex đó sau khi Export as plain text
Không khó để nhận ra đây là đống bytes của 1 file zip (Thật ra nhìn header là biết ngay nếu ai đã tìm hiểu qua về signature của file)

![getData](/2022/HackTheBoo2022/forensics/trick_or_breach/images/getData.png)

Và mình đã tìm thấy flag tại file `sharedStrings.xml` sau khi extract file zip vừa lấy được

![getFlag](/2022/HackTheBoo2022/forensics/trick_or_breach/images/getFlag.png)

Flag: `HTB{M4g1c_c4nn0t_pr3v3nt_d4t4_br34ch}`
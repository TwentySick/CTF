# **PcapPoisoning**

## **Description**

![description](/2023/picoctf2023/forensics/pcap_poisoning/images/description.png)

## **Solution**

Sử dụng **wireshark** đọc file mà đề cho, mình thấy ở đây có nhiều package sử dụng FTP Protocol

![first look](/2023/picoctf2023/forensics/pcap_poisoning/images/firstlook.png)

Mình quyết định follow từng stream 1 như mình vẫn thường làm, thì ở ngay stream đầu tiên có thấy username và password, đi kèm package đó là 1 package đó, mình check xem và lấy được flag

![getFlag](/2023/picoctf2023/forensics/pcap_poisoning/images/getFlag.png)

Flag: `picoCTF{P64P_4N4L7S1S_SU55355FUL_14f62f23}`
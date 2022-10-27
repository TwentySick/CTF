# EncodedPayload
## Challenge

![challenge](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/challenge.png)

[File Source](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/rev_encodedpayload.zip)

## Solution

Khi nhận được file, mình đã decompile và nhận ra đây là 1 file `no section header` (cái thứ mà mình ghét).

![decompile](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/decompile.png)

Sau một hồi lục lọi trong bất lực, mình quyết sử dụng `gdb` với cái file này. Chạy một hồi đến ô địa chỉ `0x8048089` thì mình nhận ra mình đang trong một cái loop

![inLoop](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/inLoop.png)

Đặt breakpoint và sử dụng continue, mình thoát khỏi loop và đi tìm chân lí

![escapeLoop](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/escapeLoop.png)

Chạy một hồi, mình thấy có gì đó lạ lạ. `/bin/bash` ? `-c`? `echo`? Và bùm, mình tìm thấy flag

![foundFlag](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/getFlag.png)

Sau khi có flag, mình nhận ra mình có cách làm đơn giản hơn là sử dụng `strace` với file 

![easyWay](/2022/HackTheBoo2022/reverse_engineering/encodedpayload/images/easyWay.png)

Flag: `HTB{PLz_strace_M333}`
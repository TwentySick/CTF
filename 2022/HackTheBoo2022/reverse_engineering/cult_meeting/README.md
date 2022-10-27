# Cult Meeting
## Challenge

![challenge](/2022/HackTheBoo2022/reverse_engineering/cult_meeting/images/challenge.png)

[File Source](/2022/HackTheBoo2022/reverse_engineering/cult_meeting/rev_cult_meeting.zip)

## Solution

Sau khi lấy file về, mình đã decompile nó xem nó có những gì, thì mình đã tìm được 1 chuỗi trong này và nhìn có vẻ là password của cái gì đó

![foundPassword](/2022/HackTheBoo2022/reverse_engineering/cult_meeting/images/foundPassword.png)

Và mình quyết định chạy thử file này tại không thấy gì nguy hiểm cả :<

![testLocal](/2022/HackTheBoo2022/reverse_engineering/cult_meeting/images/testLocal.png)

Bất ngờ chưa vì sau khi nhập chuỗi kia, mình có quyền sử dụng bash, nên mình đã netcat đến địa chỉ IP và Port của machine của challenge và lấy flag

![getFlag](/2022/HackTheBoo2022/reverse_engineering/cult_meeting/images/getFlag.png)


Flag: `HTB{1nf1ltr4t1ng_4_cul7_0f_str1ng5}`
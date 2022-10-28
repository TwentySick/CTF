# Ouija
## Challenge

![challenge](/2022/HackTheBoo2022/reverse_engineering/ouija/images/challenge.png)

[File Source](/2022/HackTheBoo2022/reverse_engineering/ouija/rev_ouija.zip)

## Solution

Sau khi decompile, mình tìm và thấy có khá nhiều vòng lặp và lệnh sleep, tức là để chạy xong chương trình sẽ rất tốn thời gian

![decompile](/2022/HackTheBoo2022/reverse_engineering/ouija/images/decompile.png)

Và tại đoạn cuối, mình có thấy có lệnh in flag theo từng ký tự 1, nên mình quyết định sửa lại toàn bộ sleep(1), sleep(10) về sleep(0) và xuất ra file mới rồi thực thi (Thật ra lúc đó mình lười không muốn ngồi phân tích đó :( )

![afterChanged](/2022/HackTheBoo2022/reverse_engineering/ouija/images/afterChanged.png)

Chạy file, mình thành công vượt qua việc ngồi đợi chương trình chạy vì khi không có sleep, nó chạy tốc độ rất flash speed

![runFile](/2022/HackTheBoo2022/reverse_engineering/ouija/images/runFile.png)

Bằng 1 chút nghiệp vụ chỉnh sửa text, mình thành công lấy flag

![getFlag](/2022/HackTheBoo2022/reverse_engineering/ouija/images/getFlag.png)

Flag: `HTB{Adding_sleeps_to_your_code_makes_it_easy_to_optimize_later!}`
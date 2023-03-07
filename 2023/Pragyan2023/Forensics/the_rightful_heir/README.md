# The Rightful Heir

## Challenge

![challenge](/2023/Pragyan2023/Forensics/the_rightful_heir/images/challenge.png)

[key.jpg](/2023/Pragyan2023/Forensics/the_rightful_heir/key.jpg)

## Solution

Đầu tiên, mình dùng **stegseek** để crack và lấy được file ẩn đang giấu trong file ảnh, và mình đã lấy được 1 đường link

![first step](/2023/Pragyan2023/Forensics/the_rightful_heir/images/first_step.png)

Mở đường link pastebin kia, mình lấy được 1 đoạn text

![pastebin](/2023/Pragyan2023/Forensics/the_rightful_heir/images/pastebin.png)

Thấy đoạn text này, mình nảy ra suy nghĩ về twitter secret messages nên đã dùng nó để decode

![Twitter_secret_messages](/2023/Pragyan2023/Forensics/the_rightful_heir/images/Twitter_secret_messages.png)

Mở đường link được giấu trong text, mình lấy được ảnh lock.jpeg

![](/2023/Pragyan2023/Forensics/the_rightful_heir/images/lock.png)

Sau 1 hồi loay hoay, mình nhận ra file họ cho là key và mình tìm được lock, thì mình có dùng gimp để xử lý, mình nghĩ sẽ có cách tốt hơn chứ cách này mình làm thì hơi đau mắt

![](/2023/Pragyan2023/Forensics/the_rightful_heir/images/gimp_mode_diff.png)

Mình đã vẽ lại cùng với sử dụng từ điển tiếng anh vì biết rằng các từ trong flag đều có nghĩa và tạo thành 1 câu, và đây là thành quả

![](/2023/Pragyan2023/Forensics/the_rightful_heir/images/draw_and_get_flag.png)

Flag: `p_ctf{r3N3G0t1aT3_tH3_4gR33m3Nt}`
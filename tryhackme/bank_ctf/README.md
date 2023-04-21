# **Bank CTF**

## **!!! Warning !!!**

*I wrote it by my mommmmmmmm language. So if you want to understand it, I strongly recommend you search another writeups 😁*

## **Writeup**

*Đây là 1 bài khá dễ, toàn dùng tool thôi chứ không cần nghĩ nhiều như mấy bài khác*

Sử dụng *nmap*, mình đã quét ra được 2 ports được mở tại con server này là 22 và 80 (by default).

![nmap](/tryhackme/bank_ctf/images/nmap.png)

Sau khi vào trang web thì mình có thấy 1 cái button "Check robot permission", mình đã Ctrl + U (hoặc F12 hoặc làm 1 cách nào đó để đọc được cái html đấy) và thấy nó có *robots.txt*. Đây chính là 1 cái wordlist và mình đã save nó lại vì nghĩ rằng thể nào cũng sử dụng nó

![pwdlist](/tryhackme/bank_ctf/images/password_list.png)

Nhưng do chưa biết làm gì tiếp nên mình sử dụng *gobuster* để discovery cái trang web này và mình đã tìm thấy *wordpress*.

![found wordpress](/tryhackme/bank_ctf/images/found_wordpress.png)

Truy cập vào, mình có đến được 1 cái blog và click vào banking, mình lấy được flag đầu tiên

![first flag](/tryhackme/bank_ctf/images/first_flag.png)

Và để đăng được cái đống này thì ắt hẳn sẽ phải có chỗ để login các kiểu, và do mình đã mò ra với đường dẫn */wordpress/wp-admin*

![login page](/tryhackme/bank_ctf/images/login_page.png)

Sau 1 hồi mày mò các kiểu, nhập username loạn xì ngậu, mình nhận ra cái bài kia có nhắc đến patrick nên mình đã thử tên patrick và sử dụng *hydra* để tìm ra mật khẩu với wordlist là cái mình lấy được (Còn làm sao để có được cái http-form thì hãy google cách sử dụng *hydra* và sử dụng *burpsuite* để check).

![burpsuite](/tryhackme/bank_ctf/images/burpsuite.png)

![found first user to login](/tryhackme/bank_ctf/images/found_first_user_to_login.png)

Có được password, mình liền đăng nhập vào để xem user này có những gì.

![second flag](/tryhackme/bank_ctf/images/second_flag.png)

Thấy nó ghi như vậy, mình nghĩ đến tài khoản manager và liền logout để thử và đúng là có user như vậy thật (vì nếu không có nó sẽ báo không tồn tại user), tiếp tục sử dụng hydra để tìm password cho cái user này giống như cách mình làm với user patrick

![found user manager](/tryhackme/bank_ctf/images/found_user_manager_to_login_wordpress.png)

Login thành công, mình bắt đầu mày mò mọi thứ mà user này có, mình có để ý đến phần upload media nhưng không được và có tốn 1 chút thời gian cho công đoạn này. Trời không phụ lòng người khi mình tìm đến page và có cái page *Bank Login*. Thấy có cái đống số đấy, mình sử dụng 1 cái tool trên mạng để decode cho nhanh, đỡ phải gõ script (tool nào cũng được, gõ cái ra ngay)

![third flag](/tryhackme/bank_ctf/images/third_flag.png)

![second list](/tryhackme/bank_ctf/images/second_list.png)

Mình nghĩ đây có thể là list username nên đã save nó lại, sau đó lại là *hydra* để tấn công vào cổng 22 của server (mình có sử dụng cái list user mới tìm thấy và cái list password tìm thấy ở mấy bước trước). Đoạn này khá là tốn thời gian 🤡

![ssh](/tryhackme/bank_ctf/images/ssh.png)

Cuối cùng cũng tìm được, mình đã kết nối đến server này qua port 22, sau 1 hồi lục lọi, mình có tìm thấy *message_for_cat*.

![message_for_cat](/tryhackme/bank_ctf/images/message_for_cat.png)

Đọc cái này và mình thấy không có gì đặc biệt, có vẻ giống như nó đang hướng dẫn mình crack password của user nó đúng hơn. Mình đã chạy *sudo -l* để check về quyền hạn sử dụng lệnh sudo của user patrick và bùm, ngạc nhiên chưa

![check sudo](/tryhackme/bank_ctf/images/check_sudo.png)

*(ALL:ALL) ALL* là thiên đường, tức là mình không cần nghĩ cách để leo lên root khi đã biết mật khẩu của user mình đang sử dụng, chỉ cần chạy *sudo su* để vào user root thôi. Thì mình có kiểm tra directory *root* để xem có gì và tìm được flag 6

![sixth flag](/tryhackme/bank_ctf/images/sixth_flag.png)

Sau đó mình có thấy user tên là cat khi check file *passwd*

![passwd](/tryhackme/bank_ctf/images/passwd.png)

Mình đã có check thư mục home của user này và tìm thấy flag 4

![fourth flag](/tryhackme/bank_ctf/images/fourth_flag.png)

Lấy được flag, mình đã kiểm tra file *.bash_history* của user này để xem user này làm những gì. 

![bash_history](/tryhackme/bank_ctf/images/bash_history.png)

Thấy có nhắc đến file *shadow* nên mình check file *shadow* và lấy được flag cuối (thường thì mình ít check file này mặc dù file này quan trọng vkl)

![fifth flag](/tryhackme/bank_ctf/images/fifth_flag.png)

Túm cái váy lại, bài này là bài nhập môn với bộ môn boot2root, nó dễ vl, chưa có đánh đố nhiều và tại các chỗ để flag đều là hint cho bước sau. Hê hê
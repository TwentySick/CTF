# Not Steganography ( [Solved by lvcivn](https://hackappatoi.github.io/Not-Steganography/) )
## Mô tả vấn đề
![Challenge]()
## Giải pháp
Thật ra bài này là mình đọc lại writeup của 1 người giải được chứ mình ko giải được challenge này

Sau khi download file về, mình không thể mở được file do kích thước quá lớn (kích thước file là 271828x271828).\
Nên mình quyết định check Hex của file ( Mình toàn gọi là Hex chứ thật ra nó có tên riêng á )

Nó xuất hiện rất nhiều bytes có giá trị là 00

![first_check]()

Nên mình đã sử dụng `xxd` để lấy toàn bộ dữ liệu có trong file do khi mình dùng `strings` thì vẫn thấy được dữ liệu

![check1]()
![check2]()

Sau khi lấy ra được hết dữ liệu, mình tạo 1 file mới bằng đống Hex mình lấy được và chỉnh lại chiều dài file chứ không phải chiều rộng của file (Hãy đọc writeup của anh kia thì sẽ rõ hơn tại sao lại làm vậy)

Do khi thay đổi giá trị chiều dài, `CRC chunk` cũng bị thay đổi (Cái này là điểm khác biệt của PNG File, thay đổi bất kì giá trị của chunk thì CRC chunk cũng bị thay đổi dẫn đến lỗi file)

Có sự trợ giúp của pngcheck, mình đã fix thành công `CRC chunk` ( hoặc mọi người có thể sử dụng [https://www.nayuki.io/page/png-file-chunk-inspector](https://www.nayuki.io/page/png-file-chunk-inspector) để sửa, trang này được anh viết writeup sử dụng )

![Asking]()

Và đây là thành quả (Mình có sửa lại màu, ở sau PLTE Chunk, mình để giá trị là 00 00 00 FF FF FF, tương ứng với 2 màu đen trắng, còn file gốc là màu Xanh đỏ )

![Fixed]()

Lấy được ảnh, mình đã phải dùng GIMP để tìm được QR Code vì nhìn qua thì nó như 1 cái đường thẳng và nó dài vl (Có thể sử dụng Photoshop hoặc Paint mới của Window để tìm)

![Found_QR_Code]()

Và đây chính là QR Code mà mình lấy được

![QR1]()

Nhưng không thể dùng CyberChef hay 1 cái web scan mã QR bình thường để scan nó, vì nó là QR code của 1 file ảnh khác (Có trang [Base64guru]() đỉnh vl nhưng mình không dùng trong trường hợp này, mình dùng tool `zbarimg` )

Kết quả của mã QR Code bên trên

![QR2]()

Scan QR Code thứ 2, mình tìm được flag

![Solved]()

Flag:
```
ictf{size_matters}
```

Đọc xong thấy nó dễ vl mà ko giải được, thật là buồn quá đi mà =(

![Sad](https://nefariousreviews.files.wordpress.com/2015/07/great-teacher-onizuka-breakdown.jpg?w=474&h=356)

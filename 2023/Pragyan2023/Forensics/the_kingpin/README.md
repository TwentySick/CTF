# **The Kingpin**

## **Challenge**

![challenge](/2023/Pragyan2023/Forensics/the_kingpin/images/challenge.png)

[chall.pcapng](/2023/Pragyan2023/Forensics/the_kingpin/chall.pcapng)

## **Solution**

Mở file, mình thấy ở đây là wireshark đã capture được USB

![first look](/2023/Pragyan2023/Forensics/the_kingpin/images/first_look.png)

Và sau khi mình đọc nhanh 1 lượt, mình thấy ở đây có 2 file zip

![first zip](/2023/Pragyan2023/Forensics/the_kingpin/images/first_zip.png)

![second zip](/2023/Pragyan2023/Forensics/the_kingpin/images/second_zip.png)

Mình đã lấy 2 file này ra và unzip nó để xem bên trong có những gì

![unzip](/2023/Pragyan2023/Forensics/the_kingpin/images/unzip.png)

Cái thứ cụ thể ở trong các folder nó trông như này. Thật ra đây là 2 cái và nó được lặp lại nhiều lần ở các folder khác, đây là mình check ở folder 01 và 02

![first look after unzip](/2023/Pragyan2023/Forensics/the_kingpin/images/first_look_after_unzip.png)

![first look after unzip 2](/2023/Pragyan2023/Forensics/the_kingpin/images/first_look_after_unzip_2.png)

Mình đã thử ghép tất cả các hình ở chung 1 folder 01, và đây là thành quả

![first try](/2023/Pragyan2023/Forensics/the_kingpin/images/first_try.png)

Khi nhìn thấy mình toàn đỏ mà lấp ló là các chữ, đầu mình nảy ra ý tưởng là các hình lại cũng tương tự vậy và khi ghép chung vào nhau, các ảnh đè lên nhau và chỉnh Mode từ Normal sang Screen thì sẽ ra được flag (Cái này mình đã từng nghịch Photoshop nên khá là dễ dàng để có được ý tưởng này). Nhưng vấn đề ở đây là ngồi ghép từng ảnh 1 sẽ rất lâu, kể cả dùng tool trên mạng cũng chưa chắc đã được đúng ý, nên mình quyết định viết 1 đoạn script để nó thực hiện ghép cho mình.

```python
import cv2
import os

# Create folder name 'out'
if(not os.path.isdir('out')):
    os.mkdir('out')

# List folder
h_list = ['02','04','06','08','10']
v_list = ['01','03','05','07','09']

# Combine images horizontally
for folder in h_list:
  img1 = cv2.imread(folder + '/01.png')
  img2 = cv2.imread(folder + '/02.png')
  img3 = cv2.imread(folder + '/03.png')
  img4 = cv2.imread(folder + '/04.png')
  img5 = cv2.imread(folder + '/05.png')
  img6 = cv2.imread(folder + '/06.png')
  img7 = cv2.imread(folder + '/07.png')
  img8 = cv2.imread(folder + '/08.png')
  img9 = cv2.imread(folder + '/09.png')
  img10 = cv2.imread(folder + '/10.png')
  img11 = cv2.imread(folder + '/11.png')
  img12 = cv2.imread(folder + '/12.png')
  img13 = cv2.imread(folder + '/13.png')
  img14 = cv2.imread(folder + '/14.png')
  img15 = cv2.imread(folder + '/15.png')
  img16 = cv2.imread(folder + '/16.png')
  img17 = cv2.imread(folder + '/17.png')
  img18 = cv2.imread(folder + '/18.png')
  img19 = cv2.imread(folder + '/19.png')
  img20 = cv2.imread(folder + '/20.png')

  im = cv2.hconcat([img1,img2,img3,img4,img5,img6,img7,img8,img9,img10,img11,img12,img13,img14,img15,img16,img17,img18,img19,img20])
  cv2.imwrite('out/' + folder + '.png', im)

# Combine images vertically
for folder in v_list:
  img1 = cv2.imread(folder + '/A.png')
  img2 = cv2.imread(folder + '/B.png')
  img3 = cv2.imread(folder + '/C.png')
  img4 = cv2.imread(folder + '/D.png')
  img5 = cv2.imread(folder + '/E.png')
  img6 = cv2.imread(folder + '/F.png')
  img7 = cv2.imread(folder + '/G.png')
  img8 = cv2.imread(folder + '/H.png')
  img9 = cv2.imread(folder + '/I.png')
  img10 = cv2.imread(folder + '/J.png')
  img11 = cv2.imread(folder + '/K.png')
  img12 = cv2.imread(folder + '/L.png')
  img13 = cv2.imread(folder + '/M.png')
  img14 = cv2.imread(folder + '/N.png')
  img15 = cv2.imread(folder + '/O.png')
  img16 = cv2.imread(folder + '/P.png')
  img17 = cv2.imread(folder + '/Q.png')
  img18 = cv2.imread(folder + '/R.png')
  img19 = cv2.imread(folder + '/S.png')
  img20 = cv2.imread(folder + '/T.png')
  
  im = cv2.vconcat([img1,img2,img3,img4,img5,img6,img7,img8,img9,img10,img11,img12,img13,img14,img15,img16,img17,img18,img19,img20])
  
  cv2.imwrite('out/' + folder + '.png', im)
```

Sau khi lấy được 10 ảnh từ 10 folder, mình đã đẩy nó vào gimp để chỉnh sửa. Chuyển mode từ Normal sang Screen và lấy được flag

![get flag](/2023/Pragyan2023/Forensics/the_kingpin/images/get_flag.png)

Flag: `p_ctf{TH3_D3V1L_0F_H3LL5_K1TCH3N_15_B4CK}`


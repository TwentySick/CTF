# Bits and Pieces

## Challenge

![challenge](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/challenge.png)

[bitsAndPieces](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/bitsAndPieces)

## Solution

Đầu tiên, mình kiểm tra file đề cho bằng lệnh `file` (Cái này là thói quen khi mình gặp 1 bài RE để kiểm tra xem file có bị stripped hay không, rồi các thứ linh tinh đi kèm)

![check_file](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/check_file.png)

Và thật là may mắn khi file này **not stripped**, nó sẽ giảm độ khó trong RE đi được 1 phần cho mình, và mình đã decompile file này. Nhìn thoạt qua thì có 2 function encode và 2 function flagcheck

![decompile](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/decompile.png)

Mình có check các function kia để xem trong đó nó sẽ làm những gì

![encode1](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/encode_1.png)

![encode2](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/encode_2.png)

![flagcheck1](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/flagcheck1.png)

![flagcheck2](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/flagcheck2.png)

Trong function encode1, mình có thấy 1 hàm reverse và có function myfunc được sử dụng trong 2 function encode

![reverse](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/reverse.png)

![myfunc](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/myfunc.png)

Mình sẽ xử lý function reverse trước, đọc qua, mình vẫn chưa hình dung được rằng nó sẽ reverse như thế nào và nó làm gì để được gọi là reverse, nên mình đã mô phỏng lại hàm này bằng **Python3**

```python
flag = "abcdefghik"

for i in range(10):
    j = 0
    for k in range(8):
        j = j * 2
        if((ord(flag[i]) >> (k & 0x1f) & 1) != 0):
            j = j + 1
    bin_1 = bin(ord(flag[i]))[2:]
    bin_2 = bin(j)[2:]
    while(len(bin_1) != 8):
        bin_1 = '0' + bin_1
    while(len(bin_2) != 8):
        bin_2 = '0' + bin_2
    print(f"{flag[i]}")
    print(f"Before: {bin_1}")
    print(f"After:  {bin_2}")
    print()
```

Và đây là kết quả

![reverse_script_test](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/reverse_script_test.png)

Tức là cái function này sẽ đảo lại cái thứ tự các bit trong byte của character mà nó xử lý

Kiểu như này, với ký tự *a* sẽ tương đương với số 97 theo bảng mã ASCII, và số 97 khi convert về dạng bit sẽ là `01100001`, và giá trị function kia trả về là `10000110`. Vậy là đã rõ function reverse trong chương trình này sẽ thực hiện nhiệm vụ gì. Tiếp theo mình vọc vạch function myFunc

```python
def myfunc(x, y):
	out = 0
	b1 = 0
	for i in range(31,-1,-1):
		b2 = 1 << (i & 0x1f) & int(ord(y)) != 0
		b3 = 1 << (i & 0x1f) & int(ord(x)) != 0
		if((b2 and b3) or (not(b2) and not(b3))):
			b1 = 0
		else:
			b1 = 1
		out = (out << 1) | b1
	return out
```

Mình viết lại function bằng ngôn ngữ python và theo mình hiểu thì nó sẽ thực hiện dịch bit rồi OR với giá trị b1 kia (do mình định nghĩa nó thế, xinloi vì sự đặt tên vớ vẩn này). Vậy là đã có 2 function cần xử lý, giờ mình lấy dữ liệu từ flag1 và flag2 trong 2 function flagcheck

```python
flag1 = [0x3a,0x2c,0x6e,0xda,0xac,0xee,0xda,0x2e,0x2c,0xce]
flag2 = [0x41,0x14,0x13,0x19,0x33,0x2d,0x41,0x73,0x71,0x31]
```

![flag1 data](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/data_flag1.png)

![flag2 data](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/data_flag2.png)

Và... bài này để đi ngược lại từ đống dữ liệu flag kia về cái gốc thì mình ko nghĩ ra được cách gì nên mình dùng cách bần cùng nhất chính là **bruteforce** (not recommend). Và mình đã viết 1 đoạn script để xử lý cho mình đoạn này

Do nó có 2 phần, nên mình đã tách ra làm 2 để lấy từng phần 1

Phần đầu: *"X0r_1s_p0w"*

```python
strings = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

flag1 = [0x3a,0x2c,0x6e,0xda,0xac,0xee,0xda,0x2e,0x2c,0xce]

def reverse(x):
    j = 0
    for k in range(8):
        j = j * 2
        if((ord(x) >> (k & 0x1f) & 1) != 0):
            j = j + 1
    bin_2 = bin(j)[2:]
    while(len(bin_2) != 8):
        bin_2 = '0' + bin_2
    return int(bin_2, 2)

def myfunc(x, y):
    out = 0
    b1 = 0
    for i in range(31,-1,-1):
        b2 = 1 << (i & 0x1f) & int(y) != 0
        b3 = 1 << (i & 0x1f) & int(x) != 0
        if((b2 and b3) or (not(b2) and not(b3))):
            b1 = 0
        else:
            b1 = 1
        out = (out << 1) | b1
    return out

count = 0

# Get first part
for count in range(10):
    i = 0
    for i in range(len(strings)):
        temp = reverse(strings[i])
        if(myfunc(temp, 32) == flag1[count]):
            print(strings[i], end = "")
print()
```

Phần sau: *3rful_r3@1*

```python
strings = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

flag2 = [0x41,0x14,0x13,0x19,0x33,0x2d,0x41,0x73,0x71,0x31]

def myfunc(x, y):
    out = 0
    b1 = 0
    for i in range(31,-1,-1):
        b2 = 1 << (i & 0x1f) & int(y) != 0
        b3 = 1 << (i & 0x1f) & int(x) != 0
        if((b2 and b3) or (not(b2) and not(b3))):
            b1 = 0
        else:
            b1 = 1
        out = (out << 1) | b1
    return out

count = 0
flag = 'X0r_1s_p0w3'

# Get second part
while(count != len(flag2)):
    for i in range(len(strings)):
        if(myfunc(ord(flag[-1:]), ord(strings[i])) == flag2[count]):
            print(strings[i], end = "")            
            flag = flag + strings[i]
            count = count + 1
```

Sau khi lấy được phần đầu, mình có để vào phần sau, thì đoạn này khá guessing vì các từ kia là các từ có nghĩa, thì sau cái chữ *w* rất có thể là 'e', 'E', '3', và mình đã bắt đầu với '3'. Btw, nó chạy và cái vòng lặp của mình bị vô hạn ý, nhưng nó chạy và đưa cho mình flag nên lấy được phần sau mình tắt luôn :< 

Ghép 2 phần lại và check bằng file được cho để xem flag mình lấy được đã đúng chưa và đây là kết quả

![check_flag](/2023/Pragyan2023/Reverse_Engineering/bits_and_pieces/images/check_flag.png)

Vậy là flag mình lấy là đúng mặc dù script mình viết nó bị ngu ^_^

Flag: `p_ctf{X0r_1s_p0w3rful_r3@1}`

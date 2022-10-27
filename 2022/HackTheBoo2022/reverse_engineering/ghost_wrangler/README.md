# Ghost Wrangler
## Challenge

![challenge](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/images/challenge.png)

[File Source](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/rev_ghost_wrangler.zip)

## Solution

Sau khi nhận được file, mình decompile file xem có gì thì u là trời, hàm main không làm gì cả

![decompile](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/images/decompile.png)

À mà khoan, có hàm `get_flag` ở đó, mình quyết định mở lên xem có gì

![getFlagFunction](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/images/getFlagFunction.png)

Ok, vậy là biết flag sẽ được XOR với 0x13, nhưng, nó lấy data ở đâu để XOR? 

Sau một hồi mày mò, gdb tool các kiểu, mình cũng tìm được nơi giấu data

![foundData](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/images/foundData.png)

Mình có viết 1 đoạn script để lấy flag, thật ra cái này mang lên CyberChef cũng được hoặc lên mấy cái tool online đều xử lý được mà

```python
a=[0x5b,0x47,0x51,0x68,0x7b,0x27,0x66,0x7d,0x67,0x20,0x77,0x4c,0x71,0x6a,0x4c,0x67,0x7b,0x20,0x4c,0x74,0x7b,0x23,0x60,0x67,0x26,0x4c,0x23,0x75,0x4c,0x70,0x67,0x75,0x26,0x4c,0x63,0x27,0x26,0x67,0x32,0x6e]
for i in a:
    print(chr(i ^ 0x13), end="")
```

Chạy script và lấy flag

![getFlag](/2022/HackTheBoo2022/reverse_engineering/ghost_wrangler/images/getFlag.png)

Flag: `HTB{h4unt3d_by_th3_gh0st5_0f_ctf5_p45t!}`
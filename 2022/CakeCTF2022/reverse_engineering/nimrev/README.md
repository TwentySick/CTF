# NIMREV

## Challenge

![challenge](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/challenge.png)

## Solution
Firstly, checking this file seem this file enabled all things from `checksec`. So, what should I do now?

![check](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/check.png)

Let look around this file by ghidra.

![finding](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/finding.png)

Hehe, bingo, look at what I found there. The dataaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

![found](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/found.png)

Ok, I just found this by string "Wrong..." and leaked some data.

```
  *(undefined *)(plVar3 + 2) = 0xbc;
  *(undefined *)((long)plVar3 + 0x11) = 0x9e;
  *(undefined *)((long)plVar3 + 0x12) = 0x94;
  *(undefined *)((long)plVar3 + 0x13) = 0x9a;
  *(undefined *)((long)plVar3 + 0x14) = 0xbc;
  *(undefined *)((long)plVar3 + 0x15) = 0xab;
  *(undefined *)((long)plVar3 + 0x16) = 0xb9;
  *(undefined *)((long)plVar3 + 0x17) = 0x84;
  *(undefined *)(plVar3 + 3) = 0x8c;
  *(undefined *)((long)plVar3 + 0x19) = 0xcf;
  *(undefined *)((long)plVar3 + 0x1a) = 0x92;
  *(undefined *)((long)plVar3 + 0x1b) = 0xcc;
  *(undefined *)((long)plVar3 + 0x1c) = 0x8b;
  *(undefined *)((long)plVar3 + 0x1d) = 0xce;
  *(undefined *)((long)plVar3 + 0x1e) = 0x92;
  *(undefined *)((long)plVar3 + 0x1f) = 0xcc;
  *(undefined *)(plVar3 + 4) = 0x8c;
  *(undefined *)((long)plVar3 + 0x21) = 0xa0;
  *(undefined *)((long)plVar3 + 0x22) = 0x91;
  *(undefined *)((long)plVar3 + 0x23) = 0xcf;
  *(undefined *)((long)plVar3 + 0x24) = 0x8b;
  *(undefined *)((long)plVar3 + 0x25) = 0xa0;
  *(undefined *)((long)plVar3 + 0x26) = 0xbc;
  *(undefined *)((long)plVar3 + 0x27) = 0x82;
```

By my experience collected from some RE challenges, I tried XOR it with the number of character 'C', 'a', 'k', 'e' from ASCII table.

![realized](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/realized.png)

Ok, it's time to write a kiddie script to get the flag:

```python
s = [0xbc,0x9e,0x94,0x9a,0xbc,0xab,0xb9,0x84,0x8c,0xcf,0x92,0xcc,0x8b,0xce,0x92,0xcc,0x8c,0xa0,0x91,0xcf,0x8b,0xa0,0xbc,0x82]

for i in s:
    print(chr(i ^ 255), end="")
```
Flag:

![flag](https://github.com/TwentySick/CTF/blob/d671ca795459810020ec707edf2a4e35ad11dcb4/2022/CakeCTF2022/reverse_engineering/nimrev/images/flag.png)

```
CakeCTF{s0m3t1m3s_n0t_C} 
```

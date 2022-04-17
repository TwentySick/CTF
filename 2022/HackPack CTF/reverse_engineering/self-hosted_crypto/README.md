# Self-Hosted Crypto
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/10257b5552745817d6bdb41ac4ed81ea0ac1ed0d/2022/HackPack%20CTF/reverse_engineering/self-hosted_crypto/images/challenge.png)
## Solution
Convert content from file encrypted to Hex\
![Hex](https://github.com/TwentySick/CTF/blob/10257b5552745817d6bdb41ac4ed81ea0ac1ed0d/2022/HackPack%20CTF/reverse_engineering/self-hosted_crypto/images/get_hex.png)\
Then convert to Decimal, so I get an array of numbers 
```
115 121 110 116 136 78 108 111 65 113 108 86 113 64 65 46 62 46 138 10
```
And here is the pseudocode from the file giving by challenge\
![decompiler](https://github.com/TwentySick/CTF/blob/10257b5552745817d6bdb41ac4ed81ea0ac1ed0d/2022/HackPack%20CTF/reverse_engineering/self-hosted_crypto/images/decompiler.png)\
After reading, I wrote a short python script to calculate.
```python
list = [115, 121, 110, 116, 136, 78, 108, 111, 65, 113, 108, 86, 113, 64, 65, 46, 62, 46, 138, 10]

out = []
for number in list:
    number = number - 13
    out.append(number)

print(*out)
```
It just minus each number by 13, then convert them to ASCII and get the flag.
![solved](https://github.com/TwentySick/CTF/blob/10257b5552745817d6bdb41ac4ed81ea0ac1ed0d/2022/HackPack%20CTF/reverse_engineering/self-hosted_crypto/images/solved.png)\
Flag
```
flag{A_b4d_Id34!1!}
```

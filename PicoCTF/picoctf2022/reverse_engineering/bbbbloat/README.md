# bbbbloat

## Challenge
![alt text](https://github.com/TwentySick/CTF/blob/85fcb0b8ea4ad05ad0f8b9b864cf3133788b9567/PicoCTF/picoctf2022/reverse_engineering/bbbbloat/images/challenge.png)

## Solution
Using ghidra to check this file, I can easily see the condition.\
![alt text](https://github.com/TwentySick/CTF/blob/85fcb0b8ea4ad05ad0f8b9b864cf3133788b9567/PicoCTF/picoctf2022/reverse_engineering/bbbbloat/images/ghidra.png)\
Catch it, the number is 549255\
![alt text](https://github.com/TwentySick/CTF/blob/85fcb0b8ea4ad05ad0f8b9b864cf3133788b9567/PicoCTF/picoctf2022/reverse_engineering/bbbbloat/images/output.png)\
Flag:
```
picoCTF{cu7_7h3_bl047_44f74a60}
```

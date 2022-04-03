# unpackme
## Challenge
![alt text](https://github.com/TwentySick/CTF/blob/19453aa098fb72045220079afc3408ad441b0ca1/PicoCTF/picoctf2022/reverse_engineering/unpackme/images/Screenshot_2022-04-03_01_51_43.png)\
## Solution
I use upx to extract this file, then I use ghidra to check\
![alt text](https://github.com/TwentySick/CTF/blob/19453aa098fb72045220079afc3408ad441b0ca1/PicoCTF/picoctf2022/reverse_engineering/unpackme/images/Screenshot_2022-04-03_01_51_54.png)\
Easy to see here is the condition\
![alt text](https://github.com/TwentySick/CTF/blob/19453aa098fb72045220079afc3408ad441b0ca1/PicoCTF/picoctf2022/reverse_engineering/unpackme/images/Screenshot_2022-04-03_01_55_15.png)\
And flag was found\
![alt text](https://github.com/TwentySick/CTF/blob/19453aa098fb72045220079afc3408ad441b0ca1/PicoCTF/picoctf2022/reverse_engineering/unpackme/images/Screenshot_2022-04-03_01_55_55.png)\
Flag
```
picoCTF{up><_m3_f7w_5769b54e}
```

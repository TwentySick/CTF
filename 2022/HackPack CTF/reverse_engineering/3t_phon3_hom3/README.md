# 3T PHON3 HOM3
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/c34a1a183797e1b8a2f504df71c3415f9cc786a9/2022/HackPack%20CTF/reverse_engineering/3t_phon3_hom3/images/challenge.png)
## Solution
Using apktool to decompile apk file,
```bash
apktool d maybeaninvasionapp.apk 
```
Moving to new folder created by apktool, I use grep to find flag
```bash
grep -nr -I 'flag{' .
```
![solved](https://github.com/TwentySick/CTF/blob/c34a1a183797e1b8a2f504df71c3415f9cc786a9/2022/HackPack%20CTF/reverse_engineering/3t_phon3_hom3/images/solved.png)\
Flag:
```
flag{resourceful_find!}
```

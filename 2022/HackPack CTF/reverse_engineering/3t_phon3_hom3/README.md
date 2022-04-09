# 3T PHON3 HOM3
## Challenge
## Solution
Using apktool to decompile apk file,
```bash
apktool d maybeaninvasionapp.apk 
```
Moving to new folder created by apktool, I use grep to find flag
```bash
grep -nr -I 'flag' .
```
Flag:
```
flag{resourceful_find!}
```

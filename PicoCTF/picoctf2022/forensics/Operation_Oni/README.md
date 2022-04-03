# Operation Oni
## Challenge
![alt text](https://github.com/TwentySick/CTF/blob/ecf866c90700956caa98d60d5d1c3e89f48fc612/PicoCTF/picoctf2022/forensics/Operation_Oni/images/challenge.png)
## Solution
Download this file, extracting by gzip, I've got a file img here\
Mounting this file, I checked file .ash\_history and found something funny\
![alt text](https://github.com/TwentySick/CTF/blob/ecf866c90700956caa98d60d5d1c3e89f48fc612/PicoCTF/picoctf2022/forensics/Operation_Oni/images/ssh_key.png)\
Remote to machine with the key I've found, I catch the flag\
![alt text](https://github.com/TwentySick/CTF/blob/ecf866c90700956caa98d60d5d1c3e89f48fc612/PicoCTF/picoctf2022/forensics/Operation_Oni/images/remote.png)\
Flag
```
picoCTF{k3y_5l3u7h_75b85d71}
```

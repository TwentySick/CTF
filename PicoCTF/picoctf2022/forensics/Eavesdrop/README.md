# Eavesdrop

## Challenge
![alt text](https://github.com/TwentySick/CTF/blob/b669ec453994feba5264f936b86cfe0406d31c54/PicoCTF/picoctf2022/forensics/Eavesdrop/images/challenge.png)\
## Solution

Using Wireshark, I can follow the conversation from TCP stream\
Boooom, catch it\
I have ```openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123``` here\
![alt text](https://github.com/TwentySick/CTF/blob/b669ec453994feba5264f936b86cfe0406d31c54/PicoCTF/picoctf2022/forensics/Eavesdrop/images/stream_0.png)\
Up to stream 2, I've got the file.des3\
![alt text](https://github.com/TwentySick/CTF/blob/b669ec453994feba5264f936b86cfe0406d31c54/PicoCTF/picoctf2022/forensics/Eavesdrop/images/stream_3.png)\
Exporting this with the bash that I catch from stream 0, so I found the flag\
![alt text](https://github.com/TwentySick/CTF/blob/b669ec453994feba5264f936b86cfe0406d31c54/PicoCTF/picoctf2022/forensics/Eavesdrop/images/out.png)\
Flag
```
picoCTF{nc_73115_411_0ee7267a}
```

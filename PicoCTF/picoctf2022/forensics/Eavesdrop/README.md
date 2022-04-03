# Eavesdrop

## Challenge

## Solution

Using Wireshark, I can follow the conversation from TCP stream\
Boooom, catch it\
I have ```bash
openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123
``` here\
Up to stream 2, I've got the file.des3\
Exporting this with the bash that I catch from stream 0, so I found the flag\
Flag
```
picoCTF{nc_73115_411_0ee7267a}
```

# Star Pcap
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/a10324581a23c6077084f9e075a5b07999a33ca1/2022/Space%20Heroes%20CTF/forensics/star_pcap/images/challenge.png)
## Solution
Reading file pcap, looking at 'icmp.code', I found this sequence:
```
c2hjdGZ7TDBnMWMtaSQtdGgzLWJlZ2lOTmluZy0wZi13aSRkb019
```
Decode with base64 and get the flag\
![decode](https://github.com/TwentySick/CTF/blob/a10324581a23c6077084f9e075a5b07999a33ca1/2022/Space%20Heroes%20CTF/forensics/star_pcap/images/decode.png)\
\Flag:
```
shctf{L0g1c-i$-th3-begiNNing-0f-wi$doM}
```

# Buzz's Secret Watch (Part 1)
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/3c0ec7f12eeeffaf28d3d0c737e457861dcf0e06/2022/Space%20Heroes%20CTF/forensics/buzz's_secret_watch_part_1/images/challenge.png)
## Solution
Use ffmpeg to extract frame from the video
```bash
ffmpeg -i buzzsaw.avi -vf fps=10 %d.png
```
Those image here attended like from binary base\
(If you look at the led light, you will recognize that)
Binary Base:
```
01110011 01101000 01100011 01110100 01100110 01111011 01010011 01101000 00110011 01110010 00110001 01100110 01100110 00101101 01110100 01001000 00110001 01110011 00101101 01101001 01110011 00101101 01101110 00110000 00101101 01110100 00110001 01101101 00110011 00101101 01110100 00110000 00101101 01110000 01000001 01101110 00110001 01100011 01111101
```
Converting from binary base, we've got the flag\
Flag:
```
shctf{Sh3r1ff-tH1s-is-n0-t1m3-t0-pAn1c}
```

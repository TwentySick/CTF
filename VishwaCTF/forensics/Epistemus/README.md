# Epistemus
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/636b9d0dbde80bcb8b9aba5badedab08ef2f5690/VishwaCTF/forensics/Epistemus/images/challenge.png)
## Solution
Go to [the link](https://github.com/RohitStark/Epistemus) from the image giving\
Download file rar and use twitter secret message to take the password

Tweet:
```
I dｏｎ't ｔhiｎk tｈⅰs iｓ the ｒｉght plaｃe to be sｅaｒcｈіｎg ｆｏｒ ａｎｙtｈiｎg. Nothing bｕt emptiｎesｓ aｎｄ ⅴoіd. Liｔerally， ａ wastｅ οｆ time
```
=> Hiddent Message: alright the password is `r1ghtpl4c3`\
![tweet](https://github.com/TwentySick/CTF/blob/f2c2903e51093b322948cc189608c95435a16626/VishwaCTF/forensics/Epistemus/images/password.png)\
Unrar with this password then find flag with grep\
![find flag](https://github.com/TwentySick/CTF/blob/f2c2903e51093b322948cc189608c95435a16626/VishwaCTF/forensics/Epistemus/images/solved.png)\
Flag
```
vishwactf{th1ng$_a43_n0t_wh4t_th3y_4lw4y$_$33m}
```

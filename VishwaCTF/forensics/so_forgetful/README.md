# So Forgetful!
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/d13af34ff395f5a7e17068277618f85151632c58/VishwaCTF/forensics/so_forgetful/images/challenge.png)
## Solution
Open wireshark, display filter 'http' and find POST\
![wireshark](https://github.com/TwentySick/CTF/blob/d13af34ff395f5a7e17068277618f85151632c58/VishwaCTF/forensics/so_forgetful/images/wireshark.png)\
Look at what I have here\
```
userid=spiveyp&pswrd=S04xWjZQWFZ5OQ%3D%3D
```
replace %3D by = in the pswrd and decode from base64\
![decode](https://github.com/TwentySick/CTF/blob/d13af34ff395f5a7e17068277618f85151632c58/VishwaCTF/forensics/so_forgetful/images/decode.png)\
Flag 
```
vishwactf{KN1Z6PXVy9}
```

# Corrupt Company
## Challenge
![Challenge](https://github.com/TwentySick/CTF/blob/79cefadc5945aacea57caa30b183156a090a016e/2022/DCTF/misc/corrupt_company/images/challenge.png)
## Solution
Using binwalk, I easily can see that file embed with two file
![Binwalk](https://github.com/TwentySick/CTF/blob/79cefadc5945aacea57caa30b183156a090a016e/2022/DCTF/misc/corrupt_company/images/Screenshot%202022-04-17%20194915.png)

But extract this file and turn on ShowHiddenFiles mode, I can't find the "not_important.txt" file

Check Hex from this file

Ah shiet, they changed something here

![before](https://github.com/TwentySick/CTF/blob/79cefadc5945aacea57caa30b183156a090a016e/2022/DCTF/misc/corrupt_company/images/Screenshot%202022-04-17%20195326.png)

Turn it back to true form and extract again by binwalk, the flag was found

![after](https://github.com/TwentySick/CTF/blob/79cefadc5945aacea57caa30b183156a090a016e/2022/DCTF/misc/corrupt_company/images/after.png)

Flag:
```
dctf{pl5_z1p_1t_w3_4r3_4_g00d_c0mp4ny}
```

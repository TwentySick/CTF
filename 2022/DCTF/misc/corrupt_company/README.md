# Corrupt Company
## Challenge
## Solution
using binwalk, I easily can see that file embed with two file

But extract this file and turn on ShowHiddenFiles mode, I can't find the "not_important.txt" file

Check Hex from this file

Ah shiet, they changed something here

Turn it back to true form and extract again by binwalk, the flag was found

Flag:
```
dctf{pl5_z1p_1t_w3_4r3_4_g00d_c0mp4ny}
```

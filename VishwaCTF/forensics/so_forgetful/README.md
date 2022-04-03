# So Forgetful!
## Challenge
## Solution
Open wireshark, display filter 'http' and find POST\
Look at what I have here\
```
userid=spiveyp&pswrd=S04xWjZQWFZ5OQ%3D%3D
```
replace %3D by = in the pswrd and decode from base64\
Flag 
```
vishwactf{KN1Z6PXVy9}
```
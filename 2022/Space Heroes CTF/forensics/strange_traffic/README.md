# Strange Traffic
## Challenge
![challenge](https://github.com/TwentySick/CTF/blob/13adbe39365be04af5443dd157bf9e831c7caf91/2022/Space%20Heroes%20CTF/forensics/strange_traffic/images/challenge.png)
## Solution
Exporting as plain text from file pcap, I need delete to get only the number from packet.\
Number:
```
31 35 46 20 33 42 26 20 35 30 49 37 31 57 33 11 19 57 20 35 4 57 20 5 49 37 52 57 35 18 57 49 4 47 18 19 57 34 18 20 6 57 50 18 57 30 49 21 20 35 2 49 34 42 27 28
```
And I wrote that script after look at keyboard
```Python3
list=[31,35,46,20,33,42,26,20,35,30,49,37,31,57,33,11,19,57,20,35,4,57,20,5,49,37,52,57,35,18,57,49,4,47,18,19,57,34,18,20,6,57,50,18,57,30,49,21,20,35,2,49,34,42,27,28]

keyboard=['esc','`','1','2','3','4','5','6','7','8','9','0','-','=','backspace','tab','q','w','e','r','t','y','u','i','o','p','[',']','enter','capslock','a','s','d','f','g','h','j','k','l',';','\'','\\','enter','shift','z','x','c','v','b','n','m',',','.','/','shift','ctrl','superkey','alt','space','alt','superkey']

out=[]

for i in list:
    out.append(keyboard[i])

print(*out)
```
Deleting space and 'enter', replacing \'[\' with \'{\', \']\' with \'}\', \'alt\' with \'\_\', I got the flag\
![running](https://github.com/TwentySick/CTF/blob/13adbe39365be04af5443dd157bf9e831c7caf91/2022/Space%20Heroes%20CTF/forensics/strange_traffic/images/run_script.png)\
Flag:
```
shctf{thanks_f0r_th3_t4nk._he_n3ver_get5_me_anyth1ng}
```

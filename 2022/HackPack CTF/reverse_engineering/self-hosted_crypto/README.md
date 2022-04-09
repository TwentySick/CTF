# Self-Hosted Crypto
## Challenge
## Solution
Convert character from file encrypted to decimal (converting to Hex is middle step, I convert to Hex then convert from Hex to Decimal because I'm stupid at math :( )\
So I get a array of numbers 
```
115 121 110 116 136 78 108 111 65 113 108 86 113 64 65 46 62 46 138 10
```
And here is the pseudocode from the file giving by challenge
After reading, I wrote a short python script to calculate.
```python
[115, 121, 110, 116, 136, 78, 108, 111, 65, 113, 108, 86, 113, 64, 65, 46, 62, 46, 138, 10]

out = []
for number in list:
    number = number - 13
    out.append(number)

print(*out)
```
It just minus each number with 13, then convert them to ASCII and get the flag.
Flag
```
flag{A_b4d_Id34!1!}
```

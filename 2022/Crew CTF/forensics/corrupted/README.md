# Corrupted
## Challenge
## Solution
First, I check hex this file.
This file is a mbr file with a lot of 41 in head, so I delete all 41 from head and mount this file (or use some tool like FTK Tool or Autopsy)
Deleting all 41 from head, I got a mbr file. Mount this file and check folder pictures. I get the flag from file Capture (1).PNG
![solved]()
Flag:
```
crew{34sY_C0rrupt3D_GPT}
```

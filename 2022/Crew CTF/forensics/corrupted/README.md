# Corrupted
## Challenge
![Challenge](https://github.com/TwentySick/CTF/blob/be8f87f8d96ba7fe40b9e412ca37120bb34773b3/2022/Crew%20CTF/forensics/corrupted/images/challenge.png)
## Solution
First, I check hex this file.

This file is a mbr file with a lot of 41 in head, so I delete all 41 from head and mount this file (or use some tool like FTK Tool or Autopsy)

![Before](https://github.com/TwentySick/CTF/blob/be8f87f8d96ba7fe40b9e412ca37120bb34773b3/2022/Crew%20CTF/forensics/corrupted/images/before.png)

Deleting all 41 from head, I got a mbr file. 

![After](https://github.com/TwentySick/CTF/blob/be8f87f8d96ba7fe40b9e412ca37120bb34773b3/2022/Crew%20CTF/forensics/corrupted/images/after.png)

Mount this file and check folder pictures. I get the flag from file Capture (1).PNG

![solved](https://github.com/TwentySick/CTF/blob/be8f87f8d96ba7fe40b9e412ca37120bb34773b3/2022/Crew%20CTF/forensics/corrupted/images/solved.png)

Flag:
```
crew{34sY_C0rrupt3D_GPT}
```

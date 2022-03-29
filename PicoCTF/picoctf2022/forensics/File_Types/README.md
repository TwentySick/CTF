Check hex file Flag.pdf => Type of this file is .sh

```bash
cp Flag.pdf Flag.sh
chmod 700 Flag.sh
./Flag.sh
```
After that, I've got a file with head is !<arch>

```bash
ar x flag
```
The file extracted is in cpio type
```bash
mkdir extract
cpio -i < flag.cpio -D extract
cd extract
```
And, we have a lots of zip type here
```bash
bzip2 -d flag
mv flag.out flag
cp flag flag.gz
gzip -d flag.gz
lzip -d flag
lz4 -d flag.out flag_1
cp flag_1 flag.lzma
mkdir extract2
mv flag.lzma extract2
cd extract2
lzma -d flag.lzma
mkdir extract3
cp flag flag.lzo
mv flag.lzo extract3
cd extract3
lzop -x flag.lzo
lzip -d flag
7z -x flag.out
cat flag
```
After extracting those file, we've got a hex sequence. Using cyberchef to decode it, we've got the flag (I prayed to God for who is created this chall)

```
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f39353063346665657d0a
```

Flag
```
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_950c4fee}
```


## Description

This is a really weird text file TXT? Can you find the flag?

## Hints

1. How do operating systems know what kind of file it is? (It's not just the ending!
2. Make sure to submit the flag as picoCTF{XXXXX}


## How to Solve

Cek file extension

```
┌──(free㉿free)-[~/CTF/picoCTF/Forensics/extensions]
└─$ file flag.txt                                     
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced

```

Ubah extension file dari `.txt` menjadi `.png`

![Alt text](images/flag.png)
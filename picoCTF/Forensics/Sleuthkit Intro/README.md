
## Description

Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
- Download disk image
- Access checker program: nc saturn.picoctf.net 64605
  

## Hints

**(None)**



## How to Solve


```
┌──(free㉿free)-[/mnt/…/CTF/picoCTF/Forensics/Sleuthkit Intro]
└─$ wget https://artifacts.picoctf.net/c/164/disk.img.gz                     
--2024-02-22 17:15:11--  https://artifacts.picoctf.net/c/164/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 18.67.172.13, 18.67.172.71, 18.67.172.25, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|18.67.172.13|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29714372 (28M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                               100%[===================================================================================>]  28.34M  5.79MB/s    in 4.9s    

2024-02-22 17:15:18 (5.77 MB/s) - ‘disk.img.gz’ saved [29714372/29714372]

                                                                                                                                                                      
┌──(free㉿free)-[/mnt/…/CTF/picoCTF/Forensics/Sleuthkit Intro]
└─$ gunzip disk.img.gz 
                                                                                                                                                                      
┌──(free㉿free)-[/mnt/…/CTF/picoCTF/Forensics/Sleuthkit Intro]
└─$ mmls disk.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
                                                                                                                                                                      
┌──(free㉿free)-[/mnt/…/CTF/picoCTF/Forensics/Sleuthkit Intro]
└─$ nc saturn.picoctf.net 64605
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
picoCTF{mm15_f7w!}


```


## Description

Every file gets a flag.
The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here.


## Hints

**(None)**




## How to Solve

Extract file tersembunyi dalam file flag.png

```
└─$ binwalk -e flag.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2858, uncompressed size: 3015, name: secret/flag.png
42897         0xA791          End of Zip archive, footer length: 22

```

Cek struktur dari folder hasil ekstraksi

```
└─$ tree _flag.png.extracted               
_flag.png.extracted
├── 29
├── 29.zlib
├── 9B3B.zip
└── secret
    └── flag.png

2 directories, 4 files

```

Terlihat flag berada dalam direktori `_flag.png.extracted/secret/flag.png`

![Alt text](images/flag.png)
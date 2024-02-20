## Descripton

Figure out how they moved the flag.


## Hints 

- What are some other ways to hide data?



## How to Solve


Dari hint yang diberikan mengarah pada kata kunci **hide data**. file yang diberikan berupa hasil caputre jaringan dari wireshark, wireshark sendiri menyediakan fitur atau opsi untuk mengekspor objek-objek yang ditransfer dalam suatu sesi.

![Alt text](images/obj.png)

Pertama setelah melakukan export saya membuka apa saja isi dari file, file instruction.txt dan plan disini berisi teks dengan struktur enkripsi ROT13
```
instruction.txt :   GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
plan            :   VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
```  

Setelah di dekripsi isi file berisi sebuah pesan

```
TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN.
I USED THE PROGRAM AND HID IT WITH-DUEDILIGENCE. CHECKOUT THE PHOTOS
```

Isi pesan tersebut mengarah pada file program.deb . seperti yang kita tau file dengan ekstensi .deb digunakan untuk menyimpan dan mengelola paket perangkat lunak yang diinstal di sistem Linux. beberapa langkah yang saya gunakan untuk tidak menginstall program tersebut melainkan dengan meng-export dan menginvestigasi programnya. 

```
┌──(free㉿free)-[picoCTF/Forensics/Trivial Flag Transfer Protocol/export]
└─$ mkdir program
                                                                                                                                                                      
┌──(free㉿free)-[picoCTF/Forensics/Trivial Flag Transfer Protocol/export]
└─$ dpkg -x program.deb program
                                                                                                                                                                      
┌──(free㉿free)-[picoCTF/Forensics/Trivial Flag Transfer Protocol/export]
└─$ ls
instructions.txt  picture1.bmp  picture2.bmp  picture3.bmp  plan  program  program.deb
                                                                                                                                                                      
┌──(free㉿free)-[picoCTF/Forensics/Trivial Flag Transfer Protocol/export]
└─$ tree program                       
program
└── usr
    ├── bin
    │   └── steghide
    └── share
        ├── doc
        │   └── steghide
        │       ├── ABOUT-NLS.gz
        │       ├── BUGS
        │       ├── changelog.Debian.amd64.gz
        │       ├── changelog.Debian.gz
        │       ├── changelog.gz
        │       ├── copyright
        │       ├── CREDITS
        │       ├── HISTORY
        │       ├── LEAME.gz
        │       ├── README.gz
        │       └── TODO
        ├── locale
        │   ├── de
        │   │   └── LC_MESSAGES
        │   │       └── steghide.mo
        │   ├── es
        │   │   └── LC_MESSAGES
        │   │       └── steghide.mo
        │   ├── fr
        │   │   └── LC_MESSAGES
        │   │       └── steghide.mo
        │   └── ro
        │       └── LC_MESSAGES
        │           └── steghide.mo
        └── man
            └── man1
                └── steghide.1.gz

17 directories, 17 files

```


Terlihat pada direktori /bin bahwa program ini berisi steghide. steghide sendirinya merupakan program untuk menyembuyikan file di dalam file. Langkah terakhir yaitu untuk melakukan check apakah ada file tersembunyi di antara `picture1.bmp` `picture2.bmp` `picture3.bmp`. Sebelum nya pada pesan plan mengatakan ( I USED THE PROGRAM AND HID IT WITH-**DUEDILIGENCE**. CHECKOUT THE PHOTOS ) yang mungkin akan mengarah pada passphrase atau password saat meng-extract file tersebut.


```
┌──(free㉿free)-[export/program/usr/bin]
└─$ ./steghide extract -sf ../../../picture1.bmp || ./steghide extract -sf ../../../picture2.bmp || ./steghide extract -sf ../../../picture3.bmp
Enter passphrase: 
steghide: could not extract any data with that passphrase!
Enter passphrase: 
steghide: could not extract any data with that passphrase!
Enter passphrase: 
wrote extracted data to "flag.txt".
                                                                                                                                                                      
┌──(free㉿free)-[export/program/usr/bin]
└─$ cat flag.txt                                                                                 
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```
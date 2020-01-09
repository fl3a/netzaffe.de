---
layout: post
date: "2020-01-08 08:50:05 +0100"
image:
toc: false
tags:
- Linux
- uberspace
- howto
- Open Source
- apache2
- Logs
- Analytics
- Datenbank 
title: "GoAccess: Persistierung von WebLogs in Tokyo Cabinet Datenbank"
---

```  
checking for tchdbnew in -ltokyocabinet... no
configure: error: *** Missing development libraries for Tokyo Cabinet Database
```  
  
```  
toast add https://fallabs.com/tokyocabinet/tokyocabinet-1.4.48.tar.gz
```  

```  
toast find tokyocabinet
```  
```  
wget -O- https://fallabs.com/tokyocabinet/
--2020-01-07 23:05:25--  https://fallabs.com/tokyocabinet/
Auflösen des Hostnamen »fallabs.com«.... 49.212.133.108
Verbindungsaufbau zu fallabs.com|49.212.133.108|:443... verbunden.
HTTP Anforderung gesendet, warte auf Antwort... 200 OK
Länge: 6819 (6,7K) [text/html]
In »»STDOUT«« speichern.

100%[===================================================================================================================>] 6.819       --.-K/s   in 0s      

2020-01-07 23:05:26 (127 MB/s) - auf die Standardausgabe geschrieben [6819/6819]


tokyocabinet
  version 1.4.48: found
    urls:
       https://fallabs.com/tokyocabinet/tokyocabinet-1.4.48.tar.gz
```  


```
toast arm tokyocabinet
```


```
echo $LD_LIBRARY_PATH 
/home/fl3a/.toast/armed/lib
```


```
make
./configure --enable-utf8 --enable-geoip=legacy --enable-tcb=btree  --prefix=$HOME
```

```
Your build configuration:

  Prefix         : /home/fl3a
  Package        : goaccess
  Version        : 1.3
  Compiler flags :  -pthread
  Linker flags   : -lnsl -ltokyocabinet -lncursesw -lGeoIP -lpthread   -lz -lbz2 -ltokyocabinet -lrt -lc
  Dynamic buffer : no
  Geolocation    : GeoIP Legacy
  Storage method : On-disk B+ Tree Database (Tokyo Cabinet)
  TLS/SSL        : no
  Bugs           : goaccess@prosoftcorp.com
```

```
ls -l logs/webserver/
insgesamt 15668
-rw-r--r--. 1 root root  582507  9. Jan 10:45 access_log
-rw-r--r--. 1 root root 1839549  9. Jan 03:54 access_log.1
-rw-r--r--. 1 root root 2194096  8. Jan 03:59 access_log.2
-rw-r--r--. 1 root root 2115343  7. Jan 03:59 access_log.3
-rw-r--r--. 1 root root 2161323  6. Jan 03:59 access_log.4
-rw-r--r--. 1 root root 1999593  5. Jan 03:59 access_log.5
-rw-r--r--. 1 root root 2332544  4. Jan 03:58 access_log.6
-rw-r--r--. 1 root root 2744661  3. Jan 03:59 access_log.7
```

```
#!/bin/bash
goaccess -p $HOME/etc/goaccess/goaccess.conf \
  --load-from-disk --db-path=$HOME/goaccess.db/ --keep-db-files \
  -a -o ~/html/index.html
```

```
#!/bin/bash
goaccess -p $HOME/etc/goaccess/goaccess.conf \
  --process-and-exit $HOME/logs/webserver/access_log.1 \
  --load-from-disk --db-path=$HOME/goaccess.db/ --keep-db-file
```  

```
5 4 * * * /home/cleo/bin/goaccessParseYesterdaysLog
10 4 * * * /home/cleo/bin/goaccess2html
```


---
title: GoAccess auf Uberspace installieren
tags:
- Linux
- uberspace
- howto
- Open Source
layout: post
image: /assets/imgs/goaccess-ncurces-console-screenshot.png
---
<figure>
  <img src="/assets/imgs/goaccess-ncurces-console-screenshot.png" alt="" />
  <figcaption>Screenshot: GoAccess auf der Konsole</figcaption>
</figure>
https://goaccess.io/ MIT Lizenz Analyse Logfile https://github.com/allinurl/goaccess
```
wget https://github.com/allinurl/goaccess/archive/v1.3.tar.gz
tar xfzv v1.3.tar.gz 
rm v1.3.tar.gz 
cd goaccess-1.3/
autoreconf -fiv
```
https://wiki.uberspace.de/system:toast  toast - packageless package manager for Unix systems and non-root users 
```
toast arm gettext
```
autoreconf -fiv
./configure --enable-geoip --enable-utf8 --prefix=/home/fl3a
make
make install
cd 
mkdir etc
cd etc
curl -O  https://raw.githubusercontent.com/allinurl/goaccess/master/config/goaccess.conf
```

```
vim ~/etc/goaccess.conf
```
```
log-format COMBINED
log-file /home/fl3a/logs/access_log
```

```
goaccess -a -p ~/etc/goaccess.conf 
```

* * *
https://goaccess.io/
http://www.toastball.net/toast/
https://wiki.uberspace.de/system:toast

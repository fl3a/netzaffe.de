---
title: GoAccess auf Uberspace installieren
tags:
- Linux
- uberspace
- howto
- Open Source
- apache2
- Logs
- Analytics
layout: post
toc: true
image: /assets/imgs/goaccess-ncurces-console-screenshot.png
---
<figure>
  <img src="/assets/imgs/goaccess-ncurces-console-screenshot.png" alt="" />
  <figcaption>Screenshot: GoAccess auf der Konsole</figcaption>
</figure>
https://goaccess.io/ MIT Lizenz Analyse Logfile https://github.com/allinurl/goaccess
i
## Installation
```
mkdir ~/repos
cd ~/repos
 git clone https://github.com/allinurl/goaccess.git
cd goaccess/
```
```
autoreconf -fiv
```
```
./configure --enable-geoip --enable-utf8 --prefix=/home/fl3a
make
make install
```

### Update von gettext

Wenn `autoreconf -fiv` mit folgender Meldung abricht: 

```
autoreconf: Entering directory `.'
autoreconf: running: autopoint --force
autopoint: *** The AM_GNU_GETTEXT_VERSION declaration in your configure.ac  
file requires the infrastructure from gettext-0.18 but this version
is older. Please upgrade to gettext-0.18 or newer.
autopoint: *** Stop.
autoreconf: autopoint failed with exit status: 1
```

https://wiki.uberspace.de/system:toast  toast - packageless package manager for Unix systems and non-root users 
```
toast arm gettext
```

## Konfiguration

```
vim ~/etc/goaccess.conf
```
```
log-format COMBINED
log-file /home/fl3a/logs/access_log
```

## Nutzung

### Beispiele

```
goaccess -a -p ~/etc/goaccess.conf 
```
### Hotkeys

Hier noch ein paar Hotkeys für die Bedienung der Ncurses Oberfläche von GoAccess,
also auf der Kommandozeile.

* kpkpk
* jojoj
* fefw

* * *

https://goaccess.io/
http://www.toastball.net/toast/
https://wiki.uberspace.de/system:toast

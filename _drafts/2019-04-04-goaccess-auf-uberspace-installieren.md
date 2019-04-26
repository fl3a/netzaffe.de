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

* Log Fomate: Apache, Nginx, Amazon S3
* Ausgabe: Konsole, HTML, JSON, CSV

## Installation
```
mkdir ~/repos
```
```
cd ~/repos
```
```
git clone https://github.com/allinurl/goaccess.git
```
```
cd goaccess/
```
```
autoreconf -fiv
```
```
./configure --enable-geoip --enable-utf8 --prefix=/home/fl3a
```
```
make
```
```
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
goaccess -p ~/etc/goaccess/goaccess.conf ~/logs/access_log 
```

```
grep '^.*-\ - \[22/Apr/2019' ~/logs/access_log | goaccess  -p ~/etc/goaccess/goaccess.conf
```
```
zcat ~/logs/access_log.*.gz | goaccess --log-format COMBINED 
```

### Hotkeys

Hier noch ein paar gebräuckliche Hotkeys für die Bedienung der von GoAccess auf der Konsole:

* `TAB`, die Sektionen anwählen (nach unten)
* `SHIFT` + `TAB`, die Sektionen anwählen (nach oben)
* `ENTER`, das angwählte Sektion öffen
* `1-9`, wählt die Sektion mit der Nummer direkt an, z.B. `4` für die *404er HTTP Status Codes*
* `j`, in Sektion nach unten scrollen
* `k`, in Sektion nach oben scrollen
* `h`, öffnet die Hilfe
* `q`, schließt das aktive Element, z.B. Hilfe, Sektion oder GoAceccess selbst

* * *

https://goaccess.io/
http://www.toastball.net/toast/
https://wiki.uberspace.de/system:toast

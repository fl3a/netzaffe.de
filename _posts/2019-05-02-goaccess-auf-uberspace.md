---
title: GoAccess auf Uberspace
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
last_modified_at: 2019-05-12
---
<figure>
  <img src="/assets/imgs/goaccess-ncurces-console-screenshot.png" 
  alt="Screenshot: GoAccess Web-Analytics auf der Konsole" />
  <figcaption>Screenshot: GoAccess Web-Analytics auf der Konsole</figcaption>
</figure>
Nach einer längeren Suche nach einem *Apache Log Viewer*, der auf der Konsole läuft
und *404er/Not found* aussagekräftig darstellen kann, 
bin ich auf [GoAccess](https://goaccess.io/) gestoßen.

[GoAccess](https://github.com/allinurl/goaccess) ist eine schlanke, 
FLOSS (MIT Lizenz) Web Analytics-Software, die die Zugriffsdateien des Webservers, 
die sog. Access-Logs auswertet. Die Anwendung kann mit z.B. Apache-, Nginx-, Google Cloud Storage-, 
oder Amazon-S3-Logs umgehen,
läuft mit einer sogar recht ansprechenden Nucurse-Oberfläche[^ncurses] auf der Konsole
und kann zudem noch Exporte nach JSON, CSV und HTML, was bedeutet, 
dass die GoAccess auch wie Matomo(ehemals Piwik) oder Google-Analytics auch über den Browser bedienbar ist.

Hier beschreibe ich die Installation von GoAccess aus dem Quellcode auf Uberspace 6, 
bei U7 ist GoAccess per Default mit an Board(und alle so yeah)[^ureact]. 
Zudem gebe dir neben der Konfiguration von GoAccess auch Einblick in die Nutzung auf der Shell,
ein paar nette Tipps und nützliche Beispiele mit an die Hand.

Der Großteil dieses Artikels, auch die Installation sollte so generisch sein, 
dass man ihn recht einfach auf andere Systeme übertragen kann.<!--break-->

Es sei noch angemerkt, dass GoAccess auch Ausgaben in Realtime erzeugen kann,
dieses Feature ist allerdings für die Anwendung auf Uberspace 6 irrelvant, da 
die Access-Logs dort nicht live geschrieben werden[^logs].

## Installation von GoAccess
```
mkdir ~/repos
```
```
cd ~/repos
```

Wir besorgen uns den Quelltext von GoAccess via Git.
```
git clone https://github.com/allinurl/goaccess.git
```
```
cd goaccess/
```
```
autoreconf -fiv
```
Es folgt der *Dreisatz*: 
```
./configure --enable-geoip --enable-utf8 --prefix=$HOME
```
```
make
```
```
make install
```

### Update von gettext

Wenn `autoreconf -fiv` mit z.B. folgender Meldung abricht,
dann ist das benötigte *gettext* auf dem System zu alt.
Das war bei mir auf einer Uberspace 6 Instanz der Fall.

```
autoreconf: Entering directory `.'
autoreconf: running: autopoint --force
autopoint: *** The AM_GNU_GETTEXT_VERSION declaration in your configure.ac  
file requires the infrastructure from gettext-0.18 but this version
is older. Please upgrade to gettext-0.18 or newer.
autopoint: *** Stop.
autoreconf: autopoint failed with exit status: 1
```

Kein Problem, das lässt sich lösen mit toast[^toast1] [^toast2] lösen:
```
toast arm gettext
```
Jetzt könnt ihr euch einen Kaffee holen, das dauert ein wenig...

Nachdem toast durchgelaufen ist, wiederholen wir `autoreconf -fiv` 
und machen mit dem *Dreisatz*(s.o.) weiter. 

## Konfiguration von GoAccess

### ~/etc/goaccess/goaccess.conf

Die Config von GoAccess liegt durch die `--prefix=$HOME` Option von *configure*
unter `etc/goaccess/goaccess.conf` in deinem Home-Verezeichnis.

```
vi ~/etc/goaccess/goaccess.conf
```

Es gibt nur eine Einstellung, die für GoAccess wirklich zwingend ist 
und zwar die des Aufbaus des *Access-Logs*[^logs]
```
log-format COMBINED
```

Dann möchten wir noch, dass uns GoAccess, die Suchbegriff, mit denen Besucher 
über Google und Co auf unsere Seiten kommen auswertet.

Dies ist via Default mit `ignore-panel KEYPHRASES` dektiviert, 
wir suchen die Stelle und kommentieren die Zeile mit einer `#` am Zeilenanfang aus:
```
#ignore-panel KEYPHRASES
```

gleiches wiederholen wir für die Referrer.
```
#ignore-panel REFERRERS
```

### Anpassung der Variablen MANPATH

Damit der Aufruf von `man goaccess` auch die dazugehörige Manpage und nicht

> Keine Handbuchseite für goaccess 

anzeigt wird, müssen wir die Umgebungsvariable *MANPATH* anpassen.

Dazu fügen wir in *.bash_profile* die folgende Zeile ein:
```
export MANPATH="$MANPATH:$HOME/share/man/"
```

## Nutzung von GoAccess

### Beispiele

Einfache Ausführung mit Config und *Standard-Logfile*:
```
goaccess -p ~/etc/goaccess/goaccess.conf ~/logs/access_log 
```

Hier ein paar Beispiele, die auf ganz praktisch fand:

Wir wollen uns nur die Logs von einem bestimmtem Tag anzeigen lassen, z.B. den 22. April 2019 
und *pipen* die Ausgabe von `grep` nach GoAccess:
```
grep '^.*-\ - \[22/Apr/2019' ~/logs/access_log | goaccess  -p ~/etc/goaccess/goaccess.conf
```

Die via *Gzip* komprierten Logs von ca. vier Wochen via `zcat` an GoAccess durchreichen,
diesmal ohne Config stattdessen mit Log-Fomat via Option:
```
zcat ~/logs/access_log.*.gz | goaccess --log-format COMBINED 
```

Ausgabe in eine Datei via `-o` Option, hier der Export in eine Webseite, entscheidend ist der Suffix der Datei.
```
goaccess -o export.html -a -d -p ~/etc/goaccess/goaccess.conf ~/logs/access_log 
```
Durch das Argument hinter `-o`, sind auch noch Exporte via Dateiendung `.csv` und `.json`
in die entsprechenden Formate möglich.

### Hotkeys

Hier noch ein paar gebräuchliche Hotkeys für die Bedienung der von GoAccess auf der Konsole:

* `TAB`, die Panels anwählen (nach unten)
* `SHIFT` + `TAB`, die Panels anwählen (nach oben)
* `ENTER`, das angwählte Panel öffen
* `1-9`, wählt das Panel mit der Nummer direkt an, z.B. `4` für die *404er HTTP Status Codes*
* `j`, in Panel nach unten scrollen
* `k`, in Panel nach oben scrollen
* `h`, öffnet die Hilfe
* `q`, schließt das aktive Element, z.B. Hilfe, Panel oder letztendlich GoAceccess selbst

Noch mehr Beispiele findest du via `goaccess --help` oder in der Manpage[^man]. 

* * *
[^ncurses]: [Ncurses](https://de.wikipedia.org/wiki/Ncurses)
[^ureact]: [https://twitter.com/ubernauten/status/1124018556922888196](https://twitter.com/ubernauten/status/1124018556922888196)
[^toast1]: [toast - packageless package manager for Unix systems and non-root users](https://wiki.uberspace.de/system:toast) 
[^toast2]: [toast homepage]([http://www.toastball.net/toast/)
[^logs]: [Webserver Logs, access_log](https://wiki.uberspace.de/webserver:logs#access_log)
[^man]: [GoAccess Manual Page](https://goaccess.io/man)
*[FLOSS]: Free/Libre Open Source Software

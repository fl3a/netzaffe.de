---
tags:
- Debian
- Security
- Repositories
- howto
- Git
- Drupal
layout: post
permalink: /git-gitosis-gitweb-the-debian-way.html
image: /assets/imgs/1024px-Git-logo-2007.svg.png
toc: true
nid: 978
title: Git, Gitosis, Gitweb (the Debian way)
---
<figure role="group">
  <img src="/assets/imgs/1024px-Git-logo-2007.svg.png" alt="git logo" />
  <figcaption>Git-Logo, Git, CC BY 3.0</figcaption>
</figure>

Installation und Konfiguration von Git, Gitosis und Gitweb unter Debian 5 (Lenny).

  - [Git](http://git-scm.com/) ist ein DVCS, welches 2005 von Linus
    Thorvalds  
    als Alternative zum vorher genutzten proprietären BitKeeper für die
    Quellcode-Verwaltung des Linux-Kernels entwickelt wurde.
  - [Gitosis](http://eagain.net/gitweb/?p=gitosis.git) ist eine Software
    um Git-Repositories einfach und sicher zu hosten.  
    Die Authentifizierung an gitosis erfolgt über SSH-Schlüssel.
  - [Gitweb](http://git.wiki.kernel.org/index.php/Gitweb) ist eine
    schnelle und skalierbare Weboberfläche für Git.

Das folgende Setup erstreckt sich über 3 Rechner:

1.  *birgit*, das zentrale Repository welches über gitosis verwaltet
    wird und die Gitweb Weboberfläche bereitstellt
2.  *nora*, der Server auf dem entwickelt wird
3.  *demine*, eine lokale Workstation

Warum man seinen Code versionieren sollte, müsste eigentlich jedem
Entwickler klar sein, [dass Drupal in Zukunft auf Git setzen wird](http://groups.drupal.org/node/48818#comment-133893), dürfte wohl
der Anreiz für Drupalentwickler sein sich frühzeitig mit dem Thema Git zu auseinanderzusetzen.<!--break-->

**Hätte, würde, wäre** 

Hätte ich an der [Session von Daniel und Eugen über Git](http://drupaletics.de/sessions/git-versionskontrolle-die-spass-macht),
die meiner Meinung nach eine der besten Session auf dem [DrupalCamp Essen](http://drupaletics.de/) 
war einen Monat früher teilgenommen,  
hätte ich Gitoltite bei unserem jetzigen Projekt eingesetzt und dieses
Howto würde eben von Gitolite handeln...  

...wäre besser, da gitolite unter anderem Berechtigungen auf
Branch-Ebene vergeben kann...

## Installation und Einrichtung von Gitosis

Installation von git, gitosis und gitweb über aptitude als Benutzer
*root* auf *birgit*:

```
aptitude install git-core gitosis gitweb
```

Bei der Installation von *gitosis* wird unter Debian der Systembenutzer
*gitosis* mit */srv/gitosis* als Heimatverzeichnis angelegt.

Auf *nora* ein SSH-Schlüsselpaar für den Benutzer *florian* erstellen:

```
ssh-keygen -t rsa
```

Öffentlichen Schlüssel auf den Server *birgit*, der später als zentrales
Repository fungieren soll kopieren:

```
scp .ssh/id_rsa.pub birgit:/tmp
```

Auf *birgit* Gitosis mit dem eben kopiertem Public-Key initialisieren:

```
sudo -H -u gitosis gitosis-init < /tmp/id_rsa.pub
```

Dies erzeugt die folgende Ausgabe:

```
Initialized empty Git repository in
/srv/gitosis/repositories/gitosis-admin.git/  
Reinitialized existing Git repository in
/srv/gitosis/repositories/gitosis-admin.git/
```

Durch die Initialisierung sind in */srv/gitosis* die folgenden
Verzeichnisse entstanden:

1.  */srv/gitosis/repositories*, welches die von *gitosis* verwalteten
    Repositories beinhaltet, es enthält bereits *gitosis-admin.git*, das
    Repository, welches zur Verwaltung von *gitosis* selbst dient.
2.  */srv/gitosis/gitosis/*, welches die noch leere Datei
    *projects.list* enthält, die in den nächsten Schritten pro Zeile
    durch Leerzeichen getrennt Repository und Eigentümer enthalten wird.

Als Benutzer *florian* auf *nora* das Repository

```
git clone gitosis@birgit:gitosis-admin.git
```

Das durch das Klonen entstandene Verzeichnis *gitosis-admin/* hat den
folgenden Inhalt:

  - *gitosis.conf*, die zentrale Konfigurationsdatei für gitosis
  - Das Verzeichnis *keydir*, welches die öffentichen Schlüssel zur
    Authentifizierung an gitosis enthält.  
    Durch die Initialisierung von gitosis ist in *keydir* bereits der
    öffentiche Schlüssel
    *[florian@nora.pub](mailto:florian@nora.pub "florian@nora.pub")*
    vorhanden.

### SSH Port und GIT URLS

**Achtung!**

Falls auf dem Server, auf dem Gitosis und somit in unserm Fall auch SSH läuft
ein Non Default Port verwendet wird, also nicht Port 22,
so ändert sich die in den folgenden Schritten die Git-URL.

In unserem Fall wird

```
gitosis@birgit:${REPOSITORY}.git
```

zu

```
ssh://gitosis@lbirgit:${PORT}/${REPOSITORY}.git
```

Beispielhaft für das Repository gitosis-admin mit einem SSHD welcher auf Port 1337 lauscht:

```
ssh://gitosis@lbirgit:1337/gitosis-admin.git
```

Mehr zu **Git URLS** findet sich in der Manpage zu `git-clone`.

## Der Gruppe gitosis-admin einen neuen Benutzer hinzufügen

Damit der neue Benutzer, hier florian@demine später selbständig weitere Repositories anlegen kann
muss er Mitglied in der Gruppe *gitosis-admin* werden.

Auf nora als Benutzer florian, die Datei gitosis.conf im bereits geklonten gitosis-admin Resopitory bearbeiten, 
um in der members Direktive von `[group gitosis-admin]` den Benutzer `florian@demine` hinzufügen:

```
[group gitosis-admin]
writable = gitosis-admin
members = florian@nora florian@demine
```

Anschließend, ein Commit mit aussagekräftiger Commit-Message (`-m`)...

```
git commit -a -m 'Added "florian@demine" to group gitosis-admin.'
```

Output

```
Created commit 819f0f0: Added "florian@demine" to group gitosis-admin
 1 files changed, 1 insertions(+), 1 deletions(-)
```

...und ein push um den Commit auf den Server zu übertragen:

```
git push
```

Output:

```
Counting objects: 6, done.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 534 bytes, done.
Total 4 (delta 1), reused 0 (delta 0)
To gitosis@birgit:gitosis-admin.git
   b2240d3..819f0f0  master -> master
```


## SSH-Public-Key für neuen Benutzer hinzufügen

Zuerst muss wieder für den jew. Benutzer ein SSH-Key angelegt werden, falls noch kein Key da ist, damit sich der Benutzer über diesen Key am gitiosis Konto anmelden kann.

Als florian auf demine:

```
ssh-keygen -t rsa
```

Defaults übernehmen

Falls Windows Rechner als Clients verwendet werden sollen,
hilft **PuttyGen** von der [Putty Downloadseite](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) bei der Erstellung des SSH-Public-Keys.

Hier muss ggf. nach der öffentliche SSH-Schlüssel in ein für OpenSSH verständliches Format konvertiert werden.

```
ssh-keygen -i -f is_rsa.pub > id_rsa2.pub
```

Anschießend den Teil mit dem öffentlichen Schlüssel per nach /tmp/ auf nora kopieren und gleichzeitig nach Schema *user@host.pub* umbenennen:

```
scp ~/.ssh/id_rsa2.pub nora:/tmp/florian@demine.pub
```

Weiter im Kontext mit florian auf nora um florian@demine.pub in der Verzeichnis keydir zu kopieren:

**Achtung: Der Key muss die Dateiendung .pub haben!**

```
scp ~/.ssh/id_rsa2.pub nora:/tmp/florian@demine.pub
cp /tmp/florian\@demine.pub keydir/
```

Die Datei florian@demine.pub in das gitosis-admin Repository aufnehmen:

```
git add keydir/florian\@demine.pub
```

Und wieder ein commit...

```
git commit -m 'Added Key "florian@demine.pub"'
```

...und wieder ein push, damit die Änderungen auf birgit auch wirksam werden.

```
git push
```

## Neues Repository hinzufügen

## Neues Repository anlegen

## Konfiguraton von gitweb

### /etc/gitweb.conf
   
### Virtual Host für gitweb anlegen

### Leserechte für den Webserver-Prozess

## Git personalisieren
  
##  Weiterführendes zu Git



---
title: Jekyll Deployment auf Uberspace via post-receive Hook
tags: 
- Jekyll
- "#!/bin/bash"
- uberspace
- git
- snippet
layout: post
toc: true
permalink: /jekyll-deployment-auf-uberspace-via-post-receive-hook/
---
Deployment einer [Jekyll-Site](/tags/jekyll) auf [Uberspace](https://uberspace.de) via *Git Bare Repository*[^1] und *post-receive Hook*[^2].

Zeilstellung ist, dass ein `git push` auf das *uberspace Remote Repository*[^3] das weiter unten beschriebene Skript triggert,
welches aus unserem Jekyll Repository mit all seinen Änderungen eine Website generiert 
und dann der Welt auf unserem *Uberspace Webserver*[^4] verfügbar macht.


## Vorbereitungen auf uberspace

Wir starten nach erfolgreichem SSH-Login in unserem Home-Verzeichnis und legen einen Ordner für unsers Repos an,
```
mkdir repos
```

dann erstellen wir eine Ordner für unsere Repos,
```
cd repos
```

erstellen den Ordner für das Repo auf das wir später *pushen* wollen 
(ab hier solltet ihr das exemplarische *netzaffe.de* durch eure Domain ersetzen... ;-))
```
mkdir netzaffe.de.git
```

und wechseln hinein.
```
cd netzaffe.de.git
```

Jetzt initialisieren wir den Ordner als *Bare Repo*[^1],
```
git init --bare
```

wechseln in das Verzeichnis *hooks*.
```
cd hooks
```

Dann fügen das [Skript](https://gist.github.com/fl3a/032fadb155a75adac03c85cf204051f6) als *post-receive Hook*[^1] hinzu, 
hier passiert später die ganze Magie.<!--break-->

```
curl -O post-receive https://gist.githubusercontent.com/fl3a/032fadb155a75adac03c85cf204051f6/raw/b49e91fd1158faca3e73274fc5e84a2115d4863b/uberspace-jekyll.sh
```

Last but not least, muss das Skript noch ausführbar gemacht werden:
```
chmod +x post-receive
```

## Das post-receive Skript


## Vorbereitungen im lokalen Git-Repository

Das waren die Schrite auf deinem Uberspace, weiter gehts in deinen Repo:


Remote[^3]
```
git remote add uberspace fl3a@bellatrix.uberspace.de:repos/netzaffe.de.git
```

```
git push uberspace master
```

Dieses Howto bezieht sich auf Uberspace 6, für Anmerkungen, Ideen und Feedback (nicht nur zu Uberspace 7) würde ich mich freuen!

## Credits

Dieser Artikel basiert im wesentlichen auf [Jekyll Auf Uberspace Mit Git](https://www.wittberger.net/post/jekyll-auf-uberspace-mit-git/) 
und [Jekyll Auf Uberspace](https://lc3dyr.de/blog/2012/07/22/Jekyll-auf-Uberspace/). Danke!

Der Artikel ist eine Essenz, die sich nur auf das Deployment bezieht. 
Zudem ist er aktualisiert (seit 2012, 2013 hat sich einiges in Jekyll und auf Uberspace etc getan) 
und das Skript hat noch etwas Liebe erfahren. 

===

[^1]: [Git auf einen Server bekommen](https://git-scm.com/book/de/v1/Git-auf-dem-Server-Git-auf-einen-Server-bekommen), [What is a bare git repository?](http://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/)

[^2]: [What are Git hooks?](https://githooks.com/), [Git individuell einrichten - Git Hooks](https://git-scm.com/book/de/v1/Git-individuell-einrichten-Git-Hooks) 

[^3]: [Git Grundlagen - Mit externen Repositorys arbeiten](https://git-scm.com/book/de/v1/Git-Grundlagen-Mit-externen-Repositorys-arbeite), [man git-remote](https://git-scm.com/docs/git-remote)

[^4]: [Uberspace Wiki: Webserver](https://wiki.uberspace.de/webserver)


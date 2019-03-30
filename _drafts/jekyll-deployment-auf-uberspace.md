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
permalink: /jekyll-deployment-auf-uberspace-via-bare-repo-und-post-receive-hook/
---
Deployment einer [Jekyll-Site](/tags/jekyll) auf [Uberspace](https://uberspace.de) via *Git Bare Repository*[^2] und *post-receive Hook*[^1].

Zeilstellung ist, dass ein `git push` auf das *uberspace Remote Repository*[^3] das weiter unten beschriebene Skript triggert,
welches aus unserem Jekyll Repository mit all seinen Änderungen eine Website generiert 
und dann der Welt auf unserem *Uberspace Webserver*[^4] verfügbar macht.


## Vorbereitungen auf uberspace

Wir starten nach erfolgreichem SSH-Login in unserem Home-Verzeichnis und legen Ordner für unser Repos und tmp an,
```
mkdir -p repos/tmp
```

dann erstellen wir eine Ordner für unsere Repos,
```
cd repos
```

erstellen den Ordner für das Repo auf das wir später *pushen* wollen 
(Ab hier solltet ihr das exemplarische *netzaffe.de* durch eure Domain ersetzen.)
```
mkdir netzaffe.de.git
```

und wechseln hinein.
```
cd netzaffe.de.git
```

Jetzt initialisieren wir den Ordner als *Bare Repo*[^2],
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

[uberspace-jekyll-deployment.sh](https://gist.github.com/fl3a/032fadb155a75adac03c85cf204051f6) Gist.

```
#!/bin/bash
#
# Deployment of Jekyll-Sites on Uberspace 
# via Git Bare Repository and post-receive Hook
#
# See https://netzaffe.de/jekyll-deployment-auf-uberspace-via-bare-repo-und-post-receive-hook/ 
# for requirement and more detailed description (german)

read oldrev newrev ref
pushed_branch=${ref#refs/heads/}

## Variables

build_branch='master'
site='netzaffe.de'
site_prefix='sandbox.'

git_repo=${HOME}/repos/${site}.git 
tmp=${HOME}/repos/tmp/${site}
www=/var/www/virtual/${USER}/${site_prefix}${site}

## Do the magic
 
[ $pushed_branch != $build_branch ] && exit
git clone ${git_repo} ${tmp}
cd ${tmp}
bundle install --path=~/.gem
JEKYLL_ENV=production jekyll build --source ${tmp} --destination ${www}
rm -rf ${tmp}
exit
```

### Anpassungen

Im Skript sind nur 3 Variablen anzupassen (sofern alles wie oben beschrieben umgesetzt wurde ;-D).


1. `build_branch`, **der** Branch der für das Deployment genutzt werden soll. 
 Andere Zweige werden ignoriert. Hier `master`.
2. `site` die Site bwz. die Domain. Hier `netzaffe.de`
3. `site_prefix`, Optionaler Prefix bzw. Subdomain, der der Variablen site vorangestellt wird. Hier `sandbox.`. 

### Beschreibung des Skipts 

Die anderen Variablen werden aus den oben angepassten und/oder Umgebungsvariablen[^5] zusammengesetzt.

* `git_repo`, Pfad, wo die Bare-Repo[^2] liegt, 
es fließt die Umgebungsvariable[^5] *HOME* und die Variable *site* mit ein.
* `tmp`, hier wird unser Bare-Repo[^2] temporär *hin-ge-clon-ed*, 
um als Quelle für die Generierung des statischen HTML für die Site zu dienen.
Es fließen die Umgebungsvariablei[^5] *HOME* und die Variable *site* mit ein.
* `www`, das Verzeichnis, das letztendlich vom Webserver ausgeliefert wird. 
Es fließen die Umgebungsvariable[^5] *USER* sowie *site_prefix* und *site* ein.

Das *Do the magic*

1. Überprüfung ob der übertragene- (pushed) und Build-Branch übereinstimmen, ansonsten Abruch.
2. Klonen des Bare-Repos[^2] nach *tmp*
2. Verzeichniswechsel nach *tmp*
3. Installation der im Gemfile spezifizierten Abhängigkeiten via `bundle install`
4. Generierung der HTML von *tmp* nach *www* via `jekyll build` 
5. Löschen von *tmp*
6. Beendigung des Skripts

## Vorbereitungen im lokalen Git-Repository

Das waren die Schrite auf deinem Uberspace, weiter gehts in deinen Repo.

Das oben erstellte Bare-Repository fügst du deinem Repo als sog. Remote-Repository[^3] Namens *uberspace* hinzu:
```
git remote add uberspace fl3a@bellatrix.uberspace.de:repos/netzaffe.de.git
```

Fertig, jetzt noch der push vom *master* nach *uberspace*.

```
git push uberspace master
```

Nach der Übertragung der Daten solltest du die Ausgaben von `bundle install` und `jekyll build` sehen.

Dieses Howto bezieht sich auf Uberspace 6, für Anmerkungen, Ideen und Feedback (nicht nur zu Uberspace 7) würde ich mich freuen!

## Credits

Dieser Artikel basiert im wesentlichen auf [Jekyll Auf Uberspace Mit Git](https://www.wittberger.net/post/jekyll-auf-uberspace-mit-git/) 
und [Jekyll Auf Uberspace](https://lc3dyr.de/blog/2012/07/22/Jekyll-auf-Uberspace/). Danke!

Der Artikel ist eine Essenz, die sich nur auf das Deployment bezieht. 
Zudem ist er aktualisiert (seit 2012, 2013 hat sich einiges in Jekyll und auf Uberspace etc getan) 
und das Skript hat noch etwas Liebe erfahren. 

---

[^1]: [Git auf einen Server bekommen](https://git-scm.com/book/de/v1/Git-auf-dem-Server-Git-auf-einen-Server-bekommen), [What is a bare git repository?](http://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/)

[^2]: [What are Git hooks?](https://githooks.com/), [Git individuell einrichten - Git Hooks](https://git-scm.com/book/de/v1/Git-individuell-einrichten-Git-Hooks) 

[^3]: [Git Grundlagen - Mit externen Repositorys arbeiten](https://git-scm.com/book/de/v1/Git-Grundlagen-Mit-externen-Repositorys-arbeite), [man git-remote](https://git-scm.com/docs/git-remote)

[^4]: [Uberspace Wiki: Webserver](https://wiki.uberspace.de/webserver)

[^5]: [Linux/UNIX Umgebungsvariablen](https://linuxwiki.de/UmgebungsVariable)

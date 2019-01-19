---
tags:
- svn
- ssh
- Linux
- Gut zu wissen
nid: 1633
permalink: "/blog/2014/11/26/svn-ueber-ssh-unter-linux-username-bei-svn-checkout-angeben.html"
layout: post
title: 'svn+ssh unter Linux: Username bei svn checkout angeben'
created: 1416991937
---
Neues Projekt, Repo und Credentials bekommen, aber es hapert schon beim initialen Checkout des Projekts auf der Kommandozeile, das Argument der Option `--username` wird ignoriert, stattdessen wird meine Login-Name, also florian verwendet (natürlich funktioniert das kommunizierte Passwort in der Kombination nicht :D).

```
florian@x1:~$ svn co svn+ssh://example.com/opt/repos/project --username latzel
```

```
florian@example.com's password:
```
<!--break-->
Via [URI Schema](http://en.wikipedia.org/wiki/URI_scheme) mit dem kommunizierten Username gehts.
```
svn co svn+ssh://latzel@example.com/opt/repos/project
```

```
latzel@example.com's password: 
```

Da die Kommunikation von SVN über SSH läuft, kann natürlich auch vergleichbar mit <a href="/node/990">SSH Port und GIT URLS</a> ein abweichender Port in der URI angegeben werden, zudem kann die Datei `~/.ssh/config` genutzt werden.


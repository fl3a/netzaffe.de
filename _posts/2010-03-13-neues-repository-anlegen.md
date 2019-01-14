---
tags:
- Repositories
- Linux
- howto
- Git
- Debian
nid: 983
permalink: "/git-gitosis-gitweb-the-debian-way/neues-repository-anlegen.html"
layout: book
title: Neues Repository anlegen
created: 1268494808
---
Jetzt kann als <em>florian@demine</em> ein neues Repository, hier "hongomat" 
angelegt werden:

<code>
mkdir hongomat
cd hongomat
git init
vi foo
vi bar
git add foo bar
git commit -m 'Initial commit'
</code>

Mit <code>git init</code> wird das Repository initialisiert,
es ist ein initialer Commit nötig.

<code>
git remote add origin gitosis@birgit:hongomat.git
git push origin master:refs/heads/master
</code>

Bei dem <code>git remote add</code> Statement wird mit <code>birgit:hongomat.git</code> das Remote Repository bestimmt.

Siehe <a href="http://netzaffe.de/git-gitosis-gitweb-the-debian-way/installation-und-einrichtung-von-gitosis/ssh-port-und-git-urls.html">SSH Port und GIT URLS</a> bei Abweichung vom SSH-Standard-Port (22). 

Der <code>push</code> Befehl schiebt alles in unser zentrales Repository auf <em>brigit</em>.




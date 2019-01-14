---
tags:
- ssh
- Git
nid: 990
permalink: "/git-gitosis-gitweb-the-debian-way/installation-und-einrichtung-von-gitosis/ssh-port-und-git-urls.html"
layout: book
title: SSH Port und GIT URLS
created: 1271870055
---
<strong>Achtung!</strong>
Falls auf dem Server, auf dem Gitosis und somit in unserm Fall auch <acronym title="Secure SHell">SSH</acronym> läuft
ein Non Default Port verwendet wird, also nicht Port 22,
so ändert sich die in den folgenden Schritten die Git-URL.

In unserem Fall wird 
<code>
gitosis@birgit:${REPOSITORY}.git
</code>

zu 

<code>
ssh://gitosis@lbirgit:${PORT}/${REPOSITORY}.git
</code>



Beispielhaft für das Repository <em>gitosis-admin</em> mit einem <acronym title="Secure SHell Daemon">SSHD</acronym> welcher auf Port <em>1337</em> lauscht:
<code>
ssh://gitosis@lbirgit:1337/gitosis-admin.git
</code>


Mehr zu <strong>Git URLS</strong> findet sich in der Manpage zu <code>git-clone</code>.


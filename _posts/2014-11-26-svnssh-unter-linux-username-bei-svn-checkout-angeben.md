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
<p>Neues Projekt, Repo und Credentials bekommen, aber es hapert schon beim initialen Checkout des Projekts auf der Kommandozeile, das Argument der Option <code>--username</code> wird ignoriert, stattdessen wird meine Login-Name, also florian verwendet. (natürlich funktioniert das kommunizierte Passwort in der Kombination nicht :D)</p>
<p><code>florian@x1:~$ svn co svn+ssh://example.com/opt/repos/project --username latzel
florian@example.com's password: </code></p>
<p><!--break--></p>
<p>Via URI Schema<fn>http://en.wikipedia.org/wiki/URI_scheme</fn> mit dem kommunizierten Username gehts.</p>
<p><code>svn co svn+ssh://latzel@example.com/opt/repos/project
latzel@example.com's password: </code></p>
Da die Kommunikation von SVN über SSH läuft, kann natürlich auch vergleichbar mit <a href="/node/990">SSH Port und GIT URLS</a><fn>http://netzaffe.de/git-gitosis-gitweb-the-debian-way/installation-und-einrichtung-von-gitosis/ssh-port-und-git-urls.html</fn> ein abweichender Port in der URI angegeben werden, zudem kann die Datei <code>~/.ssh/config</code> genutzt werden.


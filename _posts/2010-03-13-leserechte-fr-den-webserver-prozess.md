---
tags:
- Debian
- apache2
- Git
- Linux
- howto
nid: 987
permalink: "/git-gitosis-gitweb-the-debian-way/konfiguraton-von-gitweb/leserechte-fuer-den-webserver-prozess.html"
layout: book
title: Leserechte für den Webserver-Prozess
created: 1268495316
---
Damit der Webserver auch die Repositories in Gitweb anzeigen kann, 
habe ich den Benutzer <em>gitosis</em> der Gruppe <em>www-data</em> hinzugefügt.


Als root:
<code>
usermod -g www-data gitosis
</code>

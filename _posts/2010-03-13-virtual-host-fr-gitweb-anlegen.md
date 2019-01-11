---
tags:
- VirtualHost
- Linux
- howto
- Git
- Debian
- apache2
nid: 986
permalink: "/git-gitosis-gitweb-the-debian-way/konfiguraton-von-gitweb/virtual-host-fuer-gitweb-anlegen.html"
layout: book
title: Virtual Host für gitweb anlegen
created: 1268495226
---
Auf <em>birgit</em>, die Datei <em>/etc/apache2/sites-available/birgit.example.com</em> mit dem folgendem Inhalt anlegen:

<code>
<VirtualHost *>
  ServerName birgit.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /srv/gitosis/repositories
  SetEnv GITWEB_CONFIG /etc/gitweb.conf
  Alias /gitweb.css /usr/share/gitweb/gitweb.css
  Alias /git-logo.png /usr/share/gitweb/git-logo.png
  Alias /git-favicon.png /usr/share/gitweb/git-favicon.png
  ScriptAlias /gitweb.cgi /usr/lib/cgi-bin/gitweb.cgi
  DirectoryIndex gitweb.cgi
</VirtualHost>
</code>

Da wir in einem verteiltem Team arbeiten und Gitweb aus dem Internet aufrufbar ist,

In unserem Fall ist dies eine Atrium Installation, in der jeder Entwickler ein Benutzerkonto besitzt. 

---
tags:
- snippet
- Security
- howto
- Drupal
- apache2
nid: 702
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration-von-apache/drupals-changelog-txt-absichern.html"
layout: book
title: Drupals CHANGELOG.txt absichern
created: 1232054859
---
<h2>Security by obscurity</h2>
<p>Mein erster Gedanke war, die <i>CHANGLOG.txt</i> mit in Direktive für die <a href="/node/689">Absicherung von Drupals <i>cron.php</i></a> zu nehmen um diese Datei ebenso vor fremden Blicken zu schützen...</p>
<!--break-->
<code>
<Files cron.php,CHANGELOG.txt>
Order deny,allow
Deny from all
# Zugriff aus dem VPN erlauben
Allow from 10.10.10.0/24
Allow from 127.0.0.1
Allow from 81.169.175.14
</Files>
</code>

<p>Aber nach überprüfen der Konfiguration mit</p>
<code>
sudo apache2ctl configtest
</code>

<p>kam der folgende Fehler:</p>

<code>
Syntax error on line 6 of /etc/apache2/conf.d/drupal.conf:
Multiple <Files> arguments not (yet) supported.
</code>

<p>Zu praktisch gedacht, doch ein eigenes Statement:</p>

<code>
<Files CHANGELOG.txt>
Order deny,allow
Deny from all
</Files>
</code>

<p>Nachdem der Configtest durchgelaufen ist muss der Webserver neu gestartet werden. </p>

<code>
/etc/init.d/apache2 restart
</code>

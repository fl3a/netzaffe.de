---
tags:
- Sicherheit
- Security
- howto
- Drupal
- cron
- apache2
nid: 689
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration-von-apache/drupals-cron-php-absichern.html"
layout: book
title: Drupals cron.php absichern
created: 1228589562
---
Um Drupals <i>cron.php</i> vor unberechtigtem Zugriff zu schützen, tragen wir in <i>/etc/apache2/conf.d/drupal.conf</i> noch die folgende Passage ein:
<br />
<code>
<Files cron.php>
Order deny,allow
Deny from all
Allow from 10.10.10.0/24
Allow from 127.0.0.1
Allow from 1.2.3.4
</Files>
</code>
<!--break-->
In der ersten Allow-Direktive wird per <acronym title="Classless Inter-Domain Routing">CIDR</acronym>-Notation der Zugriff vom kompletten <acronym title="Virtual Private Network">VPN</acronym> gewährt.<br />
In der zweiten wird der Zugriff von localhost aus erlaubt.<br />
Entscheidend ist aber, daß die IP-Adresse des Server(die 3.te Direktive) gelistet ist, von hier wird <i>cron.php</i> per Cronjob aufgerufen,<br /><br />
Damit unsere <i>/etc/apache2/conf.d/drupal.conf</i> wirksam wird, muß der Webserver auch hier die Konfiguration neu einlesen:
<br />
<code>
/etc/init.d/apache2 reload
</code>

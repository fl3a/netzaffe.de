---
tags:
- Drupal
- howto
- apache2
- snippet
- ".htaccess"
nid: 688
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration-von-apache/drupal-und-htaccess.html"
layout: book
title: Drupal und .htaccess
created: 1228589087
---
Damit die von Drupal benutzte .htaccess funktioniert legen wir die Datei <i>/etc/apache2/conf.d/drupal.conf</i> mit folgendem Inhalt an:
<code>
<Directory /home/foobar/drupal/>
Options +FollowSymLinks Indexes
AllowOverride All
order allow,deny
allow from all
</Directory>
</code>

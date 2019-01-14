---
tags:
- apache2
- VirtualHost
nid: 538
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration-von-apache/virtual-host-einrichten.html"
layout: book
title: Virtual Host einrichten
created: 1222813652
---
Anlegen der Datei <i>/etc/apache2/sites-available/example.com.localhost.conf</i>,<br /> auch hier ist <i>foobar</i> wieder durch den eigenen Benutzernamen zu ersetzten,  DocumentRoot zeigt auf den symbolischen Link, welcher wiederum auf die Wurzel der Drupal-Installation zeigt.
<code>
<VirtualHost *>
ServerName example.com.localhost
ServerAlias www.example.com.localhost
ServerAdmin foobar@example.com.localhost
DocumentRoot /home/foobar/drupal/6.x
ErrorLog /var/log/apache2/example.com.localhost-error.log
CustomLog /var/log/apache2/example.com.localhost-access.log combined
</VirtualHost>
</code>
Analog zur Aktivierung des rewrite-Moduls, werden auch hier wieder symbolische Links gesetzt und zwar von <i>/etc/apache2/sites-available</i> nach <i>/etc/apache2/sites-enabled</i>.
<code>
a2ensite example.com.localhost.conf
</code>
<p>Nach den letzten Schritten müssen wir den den <a href="http://netzaffe.de/2008/09/30/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration/neustart-von-apach">Webserver neu starten</a>, damit er seine Konfiguration erneut einließt und die angelegten Direktiven wirksam werden.</p>

---
tags:
- snippet
- Gut zu wissen
- Drupal
- apache2
nid: 1632
permalink: "/drupal-und-apache-2-4-x-unter-debian-testing-jessie"
layout: blog
title: Drupal und Apache 2.4.x unter Debian Testing/Jessie
created: 1413807662
---
Da es nicht mehr all zu lange dauert bis Debian 8 erscheint, bzw. bis Jessie den Status <em>stable</em> erreicht, haben wir bereits jetzt einige(in progress...) Drupal-Installationen auf eine Debian-Jessie-KVM migriert.

Von Debian 7 zu 8 hat sich nicht nur das Major-Release-Nummer von Debian erhöht, sondern auch der Webserver Apache hat einen Sprung gemacht, von Apache Version 2.2 auf 2.4.

Das bringt einige Implikationen mit sich...<!--break-->

<h2>Dateinamenerweiterung .conf</h2>
Apache 2.4 besteht jetzt auf die <strong>Dateiendung</strong> (englisch filename extension) <strong>.conf</strong>.

Ohne Dateiendung .conf verweigert <em>a2ensite</em> den Dienst und quittiert mit <code>
ERROR: Site example.com does not exist!</code>
und selbst bei einem selbst erstellten Symlink in <em>/etc/apache2/site-enabled</em> wird die Datei nicht geladen.

<code>
/etc/apache2/
|-- apache2.conf
|       `--  ports.conf
|-- mods-enabled
|       |-- *.load
|       `-- *.conf
|-- conf-enabled
|       `-- *.conf
|-- sites-enabled
|       `-- *.conf
</code>

<h2>Neue Direktiven in den Vhosts</h2>
in Apache v.2.4.x ist jetzt das neue Modul <em>mod_authz_core<fn>http://httpd.apache.org/docs/current/mod/mod_authz_core.html</fn> für die Autorisierung zuständig.  Das in v.2.2 <code>Allow from all</code>
ist equivalent zu <code>Require all granted</code>
in Apache v. 2.4.x. 

Ohne die Umstellung auf die neue Direktive bekommen wir <code>Forbidden. You don't have permission to access /</code>, das vorhandene <code>AllowOverride All</code> welche für die Auswertung von Drupals <code>.htaccess</code> und somit auch die sog. <em>Clean-URL's</em> zuständig ist brauchen wir natürlich weiterhin.
<code type="apache">
<VirtualHost *:80>
  ServerAdmin info@example.com
  DocumentRoot "/multi/drupal/example.com/drupal"
  ServerName example.com

  ErrorLog "${APACHE_LOG_DIR}/example.com-error.log"
  CustomLog "${APACHE_LOG_DIR}/example.com-access.log" combined

  <Directory /multi/drupal/example.com/drupal/>
          AllowOverride All
          Require all granted
  </Directory>
</VirtualHost>
</code>

Siehe auch <em>Upgrading to 2.4 from 2.2</em><fn>http://httpd.apache.org/docs/trunk/upgrading.html</fn>.



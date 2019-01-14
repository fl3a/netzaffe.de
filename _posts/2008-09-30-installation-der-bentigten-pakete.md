---
tags:
- PostgreSQL
- php
- Multisite
- howto
- Drupal
- Debian
- "<?php ?>"
- drush
nid: 521
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/installation-der-benoetigten-pakete.html"
layout: book
title: Installation der benötigten Pakete
created: 1222756735
---
<p>
Die folgenden Pakete werden ben&#246;tigt:
</p>

<ul>
<li>apache2 - Der Apache Webserver in der Version 2</li>
<li>libapache2-mod-php5 - Das Apache-Modul f&#252;r PHP5</li>
<li>php5 und php5-common - Den PHP-Interpreter</li>
<li>php5-gd - Die GD Grafikbibliothek f&#252;r PHP5</li>
<li>php5-pgsql - Das PHP-Modul f&#252;r den Zugriff auf die PostgreSQL Datenbank</li>
<li>php5-<acronym title="Command-Line Interpreter">cli</acronym> - PHP für die Kommandozeile, benötigt von <acronym title="Drupal Shell"><a href="/tags/drush.html">drush</a></acronym></li>
<li>postgresql-8.1 - Der PostgreSQL Datenbankserver</li>
<li>phppgadmin - Webbasiertes Administrationswerkzeug für PostgreSQL(ähnlich phpmyadmin für mysql)</li>
</ul>

Die eigentliche Installation:
<code>
aptitude install apache2 libapache2-mod-php5 php5 php5-common php5-pgsql php5-gd php5-cli postgresql-8.1 phppgadmin</code>

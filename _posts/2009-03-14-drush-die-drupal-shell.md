---
tags:
- php-cli
- Drupal
- "<?php ?>"
- "#!/bin/bash"
- drush
nid: 712
permalink: "/drush-die-drupal-shell.html"
layout: book
title: Drush - Die Drupal-Shell
created: 1237056900
---
<p><a href="http://drupal.org/project/drush" title="Drush Projektseite auf drupal.org">Drush</a> ist eine Schnittstelle für Drupal auf der Kommandozeile, praktisch wie Schweizer-Taschenmesser und gerade für jene, die sowieso mit der Shell arbeiten.</p>

Das Drush-Modul setzt sich aus den folgenden Untermodulen zusammen:
<ul>
  <li>drush_pm - Der Paket-Manager, ähnlich apt bzw. aptitude</li>
  <li>drush_simpletest - Um Simpletest von der  Kommandozeile auszuführen(benötigt <a href="http://drupal.org/project/simpletest">simpletest</a>)</li>
  <li>drush_sql - Ausführen von SQL-Kommandos </li>
  <li>drush_tools - Nützliches Werkzeuge für die Arbeit mit Drupal</li>
</ul>

<p>Für ein lauffähiges Drush sind ein bestehendes Drupal und die folgenden Pakete unter Debian oder Ubuntu nötig:</p>
<ul>
  <li>php5-cli - PHP-Interpreter für Kommandozeile </li>
  <li>wget oder curl - Für das Heruterladen von Dateien aus dem Internet </li>
</ul>
Optional:
<ul>
  <li>subversion - Für drush_pm</li>
  <li>cvs - Für drush_pm</li>
  <li>rsync - Für die Syncronisierung von Drupal-Installationen über ssh</li>
</ul>

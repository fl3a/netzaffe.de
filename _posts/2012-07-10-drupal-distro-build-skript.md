---
tags:
- snippet
- Installations Profile
- drush
- Drupal
- "#!/bin/bash"
nid: 1609
permalink: "/blog/2012/07/10/drupal-distro-build-skript.html"
layout: blog
title: Drupal-Distro-Build-Skript
created: 1341939334
---
Das Testen von Drupal-Installationsprofilen ist relativ mühselig, da sich ein Teil der Schritte, bis man überhaupt erst zum Testen der eigentlichen Funktionalität kommt,
mit dem Build-Prozess beschäftigt.

Diesen muß man eigentlich für jede Änderung erneut durchlaufen...
<ol class="decimal">
 <li>Drush make (das macht es im Falls des <a href="https://github.com/fl3a/fserver_profile">Feature-Server-Installations-Profiles</a>)
<ol class="decimal">
   <li>Drush make mit <em>distro.make</em> aus dem Git-Repository </li>
   <li>Download des Drupal-Cores</li>
   <li>Klonen des in <em>distro.make</em> hinterlegten Repositories für das Installationsprofil</li>
   <li>Rekursive Suche nach weiteren Drush-Makefiles,
   runterladen der Drupal-Module und des Themes, die im gefundenen Makefile <em>drupal-org.make</em> spezifiziert sind</li> 
  </ol>
  </li>
 
 <li>Sybolischer-Link vom erstellten Build auf die DocumentRoot des für Testzwecke angelegten VirtualHosts</li>
 <li>Drop auf alle Tabellen in der Zieldatenbank</li>
 <li>Installation von Drupal und einem bestimmtem Installationsprofiles, hier <em>fserver_profile</em></li>
</ol>
In der scheinbaren Routine des manuellen Durchlaufen dieser Schritte entsteht zudem auch mal schnell ein Fehler.

So habe ich beim gefühlt 100sten Mal des Durchlaufens dieser Prozedur versehentlich in der falschen Datenbank alle Tabellen <em>ge-dropt-t</em> und dachte mir, Automatisierung muss her, schreib ein Shellskript...
<!--break-->
<h2>Vorraussetzungen</h2>
Neben den <em><a href="http://drupal.org/requirements/">Standard-System-Vorrausetzungen</a></em> für Drupal, wird zusätzlich folgendes für das Bash-Skript benötigt:
<ul>
 <li><a href="http://git-scm.com/">git</a></li>
 <li><a href="http://drupal.org/project/drush">drush</a></li>
 <li><a href="http://drupal.org/project/drush_make">drush make</a><br />Falls Drush vor v.5 genutzt wird
</li>
 <li><a href="http://drupal.org/project/drush_site_install6">drush site-install 6.x</a><br />Falls Drush vor v.4  mit Drupal-6.x genutzt wird</li>
</ul>
Zur Ausführung sollte sich das Skript im Suchpfad <em>$PATH</em> befinden, kann aber natürlich auch mit einem vorangestellten <em>bash</em> gestartet werden.

<h2>Das Skript</h2>
Einfaches Bash-Skript welches die o.g. Schritte durchläuft.

Das <em>droppen</em> der Tabellen in der Zieldatenbank erfolgt über <em>drush site-install</em>.
[gist:3089178:drupal_distro_build.sh]

<h2>Konfiguration</h2>
Die vom Skript benötigten Variablen, befanden sich in einer früheren Version zwischen der Interpreterdeklaration und <em>set -o nounset</em>, diese habe ich ausgelagert um das Arbeiten mit verschiedenen Branches und Projekten einfacher zu gestalten.

Die Konfiguration wird dem Skript als Parmeter beim Aufruf übergeben
[gist:3089178:example.build.conf.sh]


<h2>Beispiele</h2>
<ol>
  <li>Einfacher Aufruf mit Ausgabe
    <code>
drupal_distro_build.sh fserver6_build.conf.sh
</code>
  </li>
  <li>
    Aufruf mit Mailversand der Ausgabe des Buildprozesses, der Betreff ist hier der Name des Builds<br />
    <code>
drupal_distro_build.sh fserver6_build.conf.sh |  mail -s `head -n 1`  mail@example.com</code>
  </li>
  <li>Aufruf mit Generierung eines Logfile, welches so heißt wie der Build + Suffix <em>.log</em>
  <code>
drupal_distro_build.sh fserver6_build.conf.sh | tee `head -n 1 `.log</code>

</ol>

<h2>Möglichkeiten</h2>
Mögliche Verwendung und Einsatzszenarien:
<ul>
 <li>In Git-Hooks</li>
 <li>In Continious Integration</li>
 <li>...und natürlich manuell</li>
</ul>

<h2>Quellen</h2>
Auf github, <a href="https://gist.github.com/3089178">Gist 3089178</a>

<code>
git clone git://gist.github.com/3089178.git drupal_distro_build
</code>

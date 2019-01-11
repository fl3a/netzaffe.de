---
tags:
- Multisite
- Linux
- Links
- howto
- Drupal
- "#!/bin/bash"
- drush
nid: 707
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/drush-in-einer-multisite-umgebung.html"
layout: book
title: Drush in einer Multisite-Umgebung
created: 1233851399
---
Um <acronym title="Drupal Shell">drush</acronym> in einer Multisiteumgebung zu arbeiten, haben sich folgende Mechanismen als nützlich erwiesen:
<!--break-->
<h2>Drush-Alias für Multisite</h2>
An dieser Stelle werden Aliase auf die jeweiligen drush-Version(Symlink) und der auf <i>-r</i> bzw. <i>--root</i> folgenden Wurzel der Drupal-Installation gesetzt.
<p>Alternativ zu Aliasen auf die Drupal-Wurzel, kann dies auch über 
<a href="/drush-die-drupal-shell/drushrc-php.html">drushrc.php, die Konfigurationsdatei für drush</a> erfolgen.</p>

<p>
Drush ist in nach <i>/usr/local/share/</i> installiert worden und das Wrapper-Skript <i>/usr/local/share/drush/drush</i> ist ein Softlink nach <i>/usr/local/bin/drush</i>. 
</p>

<code>
alias drush5_='/usr/local/bin/drush/drush -r /home/drupal/5.x '
alias drush6_='/usr/local/bin/drush/drush -r /home/drupal/6.x '
</code>

<h2>Verwendung von drush in der Multisiteumgebung</h2>
Der Aufruf von drush erfolgt über den angelegten Alias + die Spezifizierung der Subsite,<br />mittels <i>-l</i> oder <i>--uri=""</i>.
<p>
Im folgenden Beispiel werden die Informationen über den Status der Seite aktualisiert.
<p>

<code>
drush6_ -l http://example.com pm-refresh
</code>

Für 5.x ist das Modul <a href="http://drupal.org/project/update_status">Update Status</a> Voraussetzung für die Aktionen <i>pm-refresh (rf)</i> und <i>pm-update (up)</i>.

<h2>sites/all/modules & sites/example.com/modules</h2>
Wenn <i>sites/all/modules</i> und <i>sites/example.com/modules</i> parallel existieren, installiert drush Module nach <i>sites/all/modules<i>.
<p>Im Falle, das <i>sites/all/modules<i>  nicht existiert, dafür aber <i>sites/example.com/modules</i> wird <i>sites/all/modules<i> erstellt und benutzt.
</p>
Um trotzdem <i>sites/example.com/modules</i> verwenden zu können existiert in <i>sites/all</i> kein <i>modules</i> Verzeichnis und <i>sites/all</i> ist schreibgeschütz.

---
tags:
- Multisite
- Linux
- howto
- drush
- Drupal
nid: 592
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung/mulisiteumgebung-vorbereiten.html"
layout: book
title: Mulisiteumgebung vorbereiten
created: 1223472111
---
Erstellung des symbolische Links auf die Wurzel der Drupal-Installation, welche später in unserem VirtualHost die DokumentRoot darstellt .
<code>
ln -s drupal-6.4-DE 6.x
</code>


Erstellung der Verzeichnisse <i>6.x_sites</i>, welche später unser die Subsites, Module, und Themes enthalten wird und <i>6.x_backup</i>, in welchem Sicherheitskopien von Modulen und Themes, welche durch <acronym title="Drupal Shell">drush</acronym> aktualisiert worden sind abgelegt werden.
<code>
mkdir 	6.x_sites 6.x_backups
</code>


Verschieben der Ordner <i>drupal-6.4-DE/sites/all</i> und <i>drupal-6.4-DE/sites/default</i> nach <i>6.x_sites</i>.		
<code>
mv drupal-6.4-DE/sites/* 6.x_sites
</code>


Ersetzen des Verzeichnisses <i>sites</i> unterhalb von <i>drupal-6.4-DE</i> durch einen symbolischen Link mit <strong>relativer Pfadangabe</strong> welcher auf <i>6.x_sites</i> zeigt uns setzen des symbolischen Links für <i>backup</i>.
<code>
rmdir drupal-6.4-DE/sites
cd drupal-6.4-DE
ln -s ../6.x_sites sites
ln -s ../6.x_backup backup
cd ..
</code>


Erstellung der Verzeichnisse <i>modules</i> und <i>themes</i>, hier sollten seit Drupal 5.x angepasste und runtergeladene Module und Themes abgelegt werden. Diese sind somit auch für die Subsites verfügbar.(Siehe auch <i>README.txt</i> in <i>sites/</i>)
<code>
mkdir 6.x_sites/all/modules 6.x_sites/all/themes
</code>

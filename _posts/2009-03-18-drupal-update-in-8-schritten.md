---
tags:
- Drupal
- Open Source
- Linux
- Multisite
nid: 717
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/drupal-update-in-8-schritten.html"
layout: book
title: Drupal Update in 8 Schritten
created: 1237384334
---
<p>Bei einem <a href="/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung.html">Drupal Setup</a> wie <a href="/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung.html">hier</a> beschrieben, sind nur 8 Schritte für ein Update innerhalb eines Drupal-Zweiges nötig.
</p>
<p>Hier wird exemplarisch das Update von Drupal-6.9 auf Drupal-6.10, welches am 27. Februar durchgeführt wurde beschrieben.</p>
<p>
Es wird empfohlen die zu aktualisierende Seite in den  Wartungsarbeiten-Modus zu versetzen und die Dateien sowie Datenbank im Vorfeld sichern.</p><!--break-->

<h2>1) Runterloaden der neuen Drupal-Version</h2>
Download der neuen Drupal-Version in das Verzeichnis in dem sich die auch die alte Drupal-Version befindet.

<code>
wget http://ftp.osuosl.org/pub/drupal/files/projects/drupal-6.10.tar.gz
</code>

<h2>2) Entpacken des Drupal-Tarballs</h2>
<code>
tar xfz drupal-6.10.tar.gz
</code>

<h2>3) sites Ordner löschen</h2>
<code>
cd drupal-6.10
rm -r sites
</code>

<h2>4) Symlink auf 6.x_sites Ordner mit relativem Pfad</h2>
<code>
ln -s ../6.x_sites sites
</code>

<code>
ls -l
lrwxrwxrwx  1 florian server    12 2009-02-27 10:13 sites -> ../6.x_sites
..
</code>

<h2>5) Symlink auf 6.x_backups Ordner mit relativem Pfad</h2>
<code>
ln -s ../6.x_backup backups
</code>

<code>
ls -l
...
lrwxrwxrwx  1 florian server    13 2009-02-27 10:19 backups -> ../6.x_backup
...
</code>

<h2>6) Symlink auf alte Drupal-Version entfernen</h2>
<code>
cd ..
unlink 6.x
</code>

<h2>7) Symlink auf die neue Drupal-Version</h2>
<code>
ln -s drupal-6.10 6.x
</code>

<code>
ls -l
...
lrwxrwxrwx 1 florian server      11 2009-02-27 10:22 6.x -> drupal-6.10
...
</code>

<h2>8) update.php als User 1 aufrufen</h2>
Falls aktiviert, den Maintanance-Modus abschalten und Voila!

---
tags:
- Multisite
- howto
- drush
- Drupal
nid: 596
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung.html"
layout: book
title: Die Drupal Multisite-Umgebung
created: 1223727684
---
So soll die Multisiteumgebung später mal aussehen:
<code>
drupal/
|-- 6.x -> drupal-6.14
|-- 6.x_backup
|-- 6.x_profiles
|-- 6.x_sites
|   |-- all   
|   |-- default
|   |-- example.com
|   |   |-- files
|   |   |-- modules
|   |   `-- themes
|   `-- sub.example.com 
|       |-- files
|       |-- modules
|       `-- themes 
`-- drupal-6.14
    |-- includes
    |-- misc
    |-- modules
    |-- profiles -> ../6.x_profiles
    |-- scripts
    `-- sites  -> ../6.x_sites
</code>
<h2>Anmerkungen</h2>
<strike>Der Ordner <strong>6.x_backup</strong> beziehungsweise der symbolische Link <strong>backup</strong> in der
Wurzel der Drupal-Installation ist <acronym title="Drupal Shell">drush</acronym>-spezifisch.</strike>
Seit <a href="http://drupalcode.org/project/drush.git/commit/16a4e2b3cf0420a7dce7d3ed79f6701bdd97e095">Commit 16a4e2b3cf0420a7dce7d3ed79f6701bdd97e095</a> auf Drush nicht mehr möglich:
</p>

<code>
Force to use a location for backups outside the drupal root.
</code>

<p>Der Ordner 6.x_sites  beziehungsweise der symbolische Link sites beinhaltet die einzelnen Sites und deren Daten.</p>
<p>Seit dem Fix von <a href="http://drupal.org/node/694708">Issue #694708</a> auf drush_multi, behandle ich <em>profiles</em> analog zu <em>sites</em>.</p>
<!--break-->

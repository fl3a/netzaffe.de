---
tags:
- snippet
- Multisite
- drush
- Drupal
- config
- "<?php ?>"
nid: 713
permalink: "/drush-die-drupal-shell/drushrc-php.html"
layout: book
title: drushrc.php
created: 1237057511
---
<h2>Die Konfigurationsdatei für drush</h2>
<p>Hier verwendet, <acronym title="Drupal Shell">drush</acronym> für Drupal 6.x.</p>

<code type="php" start="1">
<?php
$options['r'] = '/home/foobar/drupal/6.x';

$options['v'] = 1;

$options['skip-tables'] = array(
 'common' => array('accesslog', 'cache', 'cache_block', 'cache_filter', 'cache_form', 'cache_menu', 'cache_page', 'cache_update', 'history', 'search_dataset', 'search_index', 'search_total', 'sessions', 'watchdog'),
);

$options['handler'] = 'wget';
</code>
<!--break-->
<h2>Optionen in drushrc.php</h2> 
<h3>Drupal Root</h3>
<p>In Zeile 2 wird der Wurzel der Drupal-Installation gesetzt, diese ist, wie in <a href="/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung.html">Die Drupal Multisite-Umgebung</a> beschrieben, ein Symlink auf die aktuelle Version 6.x von Drupal.</p>
<h3>Verbose</h3>
<p>In Zeile 4 wird für ausführlichere Ausgaben der Verbose-Modus aktiviert</p>
<h3>Skip-Tables</h3>
<p>Im Array <i>$option['skip_tables']</i>, in Zeile 7 werden die Tabellen angegeben, welche bei <i>sql load</i> oder <i>sql dump</i>  ausgelassen werden sollen.<br />Im Gegensatz zur Datei <i>example.drushrc.php</i>, habe ich den Array um die Tabellen <i>cache_block</i>, <i>cache_form</i>, <i>cache_page</i> und <i>cache_update</i> erweitert.<br >Falls die Module Mollom und Rules installiert sind, kann der Array auch noch um <i>cache_mollom</i> und <i>cache_rules</i> erweitert werden.</p> 
<h3>Download-Methode</h3>
<p>In Zeile 8, wird <i>wget</i> als Download-Methode, für <acronym title="Drupal Shell Package Manager">drush_pm</acronym> gesetzt, welche für <i>pm install</i> oder <i>pm update</i> benutzt wird.</p>
<p>&nbsp;</p>
In dieser <i>drushrc.php</i> nicht verwendete Einstellungen.
<h3>Automatisierung</h3>
<p>Falls drush für automatisierte Aufgaben verwendet kann diese Option nützlich sein. Es werden alle Fragen, die normalerweise eine Interaktion erfordern mit <i>yes</i> beantwortet.</p>
<h3>Drupal-Site</h3>
<code type="php">
$options['y'] = 1;
</code>

<p>Falls eine Subsite(Multisite) spezifiziert werden soll, so kann dies so erreicht werden:</p>

<code type="php">
$options['l'] = 'http://example.com';
</code>
<p>&nbsp;</p>
<h2>Spezifierung der Konfigurationsdatei</h2>
Drush's Konfigurationsdatei kann, wie in <i>drush.php</i>, in der Funktion <i>drush_rc_load()</i> beschrieben über 5 Möglichkeiten angesprochen werden.<br />Dies kann über die Plazierung der drushrc.php im Dateisystem erfolgen
<ol>
  <li>In der Wurzel von Drupal</li> 
  <li>Im aktuellen Verzeichnis(CWD/PWD)</li> 
  <li>Im Heimatverzeichniss($HOME)</li> 
  <li>Im gleichen Verzeichniss wie drush.php </li> 
</ol>
oder durch:
<ol>
  <li value="5"><i>-c</i> bzw. <i>--config</i> gefolgt von der Konfigurationsdatei</li>
</ol> 
<p>Ich habe <i>drushrc.php</i> in <i>~/bin</i> plaziert, wo auch <i>drush.php</i> liegt.</p>
<strong>Achtung</strong>
<p>Falls sich dort drush's für unterschiedlich Drupal-Versionen befinden, sollte ggf. <i>drushrc.php</i> nach z.B. <i>drush6rc.php</i> umbenannt werden und mit Aliasen auf <i>drush</i> in Kombnination mit der dazugehörigen <i>drushrc.php</i> gearbeitet werden.</p>


<p>Siehe auch <a href="http://netzaffe.de/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/drush-in-einer-multisiteumgebung.html">Drush in einer Multisite-Umgebung</a>.</p>

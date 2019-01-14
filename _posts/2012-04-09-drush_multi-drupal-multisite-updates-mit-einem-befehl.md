---
tags:
- Multisite
- drush
- Drupal
nid: 1593
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/drush-multi-drupal-multisite-updates-mit-einem-befehl.html"
layout: book
title: 'drush_multi: Drupal Multisite Updates mit einem Befehl'
created: 1333969497
---
<p><a href="https://www.drupal.org/project/drush_multi">Drush Multi</a> ist eine Erweiterung für die <a href="/tags/drush.html">Drupal Shell aka drush</a>. Die eigentliche Kernkomponente, welche aus einem Shellskript hervorgegangen ist behandelt Drupal-Updates von Drupal-Multisite-Umgebungen.</p>
<h2>drush multi-drupalupdate</h2>
<p>Aktualisiert die Installation falls es (Minor-)Updates auf den Drupal-Core gibt.</p>
<p>Einfaches <em>multi-drupalupdate</em>...</p>
<p><code>drush -r /path/to/drupal multi-drupalupdate </code></p>
<p><em>multi-drupalupdate</em> mit ein paar zusätzlichen Optionen...</p>
<p><code>drush -r /path/to/drupal multi-drupalupdate --sql-dump --comment='Vor Aktualisierung auf Drupal 7.12' --updatedb </code></p>
<p>Führt ein <em>multi-drupalupdate</em> auf <em>/path/to/drupal</em> aus</p>
<ol>
	<li>Sichert die Datenbanken aller Sites, mit einem optionalem Kommentar im Dateinamen, über --sql-dump und --comment Option</li>
	<li>Versetzt alle Sites in den Wartungsmodus, über --updatedb Option</li>
	<li>Download des Drupal-Cores</li>
	<li>Ersetzung der Drupal-Verzeichnisse und Dateien durch symbolische Links, die in der aktuellen Installation gefunden wurden, wie z.B. sites, profiles, .htaccess, etc</li>
	<li>Umbiegen des symbolischen Links auf die neue Drupal-Root</li>
	<li>Ausführung von ggf. anstehenden Drupal-Datenbank-Updates</li>
	<li>Beenden des Wartungsmodus</li>
</ol>
<h2>Besonderheiten</h2>
<ul>
	<li>Die hier beschriebene <a href="/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/die-drupal-multisite-umgebung.html">Struktur der Drupal-Multisite-Umgebung</a> muss berücksichtigt werden und Drupal-Root muß ein symbolischer Link sein</li>
	<li><a href="http://is-loesungen.de/docu/drush_multi/group__symlinks.html">Automatische Erkennung und Beibehaltung von symbolischen Links</a> über relativen Pfad, analog zu <em>sites</em> und <em>profiles</em></li>
	<li>Drush Multi benötigt drush v. 4</li>
</ul>
<h2>Weitere Befehle in drush_multi</h2>
<p>Während der ArByte an dem eigentlichen Kernstück <em>multi-drupalupdate</em> sind noch andere Dinge entstanden...</p>
<dl>
	<dt>drush multi-status</dt>
	<dd>Ein erweiterter drush core Status</dd>
	<dt>drush multi-site</dt>
	<dd>Legt eine Site innerhalb der Multisite-Installation an</dd>
	<dt>drush multi-create</dt>
	<dd>Erzeugt eine Drupal-Multisite-Installation nach dem beschriebenem Schema, unterstützt zudem die Benutzung von <a href="http://drupal.org/project/drush_make">drush_make</a> makefiles</dd>
	<dt>drush multi-exec</dt>
	<dd><strike>Führt ein Kommando auf alle Site innerhalb einer Installation aus. (batch mode).</strike> Diese Funktionalität ist mittlerweile in Drush (<code>drush -r /path/to/drupal/ @sites COMMAND</code>), @see <a href="http://drupal.org/node/652778">#652778: Similar functionality is in drush core 3.x</a></dd>
	<dt>drush multi-sql-dump</dt>
	<dd>Ein erweiterter sql dump, welcher z.B. die Datenbank auch tabelleweise sichert, bzip2-Kompremierung ermöglicht (Recheninternsiver aber besser Kompremierung).</dd>
	<dt>drush multi-nagios</dt>
	<dd><strike>Zur Benutzung als Nagios/Icinga plugin um Drupal-Sites und Drupal-Installations zu überwachen</strike><br>
		Nach <a href="http://drupal.org/project/drush_nagios">drush_nagios </a> ausgelagert</dd>
</dl>
<h2>Dokumentation</h2>
<ul>
	<li>Jedes Kommando besitzt eine Hilfe, z.B. <code>drush help multi-drupalupdate</code></li>
	<li>zudem gibt es eine <a href="http://is-loesungen.de/docu/drush_multi/index.html" rel="nofollow">drush_multi Doxygen Dokumentation</a>..</li>
	<li><a href="http://de.slideshare.net/fl3a/ddd-drush-multi">Slides zu drush_multi</a> von den drupaldevDays 2010 in München.</li>
	<li><a href="http://de.slideshare.net/fl3a/drush-und-multisite-drushmulti?related=1">Slides zu "Drush und Multisite: drush_multi"</a>, DrupalCamp Vienna 2009</li>
</ul>

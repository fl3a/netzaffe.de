---
tags:
- workaround
- shortcut
- nützlich
- Firefox
- drush
- Drupal
nid: 708
permalink: "/blog/2009/02/20/drush-mm-adminrole-workaround-und-tabs-in-firefox.html"
layout: blog
title: Drush_mm-Adminrole Workaround und Tabs in Firefox
created: 1235154310
---
<strong>Drush_mm-Adminrole-Workaround</strong>
<p><a href="http://drupal.org/project/drush">Drush</a>, <a href="http://drupal.org/project/drush_mm">drush_mm</a> und <a href="http://drupal.org/project/adminrole">adminrole</a> sind wirklich nützliche Module, funktionieren aber leider <a href="http://drupal.org/node/376780">noch nicht</a> zusammen.</p>
<p>In <acronym title="Drupal Shell Module Manager">drush_mm</acronym> findet noch keine Überprüfung statt ob adminrole installiert bzw, aktiviert ist, die Funktion adminrole_update_perms() aus adminrole.module wird durch <code> drush mm install modul </code> nicht aufgerufen.</p>
<p>Und hier der Workaround: <code> drush mm install modul && drush eval "adminrole_update_perms();"</code> 
Klappt und ich weiss jetzt wofür das eval-Statement gut sein kann.</p>
<p><strong>Update 21.02.2009 02:38 Patches im Anhang</strong>
Ein kürzere, elegantere und zukunftsträchtigere Lösung, je ein Patch für drush_mm und adminrole von <a href="http://freeblogger.org/">dereine</a>, Danke! und meine Lösung, welche unabhängig von adminrole ist. <!--break--></p>
<strong>Tabs in Firefox</strong>
<p>Wie kann man in Firefox per Shortcut die Tabs wechseln?</p>
<p>So einfach, daß ich nicht darauf gekommen bin...</p>
<p><strong>Firefox und Tab = Strg + Tab</strong></p>
<p>Danke an den Kollegen-Shingo, der es mir verraten hat!</p>


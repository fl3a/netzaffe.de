---
tags:
- Debian
- Security
- Repositories
- howto
- Git
- Drupal
nid: 978
permalink: "/git-gitosis-gitweb-the-debian-way.html"
layout: book
title: Git, Gitosis, Gitweb (the Debian way)
created: 1268493988
---
<img src="http://netzaffe.de/sites/netzaffe.de/files/git-logo.png" align="left" vspace="5" hspace="20" alt="Git Logo" /><p>Installation und Konfiguration von Git, 
Gitosis 
und Gitweb unter Debian 5 (Lenny).</p>

<ul>
<li>
<a href="http://git-scm.com/">Git</a> ist ein <acronym title="Distributed Version Control System">DVCS</acronym>, welches 2005 von Linus Thorvalds 
als Alternative zum vorher genutzten proprietären BitKeeper für die Quellcode-Verwaltung des Linux-Kernels entwickelt wurde.
</li>
<li>
<a href="http://eagain.net/gitweb/?p=gitosis.git">Gitosis</a> ist eine Software um Git-Repositories einfach und sicher zu hosten.
Die Authentifizierung an gitosis erfolgt über <acronym title="Secure Shell">SSH</acronym>-Schlüssel.
</li>
<li>
<a href="http://git.wiki.kernel.org/index.php/Gitweb">Gitweb</a> ist eine schnelle und skalierbare Weboberfläche für Git.
</li>
</ul>

Das folgende Setup erstreckt sich über 3 Rechner: 
<ol>
  <li><em>birgit</em>, das zentrale Repository welches über gitosis verwaltet wird und die Gitweb Weboberfläche bereitstellt</li>
  <li><em>nora</em>, der Server auf dem entwickelt wird</li>
  <li><em>demine</em>, eine lokale Workstation</li>
</ol>


Warum man seinen Code versionieren sollte, müsste eigentlich jedem Entwickler klar sein, <a href="http://groups.drupal.org/node/48818#comment-133893">das Drupal in Zukunft auf Git setzen wird</a>, dürfte wohl der Anreiz für Drupalentwickler sein sich frühzeitig mit dem Thema Git zu auseinanderzusetzen.
<!--break-->
<strong>Hätte, würde, wäre</strong>
Hätte ich an der <a href="http://drupaletics.de/sessions/git-versionskontrolle-die-spass-macht">Session von Daniel und Eugen über Git</a>, die meiner Meinung nach eine der besten Session auf dem <a href="http://drupaletics.de/">DrupalCamp Essen</a> war einen Monat früher teilgenommen, 
hätte ich Gitoltite bei unserem jetzigen Projekt eingesetzt und dieses Howto würde eben von Gitolite handeln...
...wäre besser, da gitolite unter anderem Berechtigungen auf Branch-Ebene vergeben kann...

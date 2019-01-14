---
tags:
- howto
- gitosis
- Git
- Debian
nid: 979
permalink: "/git-gitosis-gitweb-the-debian-way/installation-und-einrichtung-von-gitosis.html"
layout: book
title: Installation und Einrichtung von Gitosis
created: 1268494264
---
Installation von git, gitosis und gitweb über aptitude als Benutzer <em>root</em> auf <em>birgit</em>:

<code>
aptitude install git-core gitosis gitweb 
</code>

Bei der Installation von <em>gitosis</em> wird unter Debian der Systembenutzer <em>gitosis</em> mit <em>/srv/gitosis</em> als Heimatverzeichnis angelegt.

Auf <em>nora</em> ein SSH-Schlüsselpaar für den Benutzer <em>florian</em> erstellen:

<code>
ssh-keygen -t rsa
</code>

Öffentlichen Schlüssel auf den Server <em>birgit</em>, der später als zentrales Repository fungieren soll kopieren:

<code>
scp .ssh/id_rsa.pub birgit:/tmp
</code>


Auf <em>birgit</em> Gitosis mit dem eben kopiertem Public-Key initialisieren:

<code>
sudo -H -u gitosis gitosis-init < /tmp/id_rsa.pub
</code>

Dies erzeugt die folgende Ausgabe:

<code>
Initialized empty Git repository in /srv/gitosis/repositories/gitosis-admin.git/
Reinitialized existing Git repository in /srv/gitosis/repositories/gitosis-admin.git/
</code>

Durch die Initialisierung sind in <em>/srv/gitosis</em> die folgenden Verzeichnisse entstanden:
<ol>
  <li><em>/srv/gitosis/repositories</em>, welches die von <em>gitosis</em> verwalteten Repositories beinhaltet, es enthält bereits <em>gitosis-admin.git</em>, das Repository, welches zur Verwaltung von <em>gitosis</em> selbst dient.</li> 
  <li><em>/srv/gitosis/gitosis/</em>, welches die noch leere Datei <em>projects.list</em> enthält, die in den nächsten Schritten pro Zeile durch Leerzeichen getrennt Repository und Eigentümer enthalten wird.</li>
</ol>


Als Benutzer <em>florian</em> auf <em>nora</em> das Repository <code>gitosis-admin</code> klonen:

<code>
git clone gitosis@birgit:gitosis-admin.git
</code>

Das durch das Klonen entstandene Verzeichnis <em>gitosis-admin/</em> hat den folgenden Inhalt:
<ul>
  <li><em>gitosis.conf</em>, die zentrale Konfigurationsdatei für gitosis</li>
  <li>Das Verzeichnis <em>keydir</em>, welches die öffentichen Schlüssel zur Authentifizierung an gitosis enthält. 
Durch die Initialisierung von gitosis ist in <em>keydir</em> bereits der öffentiche Schlüssel <em>florian@nora.pub</em> vorhanden.</li>
</ul>

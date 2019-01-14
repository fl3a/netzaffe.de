---
tags:
- Internet
- howto
- gpg
nid: 682
permalink: "/gnupg-micro-howto/arbeiten-mit-gnupg/arbeiten-mit-keyservern.html"
layout: book
title: Arbeiten mit Keyservern
created: 1227912493
---
<h2>Puclic-Key  auf Keyserver hochladen</h2>
Damit unser öffentlicher Schlüssel jedem zur Verfügung stehen kann, exportieren wir ihn auf den Schlüsselserver.
<br /><br />
<code>
gpg --send-key 269B69D1
</code>
<br /><br />
Bei dem Zusammenspiel von GnuPG und Schlüsselservern(keyserver) kann man den Keyserver spezifizieren, 
ohne explizite Angabe des Keyservers, wird der in der ~/.gnupg/options definierte Keyserver verwendet.
<br /><br />
<code>
gpg --keyserver subkeys.pgp.net --send-key 269B69D1
</code>
<br />
<br />
<h2>Schlüssel auf Keyserver suchen</h2>
Bei einer erfolgreichen Suchanfrage besteht die Möglichkeit, gefundenen Schlüssel interaktiv in den Schlüsselbund zu importieren.
<br />Suche auf dem Keyserver, z.B. nach Namen
<code>
gpg --search-keys 'Florian Latzel'
</code>
<br />
oder sie Suche nach einer EMail-Adresse
<br /><br />
<code>
gpg --search-keys f punkt latzel ät is-loesungen punkt de
</code>
<br />
<br />
<h2>Public-Key von Keyserver importieren</h2>
Um einen Public-Key, dessen Key-ID bekannt ist vom Keyserver herunterzuladen, wird die folgende Options verwendet.
<br /><br />
<code>
gpg --recv-keys 269B69D1
</code>

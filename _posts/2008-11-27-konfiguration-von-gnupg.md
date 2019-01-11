---
tags:
- howto
- gpg
- Debian
- Datenintegrität
nid: 678
permalink: "/gnupg-micro-howto/konfiguration/konfiguration-von-gnupg.html"
layout: book
title: Konfiguration von GnuPG
created: 1227820460
---
<h2>~/.gnupg/options</h2>
Unter Debian und Ubuntu heißt die zuständige Konfigurationsdatei options, diese befindet in unserem Heimatverzeichnis im Verzeichnis .gnupg.
<p>
Bei default-key wird die Schlüssel-ID unseres Hauptschlüssels angegeben,
die Direktive keyserver ist für die Interaktion mit den Keyservern im Internet zuständig.
</p>
<code>
default-key 269B69D1
keyserver hkp://wwwkeys.eu.pgp.net
require-cross-certification
charset utf-8
use-agent
</code>
<h2>~/.gnupg/gpg.conf</h2>
Unter opensuse 11 heißt das Pedant zu ~/.gnupg/options gpg.conf, die Inhalte sind gleich.

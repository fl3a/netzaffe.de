---
tags:
- Verschlüsselung
- Open Source
- howto
- gpg
- Datenintegrität
nid: 675
permalink: "/gnupg-micro-howto/arbeiten-mit-gnupg/arbeiten-mit-private-keys.html"
layout: book
title: Arbeiten mit Private-Keys
created: 1227815895
---
<h2>Sichern der Private-Keys</h2>
Für eine Sicherheitskopie oder das Arbeiten auf mehreren Maschinen exportieren wir den Geheimen Schlüssel (Private Key).
Dieser sollte auf einem externen Datenträger gespeichert und an einem sicheren Ort aufbewahrt werden.<br />
Um den den Schlüssel auf einen anderen Rechner zu transferieren sollte eine verschlüsselte Verbindung benutzt werden.
<br /><br />
<code>
gpg --export-secret-key 269B69D1 > 269B69D1-private.key
</code>

<h2>Private-Keys auflisten</h2>
Analog zur Auflistung der Public-Keys geht dies auch mit den Private-Keys, <br />
alternativ steht noch -K als Shortoption zur Verfügung.
<br /><br />
<code>
gpg --list-private-keys
</code>

<h2>Private-Key löschen</h2>
Um einen privaten Key zu löschen wird das folgende Kommando verwendet, der zu löschende Schlüssel muss durch Key-ID oder EMail angegeben werden.
<br /><br />
<code>
gpg --delete-private-keys 269B69D1
</code>

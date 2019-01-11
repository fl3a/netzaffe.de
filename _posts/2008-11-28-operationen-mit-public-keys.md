---
tags:
- howto
- gpg
- Datenintegrität
nid: 681
permalink: "/gnupg-micro-howto/arbeiten-mit-gnupg/operationen-mit-public-keys.html"
layout: book
title: Operationen mit Public-Keys
created: 1227911900
---
Operationen mit den Public-Keys
<h2>Public-Keys auflisten</h2>
Erzeugt eine Auflistung aller Public-Keys im Keyring.
<br /><br />
<code>
gpg --list-keys
</code>
<br />
Es erscheint unser frisch erzeugter Schlüssel
<br />
<br />
<h2>Fingerprint ausgeben</h2>
Analog zur Ausgabe wie mit --list-keys lässt zusätzlich noch der Fingerprint anzeigen.
<br /><br />
<code>
gpg --fingerprint 
</code>
<br />
Der Fingerprint besteht aus 10 4er Paaren(hexadezimal), die letzen 2 4er Paare sind gleichzeitig die Key-ID.<br />
Die Key-ID müssen wir uns für den nächsten Schritt merken.
<br />
<br />
<code>
B043 7BFD 2D37 E901 4F88 2463 7681 46CD 269B 69D1
</code>
<br />
<br />
<h2>Public-Keys in Datei exportieren</h2>
Den Public-Key in eine ASCII-Armored Datei exportieren, die Angabe des Schlüssels erfolgt über Key-ID oder die E-Mailadresse.
<br /><br />
<code>
gpg --export -a -o f-punkt-latzel-ät-loesungen-de.asc f punkt-latzel ät loesungen punkt de
</code>
<br />
<br />
<h2>Public-Key aus Datei importieren</h2>
Mit dem folgendem Befehl wird Keyring importiert.
<br /><br />
<code>
gpg --import <Datei>
</code>

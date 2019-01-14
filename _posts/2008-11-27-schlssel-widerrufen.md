---
tags:
- Verschlüsselung
- howto
- gpg
- Datenintegrität
nid: 674
permalink: "/gnupg-micro-howto/arbeiten-mit-gnupg/schluessel-widerrufen.html"
layout: book
title: Schlüssel widerrufen
created: 1227815330
---
<h2>Den Revoke-Key importieren</h2>
Um den Revoke-Key nutzen zu können, muß dieser in unseren Keyring importiert werden.
<br /><br />
<code>
gpg --import 269B69D1-revoke-key.asc
</code>
<br />
<h2>Schlüssel auf Server widerrufen</h2>
Wir senden unseren Keyring, in dem sich jetzt unser Revoke-Key befindet zum Keyserver, um ihn dort zu widerufen.<br />
Alternativ zur Key-ID kann auch der Fingerabdruck verwendet werden.
<br /><br />
<code>
gpg --send-keys 269B69D1
</code>

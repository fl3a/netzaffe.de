---
tags:
- Verschlüsselung
- howto
- gpg
- Datenintegrität
nid: 680
permalink: "/gnupg-micro-howto/die-schluesselerstellung/einen-revoke-key-erstellen.html"
layout: book
title: Einen Revoke-Key erstellen
created: 1227903636
---
Es gibt Falle, in dem du deinen Schlüssel auf den Keyservern widerrufen möchtest, wie z.B. eine mittlerweile unzureichenede Stärke des Schlüssels, Schlüssel oder Rechner sind korrumpiert worden.<br />
Einen Widerrufungsschlüssels solltest du unbedingt erstellen und sicher aufbewahren.
<h2>Erstellung des Revoke-Keys</h2>
Nutzer-ID kann EMail oder die Key-ID sein.
<br /><br />

<code>
gpg --gen-revoke 269B69D1 > 269B69D1-revoke-key.asc
</code>

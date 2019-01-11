---
tags:
- howto
- gpg
- Terminologie
nid: 687
permalink: "/gnupg-micro-howto/konzept-und-terminologie.html"
layout: book
title: Konzept und Terminologie
created: 1227958103
---
<p>GnuPG verwendet das sog.  Public-Key-Verschlüsselungsverfahren<fn>https://de.wikipedia.org/wiki/Public-Key-Verschl%C3%BCsselungsverfahren</fn>, dass heißt, das es 2 Arten von Schlüssel gibt, Öffentliche- (Public Keys)<fn>https://de.wikipedia.org/wiki/%C3%96ffentlicher_Schl%C3%BCssel</fn> und Private Schlüssel (private Keys)<fn>https://de.wikipedia.org/wiki/Geheimer_Schl%C3%BCssel</fn>. Jeder Schlüssel hat sein dazugehöriges Gegenstück, allgemein als Schlüsselpaar bezeichnet.</p>
<p>Der öffentlicher Schlüssel wird wird zum Verschlüsseln und zur Überprüfung von Signaturen genutzt und muss deinem Kommunikationspartner zur Verfügung stehen damit er diese Aktionen ausführen kann und wird i.d.R. über z.B. sog. Keyserver öffentlich verbreitet.</p>
<p>Der private Schlüssel wird hingegen zum Signieren und Entschlüsseln genutzt und sollte, wie der Name schon vermuten lässt eher nicht weitergegeben werden und ist i.d.R mit einem Passwort geschützt.</p>
<p>Die Schlüssel werden über Schlüsselbünde verwaltet, auch hier wieder die Unterscheidung: 
<ul>
<li>einen für die Öffentlichen, <code>~/.gnupg/pubring.gpg</code>, eigenen Keys und die deiner Kommunikationspartner</li>
<li>und den für die Privaten, <code>~/.gnupg/secring.gpg</code></li>
</ul>


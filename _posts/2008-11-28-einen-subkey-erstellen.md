---
tags:
- Verschlüsselung
- Open Source
- howto
- gpg
- Datenintegrität
nid: 679
permalink: "/gnupg-micro-howto/die-schluesselerstellung/einen-subkey-erstellen.html"
layout: book
title: Einen Subkey erstellen
created: 1227865791
---
<h2>Mehrere Email Adressen mit einem GPG-Key nutzen</h2>
Statt der Erstellung einer neuen ID je verwendeter Emailadresse,<br />
besteht die Möglichkeit Unterschlüssel(subkeys) zu erstellen, die sich dann im gleichen Schlüsselbund befinden und das selbe Passwort für den privaten Schlüssel verwenden.
<br />
Der Aufruf von gpg kann auch über die ID als Parameter vollzogen werden.
<code>
gpg --edit-key f punkt latzel ät is-loesungen punkt de
</code>

Wir befinden uns jetzt im interaktiven Modus von gnupg,
mit adduid initieren die Erstellung des Subkeys.
<code>
adduid
</code>

<h2>Realname</h2>
Wie bei der Erstellung des Schlüssel, wird bei dem Erzeugen einen Subkey nach einem Realname gefragt.
<br />
<code>
Real name: 
</code>

<code>
Florian Latzel
</code>
<h2>Emailadresse</h2>
Auch der Subkey wird wieder an eine EMail-Adresse gebunden.
<code>
Email address: 
</code>
<code>
floh ät netzaffe punkt de
</code>
<h2>Kommentar</h2>
Wenn gewollt, kann der Subkey auch wieder kommentiert werden.
<code>
Comment: gib dem Netzaffen Zucker!
</code>
<h2>Bestätigung</h2>
<code>
You selected this USER-ID:
    "Florian Latzel (gib dem Netzaffen Zucker!) <floh ät netzaffe punkt de>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
</code>

<code>
You need a passphrase to unlock the secret key for
user: "Florian Latzel <f punkt latzel ät is-loesungen punkt de>"
1024-bit DSA key, ID 269B69D1, created 2007-05-25
</code>
Wir bestätigen die korrekten Angaben mit
<code>
o
</code>
Es erscheint anschließend wieder der Prompt von gpg.
<code>
Command>
</code>
Wir speichern, hiernach ist die Erstellung des Subkeys abgeschlossen.
<code>
save
</code>

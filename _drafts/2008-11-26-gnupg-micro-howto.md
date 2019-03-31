---
date: 2008-11-26 07:43

toc: true
tags:
- Datenschutz 
- email 
- gpg 
- howto 
- Linux 
- Netzkultur 
- Sicherheit 
- Verschlüsselung 
layout: post
permalink: /gnupg-micro-howto
title: GnuPG (GPG) Micro Howto
---
<figure role="group">
  <img src="/assets/imgs/1280px-GnuPG.svg.png" alt="GnuPG Logo 1280x387" title="GnuPG Logo" />
  <figcaption>GnuPG Logo, Thomas Wittek, GnuPG Projekt, Gemeinfrei</figcaption>
</figure>
Installation, Konfiguration und Nutzung von GnuPG unter Linux, MacOSX und Windows auf der Kommandozeile.

Verwendet wurde Debian Etch
mit gpg 1.4.6
und pinentry 0.7.2.

Getestet wurden:

- Ubuntu 8.04 mit gpg 1.4.6 und pinentry 0.7.4
- openSuSE 11 mit gpg2 2.0.9-22.1 und pinentry 0.7.5-5.1
- Windows Vista mit gnupg-w32cli-1.4.9.exe

## Konzept und Terminologie

GnuPG verwendet das sog. Public-Key-Verschlüsselungsverfahren1, dass heißt, das es 2 Arten von Schlüssel gibt, Öffentliche- (Public Keys)2 und Private Schlüssel (private Keys)3. Jeder Schlüssel hat sein dazugehöriges Gegenstück, allgemein als Schlüsselpaar bezeichnet.

Der öffentlicher Schlüssel wird wird zum Verschlüsseln und zur Überprüfung von Signaturen genutzt und muss deinem Kommunikationspartner zur Verfügung stehen damit er diese Aktionen ausführen kann und wird i.d.R. über z.B. sog. Keyserver öffentlich verbreitet.

Der private Schlüssel wird hingegen zum Signieren und Entschlüsseln genutzt und sollte, wie der Name schon vermuten lässt eher nicht weitergegeben werden und ist i.d.R mit einem Passwort geschützt.

Die Schlüssel werden über Schlüsselbünde verwaltet, auch hier wieder die Unterscheidung:

    einen für die Öffentlichen, ~/.gnupg/pubring.gpg, eigenen Keys und die deiner Kommunikationspartner
    und den für die Privaten, ~/.gnupg/secring.gpg

    1. https://de.wikipedia.org/wiki/Public-Key-Verschl%C3%BCsselungsverfahren
    2. https://de.wikipedia.org/wiki/%C3%96ffentlicher_Schl%C3%BCssel
    3. https://de.wikipedia.org/wiki/Geheimer_Schl%C3%BCssel
<!--break-->

## Erstellung eines GnuPG Schlüsselpaares

Zur Erstellung eines GnuPG Schlüsselpaares ist der folgende Befehl ist unter der Benutzer-ID des Hauptbenutzers auszuführen. 
Andernfalls muss der Ort durch --homedir /home/foobar/.gnupg angeglichen werden.
```
gpg --gen-key
```

Verschüsselungsalgorithmus wählen
```
gpg (GnuPG) 1.4.6; Copyright (C) 2006 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.
Please select what kind of key you want:
   (1) DSA and Elgamal (default)
   (2) DSA (sign only)
   (5) RSA (sign only)
Your selection?
```

Wir entscheiden uns für die Voreinstellung DSA und Elgamal.
```
1
```
Stärke des Schlüssels

```
DSA keypair will have 1024 bits.
ELG-E keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)
```

Wir wählen die Voreinstellung und bestätigen diese.


Gültigkeitzeiraum des Schlüssels
Hier kann spezifiziert werden ob und wann der Schlüssel verfällt.
```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
```

Der Schlüssel soll vorerst 1 Jahr gültig sein.
```
1y
```

Es erscheint das Ablaufdatum des Schlüssels, ein Jahr in der Zukunft.
```
Key expires at Mo 23 Nov 2009 20:08:50 CET
Is this correct? (y/N)
```

Wir bestätigen die Angaben mit
```
y
```

Realname, Eingabe des vollen Namens, der dem Schlüssel zugeordnet werden soll.

```
Florian Latzel
```

Emailadresse, Angabe der Emailadresse, an die Schlüssel gebunden werden soll .
```
f punkt latzel ät is-loesungen punkt de
```

Kommentar, in diesem Schritt haben wir die Möglichkeit, unserem Schlüssel zu kommentieren
```
!Recht auf Datenintegrität!
```

Bestätigung, nach Angabe aller Daten werden diese nochmal ausgegeben, es besteht die Möglichkeit die einzelnen Werte zu korregieren.
```
You selected this USER-ID:
    "Florian Latzel (Individuelle System Lösungen) f punkt latzel ät is-loesungen punkt de"
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
```

Wir bestätigen unsere Angaben sofern diese korrekt sind mit
```
o
```

Passwort für den privaten Schlüssel.
Eingabe des Passworts und anschließende Wiederholung, das Passwort wird nicht am Bildschirm ausgegeben.

### Einen GPG-Revoke-Key erstellen

Es gibt Falle, in dem du deinen Schlüssel auf den Keyservern widerrufen möchtest, 
wie z.B. eine mittlerweile unzureichenede Stärke des Schlüssels, Schlüssel oder Rechner sind korrumpiert worden.

Einen GnuPG Widerrufungsschlüssels solltest du unbedingt erstellen und sicher aufbewahren.

Erstellung des GNUPG Revoke-Keys, die Nutzer-ID kann EMail oder die Key-ID sein.
Hier mit Key-ID `269B69D1`, der Revoke-Key wird in der Datei *269B69D1-revoke-key.asc*.
```
gpg --gen-revoke 269B69D1 > 269B69D1-revoke-key.asc
```

### Einen GPG-Subkey erstellen

Mehrere Email Adressen mit einem GPG-Key nutzen.

Statt der Erstellung einer neuen ID je verwendeter Emailadresse,
besteht die Möglichkeit Unterschlüssel(subkeys) zu erstellen, 
die sich dann im gleichen Schlüsselbund befinden und das selbe Passwort für den privaten Schlüssel verwenden.

Der Aufruf von gpg kann auch über die ID als Parameter vollzogen werden.
```
gpg --edit-key f punkt latzel ät is-loesungen punkt de
```

Wir befinden uns jetzt im interaktiven Modus von gnupg,
mit adduid initieren die Erstellung des Subkeys.
```
adduid
```
Realname, wie bei der Erstellung des Schlüssel, wird bei dem Erzeugen einen Subkey nach einem Realname gefragt.
```
Real name:
```
```
Florian Latzel
```

Emailadresse, auch der Subkey wird wieder an eine EMail-Adresse gebunden.
```
Email address:
```
```
floh ät netzaffe punkt de
```

Kommentar, wenn gewollt, kann der Subkey auch wieder kommentiert werden.
```
Comment: gib dem Netzaffen Zucker!
```

Bestätigung
```
You selected this USER-ID:
    "Florian Latzel (gib dem Netzaffen Zucker!) <floh ät netzaffe punkt de>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
You need a passphrase to unlock the secret key for
user: "Florian Latzel <f punkt latzel ät is-loesungen punkt de>"
1024-bit DSA key, ID 269B69D1, created 2007-05-25
```

Wir bestätigen die korrekten Angaben mit
```
o
```

Es erscheint anschließend wieder der Prompt von gpg.
```
Command>
```

Wir speichern, hiernach ist die Erstellung des Subkeys abgeschlossen.
```
save
```

## Konfiguration von GnuPG

Konfiguration von GnuPG in *~/.gnupg/options*.

Unter Debian und Ubuntu heißt die zuständige Konfigurationsdatei options, diese befindet in unserem Heimatverzeichnis im Verzeichnis .gnupg.

Bei default-key wird die Schlüssel-ID unseres Hauptschlüssels angegeben,
die Direktive keyserver ist für die Interaktion mit den Keyservern im Internet zuständig.
```
default-key 269B69D1
keyserver hkp://wwwkeys.eu.pgp.net
require-cross-certification
charset utf-8
use-agent
```

*~/.gnupg/gpg.conf*, unter opensuse 11 heißt das Pedant zu *~/.gnupg/options* unter Debian *gpg.conf*, die Inhalte sind gleich.

## Konfiguration des gpg-agents

```
pinentry-program /usr/bin/pinentry-qt
no-grab
default-cache-ttl 1800

debug-level basic
log-file socket:///home/florian/.gnupg/log-socket
```

...to be continued.

## Arbeiten mit GnuPG

Eine Kurzreferenz von GnuPG-Befehlen und -Optionen die öfter mal benutzt werden.

### Arbeiten mit Private-Keys

Sichern der Private-Keys. 

Für eine Sicherheitskopie oder das Arbeiten auf mehreren Maschinen exportieren wir den Geheimen Schlüssel (Private Key).
Dieser sollte auf einem externen Datenträger gespeichert und an einem sicheren Ort aufbewahrt werden.

Um den den Schlüssel auf einen anderen Rechner zu transferieren sollte eine verschlüsselte Verbindung benutzt werden.
```
gpg --export-secret-key 269B69D1 > 269B69D1-private.key
```

Private-Keys auflisten. Analog zur Auflistung der Public-Keys geht dies auch mit den Private-Keys,
alternativ steht noch -K als Shortoption zur Verfügung.
```
gpg --list-private-keys
```

Private-Key löschen. Um einen privaten Key zu löschen wird das folgende Kommando verwendet, 
der zu löschende Schlüssel muss durch Key-ID oder EMail angegeben werden.
```
gpg --delete-private-keys 269B69D1
```

### Arbeiten mit Public-Keys

Operationen mit den Public-Keys.

Public-Keys auflisten. Erzeugt eine Auflistung aller Public-Keys im Keyring.
```
gpg --list-keys
```

Es erscheint unser frisch erzeugter Schlüssel

Fingerprint ausgeben. Analog zur Ausgabe wie mit --list-keys lässt zusätzlich noch der Fingerprint anzeigen.
```
gpg --fingerprint
```

Der Fingerprint besteht aus 10 4er Paaren(hexadezimal), die letzen 2 4er Paare sind gleichzeitig die Key-ID.
Die Key-ID müssen wir uns für den nächsten Schritt merken.
```
B043 7BFD 2D37 E901 4F88 2463 7681 46CD 269B 69D1
```

Public-Keys in Datei exportieren. 

Den Public-Key in eine ASCII-Armored Datei exportieren, die Angabe des Schlüssels erfolgt über Key-ID oder die E-Mailadresse.
```
gpg --export -a -o f-punkt-latzel-ät-loesungen-de.asc f punkt-latzel ät loesungen punkt de
```

Public-Key aus Datei importieren. Mit dem folgendem Befehl wird Keyring importiert.
```
gpg --import <Datei>
```

### Arbeiten mit Keyservern

#### Public-Key auf Keyserver veröffentlichen

Damit unser öffentlicher Schlüssel jedem zur Verfügung stehen kann, exportieren wir ihn auf den Schlüsselserver.
```
gpg --send-key 269B69D1
```

Bei dem Zusammenspiel von GnuPG und Schlüsselservern(keyserver) kann man den Keyserver spezifizieren,
ohne explizite Angabe des Keyservers, wird der in der ~/.gnupg/options definierte Keyserver verwendet.
```
gpg --keyserver subkeys.pgp.net --send-key 269B69D1
```

#### Schlüssel auf Keyserver suchen

Bei einer erfolgreichen Suchanfrage besteht die Möglichkeit, gefundenen Schlüssel interaktiv in den Schlüsselbund zu importieren.

Suche auf dem Keyserver, z.B. nach Namen
```
gpg --search-keys 'Florian Latzel'
```

oder sie Suche nach einer EMail-Adresse
```
gpg --search-keys f punkt latzel ät is-loesungen punkt de
```

#### Public-Key von Keyserver importieren

Um einen Public-Key, dessen Key-ID bekannt ist vom Keyserver herunterzuladen, wird die folgende Options verwendet.
```
gpg --recv-keys 269B69D1
```

### Schlüssel widerrufen

Den Revoke-Key importieren.

Um den Revoke-Key nutzen zu können, muß dieser in unseren Keyring importiert werden.
```
gpg --import 269B69D1-revoke-key.asc
```

Schlüssel auf Server widerrufen. 

Wir senden unseren Keyring, in dem sich jetzt unser Revoke-Key befindet zum Keyserver, um ihn dort zu widerufen.
Alternativ zur Key-ID kann auch der Fingerabdruck verwendet werden.
```
gpg --send-keys 269B69D1
```

## Software für die GnuPG Nutzung

Diverse nützliche Software für die Nutzung von GnuPG unter Windows, 
Mac OS, die Integration in Mail-Clients, Datei Browser oder Ähnliches.

- Enigmail - GnuPG Integration für Mozilla Applikationen wie z.B. Thunderbird
- gpg4win - EMail-Sicherheit mit GnuPG für Windows, u.a. Outlook- oder Explorer Integration
- signing-party - Diverse nützliche OpenPGP für Tools< für Keysigning-Partys[^4]
- GPG Suite (GPG Tools) für die Nutzung Mac OS, wie z.B. Einbindung in Apple Mail

## Weiterführendes zu GnuPG & Fußnoten

- GNU Privacy Guard - Wikipedia
- Das GNU-Handbuch zum Schutze der Privatsphäre
- Deutsches GPG Mini Howto auf gnupg.org
- GPG Schlüsselverwaltung für apt-get(Secure APT)
- GnuPG in der Debian-Referenz
- GnuPG auf ubuntuusers.de

[^4]: [Keysigning-Party](https://de.wikipedia.org/wiki/Keysigning-Party)
- Das GnuPG Keysigning-Party HOWTO von V. Alex Brennen
- GPG und Vim
- GPG-Agent und SSH Keys nutzen
- PGP-Keyserver mit Webfrontend
- RFC2440: OpenPGP Message Format
- RFC2015: MIME Security With Pretty Good Privacy
- Die c't-Krypto-Kampagne
- [Einfach erklärt: E-Mail-Verschlüsselung mit PGP](https://www.heise.de/ct/artikel/Einfach-erklaert-E-Mail-Verschluesselung-mit-PGP-4006652.html)

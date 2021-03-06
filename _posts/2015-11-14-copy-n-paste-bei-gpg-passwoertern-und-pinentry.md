---
tags:
- Verschlüsselung
- gpg
nid: 1639
layout: post
title: Copy 'n' Paste bei GPG Passwörtern und Pinentry
created: 1447521112
---
Ihr kennt das vielleicht, für Dein Projekt-Team wird eine neue Verteiler-Email-Adresse angelegt, einhergehend wird damit auch ein neues GnuPG-Schlüsselpaar erstellt.

Natürlich erfolgt, erfolgt die Kommunikation verschlüsselt via GNUPG, also bekommt ihr seperat den öffentlichen, den privaten Schlüssel und die Passphrase für den privaten Schlüssel, die Charakteristika eines guten Passworts ist erfüllt und zudem noch sehr gut gemeint lang.
Tippen und mühselig und kann einige Anläufen dauern, und  Pinentry (QT4) kann leider kein Copy 'n' Paste...so geht es trotzdem ohne abtippen.
<!--break-->

Bearbeitet eure gpg-agent.conf...
```
vi ~/.gnupg/gpg-agent.conf
```

...und fügt die folgenden Zeilen hinzu, so wechselt ihr das Programm, welches Pinentry zuständig ist.

```
# Keyboard control
no-grab

# PIN entry program
pinentry-program /usr/bin/pinentry-curses
```

Abschiessen, neustarten um die Änderung an der Config des GPG-Agenten wirksam zu machen: 
```
killall gpg-agent
gpg-agent --daemon
```

Bearbeiten der gewünschten Schlüsselkennung, die Kennung findet ihr mit gpg --list-secret-keys raus:
```
gpg --edit-key C36EE292
```
Ändern der Passphrase
```
gpg> passwd
```

Anschließend wird man 1 x nach dem aktuellem Passwort gefragt, wenn dies erfolgreich war, 2 x nach dem neuem Passwort.
Anschließend wird der Vorgang gespeichert.
```
gpg> save
```

Jetzt noch einmal alles durchtreten und das euer frei gewähltes Passwort sollte greifen.

```
killall gpg-agent
gpg-agent --daemon
```

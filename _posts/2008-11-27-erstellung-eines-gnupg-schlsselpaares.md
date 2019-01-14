---
tags:
- Verschlüsselung
- gpg
- Datenschutz
nid: 672
permalink: "/gnupg-micro-howto/die-schluesselerstellung.html"
layout: book
title: Erstellung eines GnuPG Schlüsselpaares
created: 1227810772
---
<p>Zur Erstellung eines GnuPG Schlüsselpaares ist der folgende Befehl ist unter der Benutzer-ID des Hauptbenutzers auszuführen. (Andernfalls muss der Ort durch --homedir /home/foobar/.gnupg angeglichen werden). <code>
gpg --gen-key 
</code>
</p>
<h2>Verschüsselungsalgorithmus wählen</h2>
<code>
gpg (GnuPG) 1.4.6; Copyright (C) 2006 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.
Please select what kind of key you want:
   (1) DSA and Elgamal (default)
   (2) DSA (sign only)
   (5) RSA (sign only)
Your selection?
</code> 
Wir entscheiden uns für die Voreinstellung DSA und Elgamal. 
<code>
1
</code>
</p>
<h2>Stärke des Schlüssels</h2>
<p>
<code>
DSA keypair will have 1024 bits.
ELG-E keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)
</code> 
Wir wählen die Voreinstellung und bestätigen diese.</p>
<h2>Gültigkeitzeiraum des Schlüssels</h2>
<p>Hier kann spezifiziert werden ob und wann der Schlüssel verfällt. 
<code> 
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)</code> 
Der Schlüssel soll vorerst 1 Jahr gültig sein. 
<code> 1y </code> 
Es erscheint das Ablaufdatum des Schlüssels, ein Jahr in der Zukunft. 
<code> 
Key expires at Mo 23 Nov 2009 20:08:50 CET
Is this correct? (y/N)
</code> 
Wir bestätigen die Angaben mit 
<code> y </code></p>
<h2>Realname</h2>
<p>Eingabe des vollen Namens, der dem Schlüssel zugeordnet werden soll. 
<code> Florian Latzel </code>
</p>
<h2>Emailadresse</h2>
<p>Angabe der Emailadresse, an die Schlüssel gebunden werden soll . 
<code> f punkt latzel ät is-loesungen punkt de 
</code>
</p>
<h2>Kommentar</h2>
<p>In diesem Schritt haben wir die Möglichkeit, unserem Schlüssel zu kommentieren 
<code>!Recht auf Datenintegrität!
</code></p>
<h2>Bestätigung</h2>
<p>Nach Angabe aller Daten werden diese nochmal ausgegeben, es besteht die Möglichkeit die einzelnen Werte zu korregieren. 
<code> 
You selected this USER-ID:
   "Florian Latzel (Individuelle System Lösungen) f punkt latzel ät is-loesungen punkt de"
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?</code> 
Wir bestätigen unsere Angaben sofern diese korrekt sind mit 
<code> o </code></p>
<h2>Passwort für den privaten Schlüssel</h2>
<p>Eingabe des Passworts und anschließende Wiederholung, das Passwort wird nicht am Bildschirm ausgegeben.</p>

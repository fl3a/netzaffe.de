---
tags:
- ssh
- Linux
- howto
- Git
- Debian
nid: 981
permalink: "/git-gitosis-gitweb-the-debian-way/ssh-public-key-fuer-neuen-benutzer-hinzufuegen.html"
layout: book
title: SSH-Public-Key für neuen Benutzer hinzufügen
created: 1268494612
---
Zuerst muss wieder für den jew. Benutzer ein SSH-Key angelegt werden, falls noch kein Key da ist, damit sich der Benutzer über diesen Key am <em>gitiosis</em> Konto anmelden kann. 

Als florian auf <em>demine</em>:
<code>
ssh-keygen -t rsa
</code>
Defaults übernehmen

Falls Windows Rechner als Clients verwendet werden sollen,
hilft PuttyGen von der <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html">Putty Downloadseite</a> bei der Erstellung des SSH-Public-Keys.
Hier muss ggf. nach der öffentliche SSH-Schlüssel in ein für OpenSSH verständliches Format konvertiert werden.
<code>
ssh-keygen -i -f is_rsa.pub > id_rsa2.pub
</code>

Anschießend den Teil mit dem öffentlichen Schlüssel per nach /tmp/ auf nora kopieren und gleichzeitig nach Schema <b>user@host.pub</b> umbenennen:
<code>
scp ~/.ssh/id_rsa.pub nora:/tmp/florian@demine.pub
</code>


Weiter im Kontext mit <em>florian</em> auf <em>nora</em> um <em>florian@demine.pub</em> in der Verzeichnis <code>keydir</code> zu kopieren:
<strong>Achtung: Der Key muss die Dateiendung <code>.pub</code> haben!</strong>

<code>
cp /tmp/florian\@demine.pub keydir/
</code>

Die Datei <em>florian@demine.pub</em> in das <em>gitosis-admin</em> Repository aufnehmen:

<code>
git add keydir/florian\@demine.pub
</code>

Und wieder ein commit...
<code>
git commit -m 'Added Key "florian@demine.pub"'
</code>

...und wieder ein push, damit die Änderungen auf <em>birgit</em> auch wirksam werden.
<code>
git push
</code>

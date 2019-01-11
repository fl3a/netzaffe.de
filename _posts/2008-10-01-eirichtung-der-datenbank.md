---
tags:
- PostgreSQL
- Linux
- createdb
- createuser
- Datenbank
nid: 540
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/eirichtung-der-datenbank.html"
layout: book
title: Eirichtung der Datenbank
created: 1222868232
---
Damit der Benutzerwechsel funktioniert, machen wir uns zu root.
<code>
su
</code> 
Um die folgenden Befehle auszuführen starten wir eine Shell unter der Identität von postgres
<code>
su postgres
</code>
<br />
Anlegen des zukünftigen Datenbankbenutzer mit den Optionen:
-P oder --pwprompt für Passwortauthentifizierung<br />
-S oder --no-superuser, Default, deshalb optional<br />
-D oder --no-createdb<br />
-R oder --no-createrole, Benutzer darf keine Rollen anlegen<br />
-E oder --encrypted, Verschlüsselung der Passwörter in der Datenbank<br />
<code>
createuser -P -S  -D  -R  -E datenbankbenutzer
</code>
Anlegen der Datenbank mit UTF-8Kodierung,-E oder --encoding- für den durch -O oder --owner spezifizierten Benutzer.
<code>
createdb -E UNICODE -O datenbankbenutzer datenbankname
</code>
Anschließend
<code>
exit
</code>
um die Shell von postgres zu beenden,
<code>
exit
</code>
um auch die Rootshell wieder zu verlassen, damit wir die nächsten Schritte als normaler Benutzer auszuführen.

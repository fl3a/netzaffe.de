---
tags:
- Drupal
- Multisite
- Subsite
nid: 593
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/einrichtung-einer-site.html"
layout: book
title: Einrichtung einer Site
created: 1223541347
---
Um als wieder Benutzer weiterzumachen:
<code>
exit
</code>


Wechsel in das 6.x_sites Verzeichnis:
<code>
cd
cd drupal/6.x_sites/
</code>


Anlegen eines Verzeichnisses für die erste Site,
<code>
mkdir -p example.com.localhost/files
</code>


Das Verzeichnis <i>files</i> für den Webserver schreibbar machen:
<code>
chmod 775 example.com.localhost/files
</code>


An dieser Stelle explizit kein <i>su -</i> um auch in diesem Verzeichnis zu bleiben.
<code>
su
</code>


<code>
chgrp www-data example.com.localhost/files
exit
</code>


Gesetz dem Fall, daß example.com irgendwann in den Produktiveinsatz
geht, geben wir diesen bei der Installationsroutine von Drupal den zukünftigen Speicherort für unsere Dateien an(<i>sites/example.com/files</i>)
und setzen hierfür noch einen Symlink
<code>
ln -s example.com.localhost example.com
</code>


Für Module und Themes, die <strong>nur</strong> für unsere Subsite verfügbar sein sollen legen wir noch die folgenden 2 Verzeichnisse an:
<code>
mkdir example.com.localhost/themes example.com.localhost/modules
</code>


Jetzt brauchen wir noch die settings.php, welche die Einstellungen für unser Site enthalten wird. 
<code>
cp default/default.settings.php example.com.localhost/settings.php
</code>

Jetzt können wir mit unsere Browser unter example.com.localhost aufrufen und kommen zur Installationsroutine von Drupal.

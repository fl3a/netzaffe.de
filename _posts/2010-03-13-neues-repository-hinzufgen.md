---
tags:
- Repositories
- Linux
- howto
- Git
- Debian
nid: 982
permalink: "/git-gitosis-gitweb-the-debian-way/neues-repository-hinzufuegen.html"
layout: book
title: Neues Repository hinzufügen
created: 1268494718
---
Jetzt können wir mit unserem frischgebackenem Admin-User <em>florian@demine</em> neue Repositories anlegen.

Als <em>florian@demine</em> auf der lokalen Workstation:

gitosis-admin.git auschecken
<code>
git clone gitosis@birgit:gitosis-admin.git
</code>

Da sich <em>florian@demine</em> bis jetzt noch nicht verbunden hat, muss dem ersten Verbindungsversuch über SSH mit <code>yes</code> zugestimmt werden:

<code>
Initialized empty Git repository in /home/florian/gitosis-admin/.git/
The authenticity of host 'birgit (88.198.7.214)' can't be established.
RSA key fingerprint is b4:c0:e6:e9:7c:fa:6b:a4:b1:d0:d2:4c:b5:b7:11:d1.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'birgit,88.198.7.214' (RSA) to the list of known hosts.
</code>

Wechsel in das soeben geklonte Repository:
<code>
cd gitosis-admin/
</code>

Die folgende Sektion, hier examplarisch die Gruppe <em>developers</em>, die auf <em>hongomat</em> unter <code>writable</code> Schreibzugriff haben soll der Datei <em>gitosis.conf</em> hinzufügen:
<code>
[group developers]
writable = hongomat
members = florian@demine
</code>

...wieder ein commit:
<code>
git commit -a -m 'Added group "developers" with member "florian@demine" and write access to "hongomat"'
</code>


...und wieder ein push:
<code>
git push
</code>

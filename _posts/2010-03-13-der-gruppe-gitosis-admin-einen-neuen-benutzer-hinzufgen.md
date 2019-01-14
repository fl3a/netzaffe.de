---
tags:
- Linux
- howto
- Git
- Debian
nid: 980
permalink: "/git-gitosis-gitweb-the-debian-way/der-gruppe-gitosis-admin-einen-neuen-benutzer-hinzufuegen.html"
layout: book
title: Der Gruppe gitosis-admin einen neuen Benutzer hinzufügen
created: 1268494426
---
Damit der neue Benutzer, hier <em>florian@demine</em> später selbständig weitere Repositories anlegen kann 
muss er Mitglied in der Gruppe <em>gitosis-admin</em> werden.


Auf <em>nora</em> als Benutzer <em>florian</em>, die Datei <em>gitosis.conf</em> im bereits geklonten <em>gitosis-admin Resopitory</em> bearbeiten, um in der members Direktive von <code>[group gitosis-admin]</code> den Benutzer <em>florian@demine</em> hizufügen:


<code>
[group gitosis-admin]
writable = gitosis-admin
members = florian@nora florian@demine
</code>

Anschließend, ein Commit <b>mit aussagekräftiger Commit-Message</b> (<code>-m</code>)...

<code>
git commit -a -m 'Added "florian@demine" to group gitosis-admin.'
</code>

Output
<code>
Created commit 819f0f0: Added "florian@demine" to group gitosis-admin
 1 files changed, 1 insertions(+), 1 deletions(-)
</code>

...und ein push um den Commit auf den Server zu übertragen:
<code>
git push
</code>

Output:
<code>
Counting objects: 6, done.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 534 bytes, done.
Total 4 (delta 1), reused 0 (delta 0)
To gitosis@birgit:gitosis-admin.git
   b2240d3..819f0f0  master -> master
</code>

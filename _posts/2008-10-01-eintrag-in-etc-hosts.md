---
tags:
- Linux
nid: 539
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/eintrag-in-etchosts.html"
layout: book
title: Eintrag in /etc/hosts
created: 1222813834
---
Damit unsere zukünfige Seite über einen <acronym title="Fully Qualified Domain Name">FQDN</acronym> erreichbar ist, erweitern wir die Datei /etc/hosts um die folgende Zeile:
<code>
127.0.0.1 example.com.localhost
</code>

---
tags:
- Drupal
- Linux
- howto
- php
- config
nid: 529
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration/php-memory_limit-hochsetzen.html"
layout: book
title: php memory_limit hochsetzen
created: 1222802203
---
Um einem "White-Screen" vorzubeugen wenn zu viele Drupal-Module installiert sind, 
setzen wir die memory_limit  in <i>/etc/php5/apache2/php.ini</i> höher.
<code>
memory_limit = 64M      ; Maximum amount of memory a script may consume (16MB)
</code>

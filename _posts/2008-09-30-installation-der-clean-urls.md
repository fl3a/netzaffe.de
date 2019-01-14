---
tags:
- Drupal
- SEO
- mod_rewrite
nid: 522
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration/installation-der-clean-urls.html"
layout: book
title: Installation der clean-urls
created: 1222756975
---
<p>Um das Feature der Suchmaschinenfreundlichen URL's(clean-url's) nutzen zu k&#246;nnen, mu&#223; noch das mod_rewrite-Modul aktiviert werden. Hier werden die symbolischen Links von /etc/apache2/mods-available nach /etc/apache2/mods-enabled gesetzt f&#252;r die entsprechenden Module gesetzt:</p>
<code ="bash">
a2enmod rewrite
</code>

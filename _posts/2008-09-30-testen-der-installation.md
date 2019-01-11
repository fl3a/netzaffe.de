---
tags:
- php
nid: 523
permalink: "/drupal-6-multisiteumgebung-mit-postgresql-unter-debian-4/konfiguration/testen-der-installation.html"
layout: book
title: Testen der Installation
created: 1222773604
---
<p>Zum testen der Apache-Installation geben wir den <acronym title="Fully Qualified Domain Name">FQDN</acronym> oder die IP-Adrese in Browser ein<br />
und sehen ein <strong>It works!</strong></p>
<p>Um zu testen, ob php l&auml;uft und alle ben&ouml;tigten Module enth&auml;lt legen wir eine Datei mit dem Namen index.php im Ordner /var/www an.</p>
<code type="bash">
echo -e "<?php\n  phpinfo();\n?>" >  /var/www/index.php 
</code>
<p>Anschlie&szlig;end rufen Datei index.php mit der <acronym title="Uniform Resource Locator">URL</acronym> unseres Webservers + /index.html &uuml;ber Browser auf<br />
und sehen in der Sektion apache2handler im Unterpunkt Loaded Modules, mod_rewrite und weiter unten die von Drupal ben&ouml;tigten PHP-Erweiterungen gd und pgsql.</p>

---
layout: post
tags:
- snippet
- Drupal
- Datenschutz
- cron
- "#!/bin/bash"
nid: 1652
redirect_from: node/1652
permalink: drupal-kommentare-dsgvo-konform.html
title: Drupal Kommentare DSGVO-konform
created: 1527412073
---
Um dem sinnigen Thema Datenschutz nicht nur im Rahmen der DSGVO bzw. GPDR nachzukommen, 
habe ich nach etwas Recherche in Punkto Kommentare (Achtung, das ist keine Rechtsberatung ;-D) für diese Site folgendes unternommen:

-  Die Mail-Benachrichtigung bei neuen Kommentaren via comment_notify[^1] habe ich deaktiviert und deinstalliert, da ich momentan keinen Weg kenne, 
dies mit Double-Opt-In umzusetzen.
- Ich nutze ich keinen Dienst für Spam-Erkennung von einem Drittanbeiter (vergl. Mollom o. Akismet), 
sondern setze auf die im Vergleich zu Captchas für den Benutzer weniger aufdringlichen Module Hashcash[^2] und Honeypot[^3]
- IP-Adressen in Kommentaren bewahre ich, aufgrund von berechtigtem Interesse 7 Tage auf, bevor ich diese mit Nullen überschreibe. 
Dafür habe ich ein kleine Shellskript geschrieben, welches ich via Cron ausführen lasse.<!--break-->

{% highlight bash lineos %}
!/bin/bash

# Anonymise hostname, which contains the ip address
# from Drupals comments table which are older than 7 days.

# Get UNIX timestamp from 7 days in the past
seven_days_ago_timestamp=`date +%s --date "-7 day"`

# SQL update statement to anonymise hostname within Drupals comment table
sql="UPDATE comments SET hostname='0.0.0.0' WHERE timestamp<$seven_days_ago_timestamp"

# Path to drupal root of your installation
drupal_root="/var/www/virtual/fl3a/netzaffe.de"

# Execute SQL update statement using Drupal's credentials via drush.
echo $sql | drush --root=$drupal_root sql-cli
{% endhighlight %}

- Das Kommentarformular wird wie alle anderen Formulare verschlüsselt via HTTPS[^4] übertragen. 
Ich habe mir ein Zertifikat von Lets Encrypt[^5] generiert und einfach jede Anfrage auf HTTPS weitergeleitet[^6].
Für die Weiterleitung von HTTP nach HTTPS in Drupals _.htaccess_ in der Sektion der _rewrite rules_  :

{% highlight apache %}
RewriteCond %{HTTPS} !=on
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
{% endhighlight %}

- Falls ihr Drupal 6 oder 7 verwendet, muss auch noch eure _settings.php_ auf HTTPS angepasst werden: `$base_url = 'https://netzaffe.de';`.

*[DSGVO]: Datenschutz-Grundverordung
*[GPDR]: General Data Protection Regulation
*[HTTPS]: Hypertext Transfer Protocol Secure

__Footnotes:__

[^1]: [comment_notify](https://www.drupal.org/project/comment_notify)
[^2]: [Hashcash](https://www.drupal.org/project/hashcash)
[^3]: [Honeypot](https://www.drupal.org/project/honeypot)
[^4]: [Uberspace: HTTPS](https://wiki.uberspace.de/webserver:https) 
[^5]: [letsencrypt](https://letsencrypt.org/)
[^6]: [Uberspace: HTTPS erzwingen](https://wiki.uberspace.de/webserver:security#https_erzwingen)

---
tags:
- Linux
- howto
- Git
- Debian
nid: 985
permalink: "/git-gitosis-gitweb-the-debian-way/konfiguraton-von-gitweb/etcgitweb-conf.html"
layout: book
title: "/etc/gitweb.conf"
created: 1268495028
---
Die Konfigurationsdatei für Gitweb, 
hier angepasst <code>$projectroot</code> welche auf das Verzeichnis <em>/srv/gitosis/repositories</em>, in dem gitosis seine Repos ablegt zeigt.

<code>
# path to git projects (<project>.git)
# $projectroot = "/var/cache/git";
$projectroot = "/srv/gitosis/repositories";

# directory to use for temp files
$git_temp = "/tmp";

# target of the home link on top of all pages
#$home_link = $my_uri || "/";

# html text to include at home page
$home_text = "indextext.html";

# file with project list; by default, simply scan the projectroot dir.
$projects_list = $projectroot;

# stylesheet to use
$stylesheet = "/gitweb.css";

# logo to use
$logo = "/git-logo.png";

# the 'favicon'
$favicon = "/git-favicon.png";
</code>
'

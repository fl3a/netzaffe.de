---
title: "netzaffe Legacy"
---

```
mysql> select title,nid from node where type='image' and promote=1; 
```
```
+------------------------------------------------+------+
| title                                          | nid  |
+------------------------------------------------+------+
| TAKE CARE                                      |  510 |
| Design Studio Punk Deluxe                      |  332 |
| FIBU Essen 2008                                |  558 |
| Köln-Buchforst zur EM 2008                     |  559 |
| Barmer Viertel - Gaststätte zur Post           |  561 |
| Sitzplatz für                                  |  564 |
| Barcodetonne                                   |  567 |
| Taxi bei BLAST                                 |  568 |
| Frisbee-Art oder ein Tisch?                    |  570 |
| Montainbike-Eldorado Hahnenkamm                |  583 |
| Jambaleia - ein Nachruf                        |  588 |
| rtfm                                           |  724 |
| Die Anderen                                    |  759 |
| My last daily scrum at BerlinOnline            |  844 |
| Lars - du Arsch                                |  848 |
| Critical Mass Cologne 2011-03-25               | 1022 |
| Angrillen 2012                                 | 1596 |
| Froscon 2012 - Social Event: Die Grillschlange | 1611 |
| Bassets BoF, DCVIE 2013                        | 1621 |
+------------------------------------------------+------+
```
<!--break-->

```
mysql> select distinct n.title,n.type,n.nid, b.bid, b.mlid from node n, book b where n.nid=b.nid and n.type='book' and n.status=1 and n.nid=b.bid;
+----------------------------------------------------------+------+------+------+------+
| title                                                    | type | nid  | bid  | mlid |
+----------------------------------------------------------+------+------+------+------+
| Arrays in der Bash                                       | book |  691 |  691 |  606 |
| Drupal 6 Multisiteumgebung mit PostgreSQL unter Debian 4 | book |  520 |  520 |  607 |
| Drush - Die Drupal-Shell                                 | book |  712 |  712 |  628 |
| GnuPG (GPG) Micro Howto                                  | book |  667 |  667 |  632 |
| Git, Gitosis, Gitweb (the Debian way)                    | book |  978 |  978 | 1857 |
| Features                                                 | book | 1602 | 1602 | 2888 |
+----------------------------------------------------------+------+------+------+------+
```

```
[fl3a@bellatrix netzaffe.de]$ echo 'select n.title,n.nid,r.body from fl3a.node_revisions r, fl3a.node n where n.nid = r.nid and n.promote=1;' | mysql| grep '<img' | sed -n 's/.*<img src="\([^"]*\)".*/\1/p'
```
```
http://upload.wikimedia.org/wikipedia/commons/1/1b/Scrum_task_board.jpg
/sites/netzaffe.de/files/postgres_cyg.gif
/sites/netzaffe.de/files/drupal-subconference-froscon.png
http://netzaffe.de/sites/netzaffe.de/files/lpi-lpic2-123x150.gif
/sites/netzaffe.de/files/floh-at-netzaffe-punkt-de.gif
http://netzaffe.de/sites/netzaffe.de/files/gfu_02.jpg
/sites/netzaffe.de/files/gpg.png
/sites/netzaffe.de/files/DrupalCampCologne/Robert_Happek/team-olga-nicer500x333.jpg
http://netzaffe.de/sites/netzaffe.de/files/git-logo.png
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
/sites/netzaffe.de/files/images/2010-drupaldevdays-munich-luckow-fl3a-scrum-presentation.preview.jpg
/sites/netzaffe.de/files/images/2010-drupaldevdays-munich-luckow-fl3a-scrum-presentation.preview.jpg
/sites/netzaffe.de/files/be-drupal.jpg
http://farm4.static.flickr.com/3552/3661911233_d82a07f38d.jpg?v=0
/sites/netzaffe.de/files/dcvie/tu-wien-besetzt.jpeg
http://netzaffe.de/sites/netzaffe.de/files/dcvie/drush_multi-session-drupalcamp-vienna.jpeg
http://netzaffe.de/sites/netzaffe.de/files/cssh-4-xterms.png
/sites/netzaffe.de/files/images/2011-drupalcity-berlin-fl3a-features-plus-presentation.preview.jpg
/sites/netzaffe.de/files/bad-code-php-vim-syntastic.png
/sites/netzaffe.de/files/agile-cologne-logo-220x81.jpeg
```

```
[fl3a@bellatrix netzaffe.de]$  echo 'select n.title,n.nid,r.body from fl3a.node_revisions r, fl3a.node n where n.nid = r.nid and n.promote=1;' | mysql | sed -n 's/.*src="\([^"]*\).*/\1/p'
```
```
http://upload.wikimedia.org/wikipedia/commons/1/1b/Scrum_task_board.jpg
http://upload.wikimedia.org/wikipedia/commons/1/1b/Scrum_task_board.jpg
/sites/netzaffe.de/files/postgres_cyg.gif
http://www.flickr.com/apps/slideshow/show.swf?v=59157
/sites/netzaffe.de/files/pictures/danksagung/mysql_100x52-64.gif
http://netzaffe.de/sites/netzaffe.de/files/lpi-lpic2-123x150.gif
http://www.flickr.com/apps/slideshow/show.swf?v=59157
http://www.flickr.com/apps/slideshow/show.swf?v=59157
/sites/default/files/6986332.jpg
/sites/netzaffe.de/files/floh-at-netzaffe-punkt-de.gif
http://netzaffe.de/sites/netzaffe.de/files/gfu_02.jpg
/sites/netzaffe.de/files/gpg.png
http://video.google.com/googleplayer.swf?docid=1354489314660322075&hl=de&fs=true
http://www.youtube.com/v/k07XZZLZ9Fw&hl=de&fs=1
https://netzaffe.de/sites/netzaffe.de/files/flyer_produkt_xmas_final.jpg
/sites/netzaffe.de/files/images/dsc00126.preview.jpg
/sites/netzaffe.de/files/images/schneemann-berlin.preview.jpg
/sites/netzaffe.de/files/DrupalCampCologne/Robert_Happek/team-olga-nicer500x333.jpg
http://netzaffe.de/sites/netzaffe.de/files/git-logo.png
http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=drupaldrush-090512153315-phpapp02&rel=0&stripped_title=drush-das-sackmesser-fr-die-kommandozeile-1425211
http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=drupaldrush-090512153315-phpapp02&rel=0&stripped_title=drush-das-sackmesser-fr-die-kommandozeile-1425211
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=scrum-aus-der-praxis-ddd2010-100512094931-phpapp02&stripped_title=scrum-aus-der-praxis-drupaldevdays-2010
/sites/netzaffe.de/files/images/2010-drupaldevdays-munich-luckow-fl3a-scrum-presentation.preview.jpg
http://vimeo.com/moogaloop.swf?clip_id=4631958&amp;server=vimeo.com&amp;show_title=1&amp;show_byline=1&amp;show_portrait=0&amp;color=00ADEF&amp;fullscreen=1
http://vimeo.com/moogaloop.swf?clip_id=4631958&amp;server=vimeo.com&amp;show_title=1&amp;show_byline=1&amp;show_portrait=0&amp;color=00ADEF&amp;fullscreen=1
/sites/netzaffe.de/files/be-drupal.jpg
http://www.flickr.com/apps/slideshow/show.swf?v=71649
http://www.youtube.com/v/0mra4UmIn4I&amp;hl=de&amp;fs=1&amp;
http://www.youtube.com/v/0mra4UmIn4I?fs=1&amp;hl=de_DE
http://www.youtube.com/v/0mra4UmIn4I?fs=1&amp;hl=de_DE
/sites/netzaffe.de/files/dcvie/tu-wien-besetzt.jpeg
http://netzaffe.de/sites/netzaffe.de/files/dcvie/drush_multi-session-drupalcamp-vienna.jpeg
http://netzaffe.de/sites/netzaffe.de/files/cssh-4-xterms.png
/sites/netzaffe.de/files/DSC00090-500px.jpg
/sites/netzaffe.de/files/images/2011-drupalcity-berlin-fl3a-features-plus-presentation.preview.jpg
http://netzaffe.de/sites/netzaffe.de/files/how-much-time-i-wasted-on-facebook-2014-08-05.png
http://netzaffe.de/sites/netzaffe.de/files/how-much-time-i-wasted-on-facebook-2014-08-05.png
http://netzaffe.de/sites/netzaffe.de/files/doxygen-var-doxygen-notation.png
/sites/default/files/PSMI.png
/sites/default/files/PSMI.png
/sites/netzaffe.de/files/bad-code-php-vim-syntastic.png
/sites/netzaffe.de/files/eine-einfuehrung-in-scrum-roger-pfaff-florian-latzel-drupalcamp-munic-2016-khe.jpg
/sites/netzaffe.de/files/eine-einfuehrung-in-scrum-roger-pfaff-florian-latzel-drupalcamp-munic-2016-khe.jpg
//platform.twitter.com/widgets.js
/sites/netzaffe.de/files/44-sessions-at-dcruhr18-highscore-bru.jpg
/sites/netzaffe.de/files/michael-lenahan-and-florian-latzel-explaining-open-space-dcruhr18-rokr.jpg
/sites/netzaffe.de/files/florian-latzel-neues-team-was-nun-dcruhr18-jkl.jpg
```

```
[fl3a@bellatrix ~]$ xzcat /mysqlbackup/latest/fl3a/fl3a/node_revisions.sql.xz | sed -n 's/.*src="\([^"]*\).*/\1/p'
```

```
[fl3a@bellatrix ~]$ var=`echo 'select n.title,n.nid,r.body from fl3a.node_revisions r, fl3a.node n where n.nid = r.nid and n.promote=1;' | mysql`
[fl3a@bellatrix ~]$ echo -e $var | sed -n 's/.*src="\([^"]*\).*/\1/p'| uniq 
```

```
var=`echo 'select r.body from fl3a.node_revisions r, fl3a.node n where n.nid = r.nid and n.promote=1;' | mysql`              
echo -e $var | sed -n 's/.*src="\([^"]*\).*/\1/p'| uniq | grep 'netzaffe.de'
```

```
/sites/netzaffe.de/files/postgres_cyg.gif
/sites/netzaffe.de/files/drupal-subconference-froscon.png
/sites/netzaffe.de/files/pictures/danksagung/mysql_100x52-64.gif
http://netzaffe.de/sites/netzaffe.de/files/lpi-lpic2-123x150.gif
/sites/netzaffe.de/files/floh-at-netzaffe-punkt-de.gif
http://netzaffe.de/sites/netzaffe.de/files/gfu_02.jpg
/sites/netzaffe.de/files/gpg.png
/sites/netzaffe.de/files/drupal-xmas.jpg
https://netzaffe.de/sites/netzaffe.de/files/flyer_produkt_xmas_final.jpg
/sites/netzaffe.de/files/images/dsc00126.preview.jpg
/sites/netzaffe.de/files/images/schneemann-berlin-und-gomez.preview.jpg
/sites/netzaffe.de/files/images/schneemann-berlin.preview.jpg
/sites/netzaffe.de/files/DrupalCampCologne/Betty/DrupalCampDE-Abschlussfoto500x269.jpg
/sites/netzaffe.de/files/DrupalCampCologne/Hagen_Graf/narres-und-peter-hecker.jpg
/sites/netzaffe.de/files/DrupalCampCologne/Robert_Happek/team-olga-nicer500x333.jpg
http://netzaffe.de/sites/netzaffe.de/files/git-logo.png
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
/sites/netzaffe.de/files/images/drupal-drush-drupalmediacamp-2009.sitepreview.jpg
/sites/netzaffe.de/files/images/2010-drupaldevdays-munich-luckow-fl3a-scrum-presentation.preview.jpg
/sites/netzaffe.de/files/images/-3.preview.jpg
/sites/netzaffe.de/files/be-drupal.jpg
/sites/netzaffe.de/files/dcvie/SirFiChi-und-fl3a-im-hotel-tag0.jpeg
/sites/netzaffe.de/files/dcvie/thomas-renner-gig-im-down-under-wien.jpeg
/sites/netzaffe.de/files/dcvie/down-under-wien.jpeg
/sites/netzaffe.de/files/dcvie/nachhilfe-von-dereine-im-zug-tag3.jpeg
/sites/netzaffe.de/files/dcvie/nachhilfe-von-dereine-im-zug-tag3-2.jpeg
/sites/netzaffe.de/files/dcvie/sirfichi-im-zug-tag3.jpeg
/sites/netzaffe.de/files/dcvie/tu-wien-besetzt.jpeg
http://netzaffe.de/sites/netzaffe.de/files/dcvie/drush_multi-session-drupalcamp-vienna.jpeg
http://netzaffe.de/sites/netzaffe.de/files/cssh-4-xterms.png
/sites/netzaffe.de/files/DSC00090-500px.jpg
/sites/netzaffe.de/files/images/2011-drupalcity-berlin-fl3a-features-plus-presentation.preview.jpg
http://netzaffe.de/sites/netzaffe.de/files/how-much-time-i-wasted-on-facebook-2014-08-05.png
http://netzaffe.de/sites/netzaffe.de/files/doxygen-var-doxygen-notation.png
/sites/netzaffe.de/files/bad-code-php-vim-syntastic.png
/sites/netzaffe.de/files/eine-einfuehrung-in-scrum-roger-pfaff-florian-latzel-drupalcamp-munic-2016-khe.jpg
/sites/netzaffe.de/files/agile-cologne-logo-220x81.jpeg
/sites/netzaffe.de/files/open-space-agile-cologne-2017_0.jpg
/sites/netzaffe.de/files/project-end-retrospective-agile-cologne-2017.jpg
/sites/netzaffe.de/files/the-me-in-all-the-we-agile-cologne-2017_0.jpg
/sites/netzaffe.de/files/the-me-in-all-the-we-agile-cologne-2017-2.jpg
/sites/netzaffe.de/files/agilecologne17/agile-cologne-logo-220x81.jpeg
/sites/netzaffe.de/files/agilecologne17/open-space-agile-cologne-2017_0.jpg
/sites/netzaffe.de/files/agilecologne17/project-end-retrospective-agile-cologne-2017.jpg
/sites/netzaffe.de/files/agilecologne17/the-me-in-all-the-we-agile-cologne-2017_0.jpg
/sites/netzaffe.de/files/agilecologne17/the-me-in-all-the-we-agile-cologne-2017-2.jpg
/sites/netzaffe.de/files/haben-alle-das-session-board-fotografiert-tag2-rokr-dcruhr18.jpg
/sites/netzaffe.de/files/michael-lenahan-and-florian-latzel-explaining-open-space-dcruhr18-rokr.jpg
/sites/netzaffe.de/files/openspace-marketplace-day2-dcruhr18-dasjo-amazee.jpg
/sites/netzaffe.de/files/44-sessions-at-dcruhr18-highscore-bru.jpg
/sites/netzaffe.de/files/haben-alle-das-session-board-fotografiert-tag2-rokr-dcruhr18.jpg
/sites/netzaffe.de/files/michael-lenahan-and-florian-latzel-explaining-open-space-dcruhr18-rokr.jpg
/sites/netzaffe.de/files/dcruhr18/haben-alle-das-session-board-fotografiert-tag2-rokr-dcruhr18.jpg
/sites/netzaffe.de/files/dcruhr18/michael-lenahan-and-florian-latzel-explaining-open-space-dcruhr18-rokr.jpg
/sites/netzaffe.de/files/dcruhr18/openspace-marketplace-day2-dcruhr18-dasjo-amazee.jpg
/sites/netzaffe.de/files/dcruhr18/44-sessions-at-dcruhr18-highscore-bru.jpg
/sites/netzaffe.de/files/florian-latzel-neues-team-was-nun-dcruhr18-jkl.jpg
/sites/netzaffe.de/files/dcruhr18/florian-latzel-neues-team-was-nun-dcruhr18-jkl.jpg
```

In Dateien ersetzen, Anpassung neue Img src:
```
 find /<Pfad>/<Dateien> -type f -exec sed -i 's/<alter Begriff>/<neuer Begriff>/g' {} \; 
```

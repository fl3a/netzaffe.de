---
title: "s/Drupal/Jekyll"
tags: 
- Drupal
- Jekyll
- SSG
- netzaffe
layout: post
toc: true
---
tl;dr Ich bin vom Drupal CMS Framework[^drupal] auf Jekyll[^jekyll], 
einen *Statischen Seiten Generator*(kurz SSG) umgestiegen.
Das folgende hat mich zum Umstieg bewegt und an Jekyll überzeugt.
 
Ich betreibe dieses Blog, oder genauer gesagt,
das Stück Software aus dem dieses Blog hervorgegangen ist seit 15 Jahren.
Das waren 15 Jahre mit Drupal, gestartet mit der Version 4.5
(das hier war auch immer meine Spielwiese um z.B. interessante Drupal-Module auzuprobieren).
2009 habe ich das Update auf Drupal 6 gemacht, seit dem Erscheinen von Drupal 2016, 
nutze ich mit ein paar Verbiegungen Drupal 6 LTS aus der Community 
(es werden laut Drupal Policy immer nur 2 Versionen unterstützt, 
ergo zu diesen Zeitpunkt Drupal in der Version 7 und v.8.).

Am Ende ist und bleibt es aber, auch trotz Versorgung mit Sicherheits-Updates 
ein 10 Jahre altes Stück Software mit einer altertümlichen Anmutung, weit vor der *Ära Mobile*. 
Zudem gibts es sicherlich auch das ein oder andere Rudiment in der Datenbank,
verursacht durch diverse Module, die diese Installation in diesen Jahren er- und überlebt hat.

Da ein Update IMHO unabwendbar war, habe ich teils mit dafür gesorgt, 
daß die von mir benötigten Module auch für Drupal 8 zur Verfügung stehen, 
und habe mit an Module-Portierungen für Drupal 8 gearbeitet, 
z.B. Footnotes[^fn], GeshiFilter[^geshi] oder Gist Input Filter[^gist].
Aber unabhängig davon, daß die Migrations-Versuche bei mir nicht auf korrekt durchliefen,
hat sich für mich Drupal 8 zu groß und sperrig angefühlt. 
Vielleicht waren es ja auch die massiven Änderungen von Drupal 7 nach 8...
 
Schon recht lange stand der Jekyll in meinem Backlog (Danke Ben für die Inspiration!), 
im Winter 2018 bin ich dann mal dazu gekommen, Jekyll zu installieren und bin das Step by Step Tutorial[^sbst]  
durchgegangen.

Aber was hat mich an Jekyll so begeistert 
und mich dazu bewegt auf einen SSG zu wechseln?<!--break-->

# Warum Jekyll?

## Drupal-Importer

Jekyll hat einen Drupal Importer für die Versionen 6 und 7, das ist weniger einr Beweggrund, 
als eine Grundvorraussetzung, da ich meine *Nodes*, also meine Beiträge natürlich mitnehmen will.

## KISS - Jekyll ist einfach.  

### Einfacher Start

Sofern *Ruby* und *Ruby Gems* installiert und konfiguriert sind ist nur ein `gem install jekyll bundler`
für die Installation, 
ein `jekyll new example.com` für das Erstellen einer Site (jekyll)
und ein `bundle exec jekyll serve --drafts` das *Hochfahren* des lokalen Webservers,
der dann unter *http://127.0.0.1:4000* erreichbar ist notwendig
um mit Jekyll lokal auf Tuchfühlung zu gehen.

### Einfache Struktur

Jekylls Funktionsweise spiegelt sich in der einfachen Verzeichnisstruktur[^dir] wider:
```
example.com
├── 404.html
├── _config.yml
├── Gemfile
├── Gemfile.lock
├── index.md
├── _drafts
|   ├── ideenfindung.md
|   └── hier-wird-noch-dran-gefeilt.md
├── _posts
|   └── 2019-04-22-agile-ruhr-hattrick.md
└── _site
    ├─ 2019
    |   └── 04
    |         └── 22
    |             └── agile-ruhr-hattrick.html
    ├── 404.html
    ├── feed.xml
    └── index.html
```

Im Minimalumfang sind die folgenden Einträge relevent:
- *_config.yml* 
  Config
- *_drafts*
   
- *_posts* 
- *_site*

### Geringe Komplexität


### Markdown

Markdown[^md] [^kramdown]


## Geschwindigkeit 

- Plain HTML

## Keine Sicherheits-Updates

Beim 2. Drupalgeddon 2[^sa] [^sa1], das hatte ein Risiko-Level[^risk] von 24 bei einer Skala bis 25, 
kam ich mit meiner handvoll Drupal Sites doch etwas ins Schwitzen.

## Viele Erweiterungen 

https://github.com/topics/jekyll-plugin

## Nerdy Arbeitsweise


- Git 
- 

## Ein neues Spielzeug

- Liquid Template Engine[^liquid]

## Fußnoten & Weiterführendes

[^drupal]: [Drupal CMS](https://drupal.org)
[^jekyll]: [Jekyll](https://jekyllrb.com)
[^hacks]: Modifiertes Drush, MydropWizzard Modul und Updates über github statt d.o[^do]
[^fn]: [footnotes 8.x port](https://www.drupal.org/sandbox/fl3a/2593257)
[^sbst]: [Jekyll Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
[^geshi]: [GeSHi Filter for syntax highlighting](https://www.drupal.org/project/geshifilter)
[^gist]: [Gist Input Filter (gist_filter) 8.x Port](https://www.drupal.org/sandbox/fl3a/2819998)
[^dir]: [Jekyll: Directory Structure](https://jekyllrb.com/docs/structure/)
[^md]: [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax)
[^sa]: [Drupal core - Highly critical - Remote Code Execution - SA-CORE-2018-002](https://www.drupal.org/SA-CORE-2018-002)
[^sa1]: [Drupalgeddon 2: Angreifer attackieren ungepatchte Drupal-Webseiten](https://www.heise.de/security/meldung/Drupalgeddon-2-Angreifer-attackieren-ungepatchte-Drupal-Webseiten-4024700.html)
[^kramdown]: [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html)
[^liquid]: [Liquid template language](https://shopify.github.io/liquid/)

*[CMS]: Content Management System
*[SSG]: Statischer Seiten Generator
*[LTS]: Long Term Support
*[KISS]: Keep It Stupid Simple

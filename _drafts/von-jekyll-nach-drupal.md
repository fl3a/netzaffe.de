---
title: "s/Drupal/Jekyll"
tags: 
- Drupal
- Jekyll
- SSG
- netzaffe
layout: post
toc: true
image: /assets/imgs/jekyll-logo-light-solid.png
---
<figure role="group">
  <img src="/assets/imgs/jekyll-logo-light-solid.png" alt="Jekyll SSG Logo" />
  <figcaption>Jekyll Logo, CC-BY 4.0</figcaption>
</figure>
tl;dr Seit Angfang 2019 läuft mein Blog bereits mit Jekyll [^jekyll], 
einen *Statischen Seiten Generator*(kurz SSG).
Dieser Artikel beschreibt, warum ich vom [^drupal] CMS Framework auf Jekyll umgestiegen bin
und was mich an Jekyll so überzeugt hat.<!--break-->

# Ein Stück Blog Geschichte

Ich betreibe dieses Blog, oder genauer gesagt,
das Stück Software aus dem dieses Blog hervorgegangen ist sei 2004.
Das waren 15 Jahre mit Drupal, gestartet mit der Version 4.5.
Diese Installation war auch immer meine Spielwiese um z.B. interessante Drupal-Module auzuprobieren.
In 2009 habe ich dann das Update auf Drupal 6 gemacht, 
seit dem Erscheinen von Drupal 2016, 
nutze ich mit ein paar Verbiegungen[^hacks] Drupal 6 LTS aus der Community 
(es werden laut Drupal Policy immer nur 2 Versionen unterstützt, 
ergo zu diesen Zeitpunkt Drupal in der Version 7 und v.8.).

Trotz der Versorgung mit Sicherheits-Updates und abgesehen von dem ein oder andere Rudiment in der Datenbank,
verursacht durch diverse Module, die diese Installation in diesen Jahren er- und überlebt hat,
ist und bleibt es ein 10 Jahre altes Stück Software mit einer recht altertümlichen Anmutung, weit vor der *Ära Mobile*. 

Somit war für mich Update unabwendbiar, also habe ich teils mit dafür gesorgt, 
daß die von mir benötigten Module auch für Drupal 8 zur Verfügung stehen, 
und habe entsprechend mit an entsprechenden Modul-Portierungen für Drupal 8 mitgearbeitet, 
z.B. an Footnotes[^fn], GeshiFilter[^geshi] oder dem Gist Input Filter[^gist].
Aber unabhängig davon, daß die Migrations-Versuche bei mir auf Anhieb nicht korrekt durchliefen,
hat sich für mich Drupal 8 mittlerweile als zu groß und sperrig für einen simplen Blog angefühlt.
 
Da war dann noch Jekyll, welches schon recht lange in meinem Backlog stand (Danke Ben von der GzEvD für die Inspiration!).
Im Winter 2018 bin ich dann mal dazu gekommen, Jekyll zu installieren und bin das Step by Step Tutorial[^sbst]  
durchzugehen.

Aber was hat mich an Jekyll so begeistert und mich dazu bewegt auf einen SSG zu wechseln?<!--break-->

# Warum Jekyll?

## Drupal-Importer

Jekyll hat einen Drupal Importer für die Versionen 6 und 7, 
das ist natürlich weniger ein Beweggrund, 
als eine Grundvorraussetzung, 
da ich meine *Nodes*, also meine geschriebenen Beiträge natürlich mitnehmen wollte.

## KISS - Jekyll ist einfach.  

### Einfacher Start

Mit bereits installiertem *Ruby* und *Ruby Gems* sind es nur ein `gem install jekyll bundler`
für die Installation, 
ein `jekyll new example.com` für das Erstellen einer Site 
und ein `bundle exec jekyll serve --drafts` das *Hochfahren* des lokalen Webservers,
der dann unter *http://127.0.0.1:4000* erreichbar ist notwendig
um mit einem lokalem Jekyll auf Tuchfühlung zu gehen.

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
- *_config.yml*   Config
- *_drafts*
- *_posts* 
- *_site*

### Geringe Komplexität

- Keine DB
- Keine besonderen Ansprüche an den Webserver
 - Keine Skriptsprache auf Live-Server
- Alles in Dateien 

### Markdown

Markdown[^md] [^kramdown]

## Geschwindigkeit 

- Plain HTML

## Keine Sicherheits-Updates

Beim 2. Drupalgeddon 2[^sa] [^sa1], das hatte ein Risiko-Level[^risk] von 24 bei einer Skala bis 25, 
kam ich mit meiner handvoll Drupal Sites doch etwas ins Schwitzen.

## Viele Erweiterungen 

Wg der weiten Verbreitung, die unter an

https://github.com/topics/jekyll-plugin

## Nerdy Arbeitsweise

- Git 

## Ein neues Spielzeug

- Liquid Template Engine[^liquid]

# Fußnoten & Weiterführendes

[^drupal]: [Drupal CMS](https://drupal.org)
[^jekyll]: [Jekyll](https://jekyllrb.com)
[^hacks]: Modifiertes Drush in Symbiose mit dem [MydropWizzard Modul](https://www.drupal.org/project/mydropwizard) für Updates über github statt d.o
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
*[GzEvD]: Gesellschaft zur Entwicklung von Dingen mbH
*[d.o]: drupal.org

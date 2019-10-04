---
title: "s/Drupal/Jekyll"
tags: 
- Drupal
- Jekyll
- SSG
- netzaffe
layout: post
toc: true
image: /assets/imgs/jekyll-logo-dark-solid.png
---
<figure role="group">
  <img src="/assets/imgs/jekyll-logo-dark-solid.png" alt="Jekyll Logo, dark solid " />
  <figcaption>Jekyll Logo, CC-BY 4.0</figcaption>
</figure>
tl;dr Seit Angfang 2019 läuft mein Blog bereits mit Jekyll [^jekyll], 
einen *Statischen Seiten Generator*(kurz SSG).
Dieser Artikel beschreibt, warum ich vom Drupal[^drupal] CMS Framework auf Jekyll umgestiegen bin
und was mich an Jekyll überzeugt hat.<!--break-->

# Geschichtsabriss

Ich betreibe dieses Blog, oder genauer gesagt,
das Stück Software aus dem dieses Blog hervorgegangen ist sei 2004.
Das waren 15 Jahre mit Drupal, gestartet mit der Version 4.5.
Diese Installation war auch immer meine Spielwiese um z.B. interessante Drupal-Module auzuprobieren.
In 2009 habe ich dann das Update auf Drupal 6 gemacht.
Seit dem Erscheinen von Drupal 8 im Jahr 2016, 
nutze ich  Drupal 6 LTS mit einigen Verbiegungen[^hacks], 
welches weiterhin aus der Community mit Updates weitervorsorgt wird.
Es sei angemerkt, dass laut Drupal Policy immer nur 2 Versionen unterstützt werden, 
ergo zu diesen Zeitpunkt Drupal in der Version 7 und v.8.

Trotz der Versorgung mit Sicherheits-Updates 
und abgesehen von dem ein oder andere Rudiment in der Datenbank,
verursacht durch diverse Module, 
die diese Installation in den Jahren er- und überlebt hat,
ist und bleibt es ein 10 Jahre altes Stück Software 
mit einer recht altertümlichen Anmutung, weit vor der *Ära Mobile*. 

Ein Upgrade war unabwendbar, also habe ich teils mit dafür gesorgt, 
daß die von mir benötigten Module auch für Drupal 8 zur Verfügung stehen, 
und habe entsprechend mit an entsprechenden Modul-Portierungen für Drupal 8 mitgearbeitet, 
z.B. an Footnotes[^fn], GeshiFilter[^geshi] oder dem Gist Input Filter[^gist].
Aber unabhängig davon, daß die Migrations-Versuche 
nach Drupal 8 bei mir auf Anhieb nicht korrekt durchliefen,
hat sich für mich Drupal 8 mittlerweile als zu groß 
und sperrig für einen simplen Blog angefühlt.
 
Da war dann noch Jekyll, 
welches schon recht lange in meinem Backlog stand 
(Danke Ben von der GzEvD für die Inspiration!).
Im Winter 2018 bin ich dann mal dazu gekommen, 
Jekyll zu installieren und bin das Step by Step Tutorial[^sbst] durchzugehen.

Aber was hat mich an Jekyll so begeistert und mich dazu bewegt auf einen SSG zu wechseln?

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
der dann unter *http://127.0.0.1:4000* erreichbar ist notwendig,
um mit einem lokalem Jekyll auf Tuchfühlung zu gehen.

### Einfache Struktur

Jekylls einfache Funktionsweise spiegelt sich in der Verzeichnisstruktur[^dir] wider:

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

Im Minimalumfang sind die folgenden Einträge relevant:
- *_config.yml* Die zentrale Konfigurationsdatei, 
hier werden grundlegende Einstellungen für die Website und seine Erweiterungen vorgenommen.
- *_drafts* Hier liegen, wie der Name bereits vermuten lässt, 
Entwürfe. 
- *_posts* Der Ordner für die publizierten Artikel.
Den Posts muss noch ein Datumsprefix vorangestellt werden.
- *_site* Der Output, von Jekyll erzeugte, statische HTML Dateien.
Das was am Ende via Webserver oder `jekyll serve` ausgeliefert wird.

### Geringe Komplexität

Jekyll benötigt im Vergleich zu einem CMS wie Drupal keine Datenbank
und damit verbunden auch keine Programmiersprache wie PHP, 
die die Verbindung zur DB herstellt 
um die nötigen SQL-Abfragen für den Aufbau der Seite auszuführen.

Somit fallen nicht nur die Konfiguration der Datenbank, 
hier MySQL bzw MariaDB und von PHP weg,
sondern auch die des Webservers.
Es reichen eigentlich gängige Voreinstellungen bei Apache aus.
Also keine wechselseitigen Abhängkeiten 
und einzelnen Stellschrauben wie bei LAMP mehr.

Das alles führt zu einer deutlichen Veringerung der Komplexität.

### Markdown

Markdown[^md] [^kramdown]

## Geschwindigkeit 

Bei Drupal erfolgt zuerst der sogenannte *Bootstrap Prozess[^boot1] [^boot2]*, 
welcher für das Laden der Konfiguration, Initialsierung der Datenbank und Variablen zuständig ist.
Dann erfolgt unter anderem via Auswertung der URL was Ausgeliefert wird, 
hier kommt maßgeblich die Datenbank an ins Spiel.

Auch wenn das sog. Bootstrapping bei anderen CMS unterschiedlich sein mag,
gleich ist die Ausführung von Code und Datenbankabfragen 
für die dynamische Darstellung eines Reqests.
Im Gegensatz zum CMS, hier werden beim SSG statische HTML Dateien ausgespielt.

## Keine Sicherheits-Updates

Durch die Verwendung einer Serverseitigen Skriptsprache,
egal ob es nun PHP, Python oder Perl im Beispiel des Apache Webservers ist, 
kann auch auf das CMS zugegriffen werden.
Software, wie CMS enthält potenziell wie jede andere Software auch Fehler, 
gleiches gilt auch für Zusatzmodule,
welche nicht den Funktionsumfang vergrößern, sondern auch das Einfallstor
für Angriffe.

Wie beim Punkt Geschwindgkeit, punktet hier auch wieder statisches HTML,
das aus dem SSG erzeugt wird. Da keine Skiptsprache bzw. Software nachgelagert ist
bzw. diese nicht über die Anfrage auf den Webserver erreichbar ist, 
fällt dieser Angriffsvektor weg.

## Viele Erweiterungen 

Wg der weiten Verbreitung, die unter an

https://github.com/topics/jekyll-plugin

## Nerdy Arbeitsweise

- Alles in Dateien
- Konsole
- Vim 
- Git 

## Ein neues Spielzeug

- Importer
- Liquid Template Engine[^liquid]
- Module, Wege, probieren

# TBD

# Fußnoten & Weiterführendes

[^drupal]: [Drupal CMS](https://drupal.org)
[^jekyll]: [Jekyll](https://jekyllrb.com)
[^hacks]: Pressflow Drupal, modifiertes Drush in Symbiose mit dem [MydropWizzard Modul](https://www.drupal.org/project/mydropwizard) für Updates über github statt d.o
[^fn]: [footnotes 8.x port](https://www.drupal.org/sandbox/fl3a/2593257)
[^sbst]: [Jekyll Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
[^geshi]: [GeSHi Filter for syntax highlighting](https://www.drupal.org/project/geshifilter)
[^gist]: [Gist Input Filter (gist_filter) 8.x Port](https://www.drupal.org/sandbox/fl3a/2819998)
[^dir]: [Jekyll: Directory Structure](https://jekyllrb.com/docs/structure/)
[^md]: [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax)
[^kramdown]: [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html)
[^boot1]: [How Drupal returns a page request](https://befused.com/drupal/page-request)
[^boot2]: [How Drupal handles the page request: Bootstrap Process](https://www.valuebound.com/resources/blog/how-drupal-handles-page-request-bootstrap-process)
[^sa]: [Drupal core - Highly critical - Remote Code Execution - SA-CORE-2018-002](https://www.drupal.org/SA-CORE-2018-002)
[^sa1]: [Drupalgeddon 2: Angreifer attackieren ungepatchte Drupal-Webseiten](https://www.heise.de/security/meldung/Drupalgeddon-2-Angreifer-attackieren-ungepatchte-Drupal-Webseiten-4024700.html)
[^risk]: [Security risk levels defined](https://www.drupal.org/drupal-security-team/security-risk-levels-defined)
[^liquid]: [Liquid template language](https://shopify.github.io/liquid/)

*[CMS]: Content Management System
*[SSG]: Statischer Seiten Generator
*[LTS]: Long Term Support
*[KISS]: Keep It Stupid Simple
*[GzEvD]: Gesellschaft zur Entwicklung von Dingen mbH
*[d.o]: drupal.org
*[LAMP]: Linux Apache MySQL PHP

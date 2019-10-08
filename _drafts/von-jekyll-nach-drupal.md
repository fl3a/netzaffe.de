---
title: "s/Drupal/Jekyll"
tags: 
- Drupal
- Jekyll
- Open Source
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
tl;dr Seit Anfang 2019 läuft mein Blog bereits mit Jekyll[^jekyll], 
einen *Statischen Seiten Generator*.
Dieser Artikel beschreibt, 
warum ich nach fast 15 Jahren *Drupal CMS Framework*[^drupal] 
auf den *Jekyll SSG* umgestiegen bin.<!--break-->

# Kleiner Geschichtsabriss

Ich betreibe dieses Blog, oder genauer gesagt,
das Stück Software aus dem dieses Blog hervorgegangen ist seit 2004.
Das waren um die 15 Jahre mit Drupal, gestartet mit der Version 4.5.
Diese Installation war auch immer meine Spielwiese um z.B. interessante Drupal-Module auzuprobieren.
In 2009 habe ich dann das Update von Drupal 5 auf Drupal 6 gemacht.

Seit dem Erscheinen von Drupal 8 im Jahr 2016, 
nutze ich  Drupal 6 LTS mit einigen Verbiegungen[^hacks], 
welches weiterhin aus der Community mit Sicherheits-Updates versorgt wird.
Es sei angemerkt, dass laut Drupal Policy immer nur 2 Versionen unterstützt werden, 
ergo zu diesen Zeitpunkt Drupal in der Version 7 und v.8.

Trotz der Versorgung mit Sicherheits-Updates 
und abgesehen von dem ein oder andere Rudiment in der Datenbank aus den Jahren,
ist und bleibt es ein 10 Jahre altes Stück Software 
mit einer recht altertümlichen Anmutung, weit vor der *Ära Mobile*. 

Ein Upgrade war unabwendbar, also habe ich teils mit dafür gesorgt, 
daß die von mir benötigten Module auch für Drupal 8 zur Verfügung stehen
und habe entsprechend mit an entsprechenden Modul-Portierungen für Drupal 8 mitgearbeitet. 
Z.B. an Footnotes[^fn], GeshiFilter[^geshi] oder dem Gist Input Filter[^gist].
Aber unabhängig davon, daß die Migrations-Versuche 
nach Drupal 8 bei mir auf Anhieb nicht korrekt durchliefen,
hat sich für mich Drupal 8 irgendwie als zu groß und sperrig 
für einen simples Blog wie meines angefühlt.
 
Aber da war dann noch Jekyll, 
welches seit Anfang 2016 in meinem Backlog stand 
(Danke Ben von der GzEvD für die Inspiration!).
Im Winter 2018 bin ich dann endlich dazu gekommen, 
Jekyll zu installieren und bin das Step by Step Tutorial[^sbst] durchzugehen.

# Warum Jekyll?

Was hat mich an Jekyll so begeistert und mich dazu bewegt auf diesen SSG zu wechseln?

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

Jekylls einfache Funktionsweise spiegelt sich auch seiner Verzeichnisstruktur[^dir] wider:

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
- *Gemfile + Gemfile.lock* Die Abhängigkeiten für dieses Projekt. 
Hier werde die sog. Gems[^gems], wie Jekyll selbst und seine Plugins inkl. Version festgehalten,
welche via Bundler[^gems] verwaltet werden. Bundler lässt sich Composer[^composer] in der Drupal/PHP-Welt vergleichen.
- *_drafts* Hier liegen, wie der Name bereits vermuten lässt, Entwürfe. 
- *_posts* Der Ordner für die publizierten Artikel.
Den Posts muss noch ein Datumsprefix vorangestellt werden.
- *_site* Die von Jekyll erzeugte Website bestehend aus statischen HTML-Dateien.
Das was am Ende auf einem Webserver oder `jekyll serve` ausgeliefert wird.

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
und einzelnen Stellschrauben wie bei LAMP in Setup und Betrieb mehr.

Das alles führt zu einer deutlichen Veringerung der Komplexität.

### Markdown

Markdown[^md] ist eine vereinfachte Auszeichnungssprache.
Ein erklärtes Ziel bei der Entstehung von Markdown war die leichte lesbarkeit.

Bei Jekyll kommt der Markdown Dialekt Kramdown[^kramdown] zum Einsatz.
Im dessen Umfang befinden sich neben klassischen Text-Markup 
unter anderem auch Fußnoten, Tabellen, Definitions-Listen und Abkürzungen.

Im Gegensatz zum HTML ist Markdown nicht nur viel leichter lesbar, 
sondern auch wesentlich schlanker und entsprechend einfach 
und auch ohne WYSIWYG Editor gut und recht intuitiv schreibar.

## Geschwindigkeit 

Bei Drupal erfolgt zuerst der sogenannte *Bootstrap Prozess*[^boot1] [^boot2],
welcher für das Laden der Konfiguration, 
Initialsierung der Datenbank und Variablen zuständig ist.
Dann erfolgt unter anderem via Auswertung der URL was ausgeliefert wird, 
hier kommt maßgeblich die Datenbank an ins Spiel.

Auch wenn das sog. Bootstrapping bei anderen CMS unterschiedlich sein mag,
gleich ist die Ausführung von Code und Datenbankabfragen 
für die dynamische Auslieferung eines Requests.

Im Vergleich zum CMS, hier werden beim SSG statische HTML Dateien ausgespielt,
das ist wesentlich performanter.

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

Spätestens seit dem letzten Drupalgeddon[^sa1] [^sa2], bin ich heilfroh, 
dass Sicherheits-Updates nichts mehr sind, 
worum ich mich kümmern muss!

## Viele Plugins & Themes 

Wegen der weiten Verbreitung von Jekyll, die unter an darin begründet ist,
dass die *GitHub Pages*[^githubpages] auch mit Jekyll betrieben werden können,
gibt es eine nicht geringe Anzahl von sog. Plugins und Themes:

Plugins
- [jekyll-plugin topic auf GitHub](https://github.com/topics/jekyll-plugin)
- [Planet Jekyll](https://github.com/planetjekyll/awesome-jekyll-plugins)

Themes
- <http://jamstackthemes.dev>
- <https://jekyllthemes.org>
- <https://jekyllthemes.io>


## Arbeitsweise

Begünstigt dadurch, dass eine Jekyll Installation nur aus Dateien besteht, 
lassen sich Erstellung und Änderung von Inhalt, 
Konfiguration und Template-Logik mit einen Editor, in meinem Fall dem vim durchführen.
Es gibt auch keinen unötigen Zwischenschritt 
über den Browser zur Bearbeitung und Speicherung von Inhalt mehr.

Darauf aufbauend, 
lassen sich natürlich Text-Dateien wunderbar mit einem VCS verwalten
und das Deployment in die *DocumentRoot* auf Uberspace 
läuft über einen *post-receive git-hook*. 
Das heisst, alle einzelnen Schritte sind über die Konsole möglich.

Diese Arbeitsweise entspricht mehr meiner Gewünschten. 
Ich habe das Gefühl effizienter zu arbeiten 
und kann mich wesentlich mehr auf die eigentliche Arbeit, 
die Erstellung von Inhalt konzentrieren.

## Ein neues Spielzeug


- Importer
- Liquid Template Engine[^liquid]
- Module, Wege, probieren
- Erfolge

## FLOSS

Klar, Jekyll ist mit MIT Lizenz FLOSS.
Und klar, die Lizenz ist wichtig, 
aber ich möchte zudem auf noch etwas anderes hinaus:

Dadurch das Konfiguration sowie *Template Logik* in Code festgehalten,
im Zusammenhang mit der Möglichkeit GitHub Pages mit Jekyll zu betreiben
und der Verbindung von Netlify (Serverless Cloud Hosting) nach GitHub oder GitLab,
bedeutet, das es gibt viele öffentlich verfügbare Repositories auf GitHub und Co gibt.

Das spart Frust und man muss das Rad nicht immer wieder neu erfinden.

# Negatives

Etwas Negatives ist die Zeit, die eine Änderung (Inhalt, Theme, etc) braucht, 
bis diese im Browser sichtbar wird, also Geschwindigkeit.

# To be continued

Ich habe noch 2 verwandte Artikel in *_draft*, die bald folgen werden:

- *Migration von Drupal 6 nach Jekyll*. 
Vorbereitende Schritte, Anpassung des Jekyll Drupal6 Importer und Nacharbeiten.
- *Jekyll Deployment auf Uberspace via Bare Repo und post-receive Hook*.
Uber das Aufsetzen und das *post-receive* Shellskript für ein Deployment auf Uberspace.

---

[^drupal]: [Drupal CMS](https://drupal.org)
[^jekyll]: [Jekyll](https://jekyllrb.com)
[^hacks]: Pressflow Drupal, modifiertes Drush in Symbiose mit dem [MydropWizzard Modul](https://www.drupal.org/project/mydropwizard) für Updates über github statt d.o
[^fn]: [footnotes 8.x port](https://www.drupal.org/sandbox/fl3a/2593257)
[^sbst]: [Jekyll Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
[^geshi]: [GeSHi Filter for syntax highlighting](https://www.drupal.org/project/geshifilter)
[^gist]: [Gist Input Filter (gist_filter) 8.x Port](https://www.drupal.org/sandbox/fl3a/2819998)
[^dir]: [Jekyll: Directory Structure](https://jekyllrb.com/docs/structure/)
[^gems]: [Ruby-Programmierung: Rubygems und Bundler](https://de.wikibooks.org/wiki/Ruby-Programmierung:_Rubygems#Rubygems_und_Bundler)
[^composer]: [Composer](https://getcomposer.org/)
[^md]: [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax)
[^kramdown]: [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html)
[^boot1]: [How Drupal returns a page request](https://befused.com/drupal/page-request)
[^boot2]: [How Drupal handles the page request: Bootstrap Process](https://www.valuebound.com/resources/blog/how-drupal-handles-page-request-bootstrap-process)
[^sa1]: [Drupal core - Highly critical - Remote Code Execution - SA-CORE-2018-002](https://www.drupal.org/SA-CORE-2018-002)
[^sa2]: [Drupalgeddon 2: Angreifer attackieren ungepatchte Drupal-Webseiten](https://www.heise.de/security/meldung/Drupalgeddon-2-Angreifer-attackieren-ungepatchte-Drupal-Webseiten-4024700.html)
[^githubpages]: [Setting up a GitHub Pages site with Jekyll](https://help.github.com/en/articles/setting-up-a-github-pages-site-with-jekyll)
[^liquid]: [Liquid template language](https://shopify.github.io/liquid/)

*[CMS]: Content Management System
*[SSG]: Statischer Seiten Generator
*[LTS]: Long Term Support
*[KISS]: Keep It Stupid Simple
*[GzEvD]: Gesellschaft zur Entwicklung von Dingen mbH
*[d.o]: drupal.org
*[LAMP]: Linux Apache MySQL PHP
*[VCS]: Version Control System
*[DB]: Datenbank
*[FLOSS]: Free/Libre Open Source Software

---
title: "s/Drupal/Jekyll"
tags: 
- Drupal
- Jekyll,
- SSG
- netzaffe
layout: post
---
tl;dr Ich bin vom Drupal CMS Framework[^drupal] auf den Jekyll[^jekyll] SSG umgestiegen.
Darum habe ich das getan und das hat mich an Jekyll überzeugt.
 
Ich betreibe dieses Blog, oder genauer gesagt,
das Stück Software aus dem dieses Blog hervorgegangen ist seit 15 Jahren.
Das waren 15 Jahre mit Drupal, gestartet mit der Version 4.5, 
das hier war auch immer meine Spielwiese um z.B. neue Drupal-Module auzuprobieren.
2009 habe ich das Update auf Drupal 6 gemacht, seit dem Erscheinen von Drupal 8, 
nutze ich den Drupal 6 LTS aus der Community 
(es werden laut Drupal Policy immer nur 2 Versionen unterstützt, 
ergo zu diesen Zeitpunkt Drupal in der Version 7 und v.8.).

Am Ende ist und bleibt es trotz Versorgung mit Updates ein 10 Jahre altes Stück Software
mit einer altertümlichen Anmutung, weit vor der *Ära Mobile* 
und sicherlich auch mit dem ein oder anderen Rudimenten in der Datenbank 
verursacht durch diverse Module, die diese Installation in diesen Jahren erlebt hat.

Da ein Update unabwendbar war, habe ich teils mit dafür gesorgt, 
daß die von mir benötigten Module auch für Drupal 8 zur Verfügung stehen, 
z.B. den Drupal Modulen Footnotes[^fn], GeshiFilter[^geshi] oder Gist Input Filter[^gist].
Unabhängig davon, daß die Migrationen bei mir nicht auf korrekt durchliefen,
hat sich für mich Drupal 8 als zu groß und sperrig angefühlt. 
 
Schon recht lange stand der SSG Jekyll in meinem Backlog (Danke Ben für die Inspiration!), 
im Winter 2018 bin ich dann mal dazu gekommen, Jekyll zu installieren und bin das Step by Step Tutorial[^sbst]  
durchgegangen.

Aber was hat mich an Jekyll so begeistert?<!--break-->

- Drupal 6 Importer
- KISS
   - Einfacher Start
   - Einfache Struktur
   - Textdateien
   - Markdown[^md] [^kramdown]
   - Liquid Template Engine[^liquid]
- Geschwindigkeit 
   - Plain HTML
- Keine Sicherheits-Updates mehr
Beim 2. Drupalgeddon 2[^sa], das hatte ein Risiko-Level[^risk] von 24 bei einer Skala bis 25, 
kam ich mit meiner handvoll Drupal Sites doch etwas ins Schwitzen.
- Nerdy Arbeitsweise
   - Git 
- Ein neues Spielzeug

## Fußnoten & Weiterführendes

*[CMS]: Content Management System
*[SSG]: Static Site Generator

[^drupal]: [Drupal CMS](https://drupal.org)
[^jekyll]: [Jekyll](https://jekyllrb.com)
[^hacks]: Modifiertes Drush, MydropWizzard Modul und Updates über github statt d.o[^do]
[^fn]: [footnotes 8.x port](https://www.drupal.org/sandbox/fl3a/2593257)
[^sbst]: [Jekyll Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
[^geshi]: [GeSHi Filter for syntax highlighting](https://www.drupal.org/project/geshifilter)
[^gist]: [Gist Input Filter (gist_filter) 8.x Port](https://www.drupal.org/sandbox/fl3a/2819998)
[^md]: [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax)
[^sa]: [Drupal core - Highly critical - Remote Code Execution - SA-CORE-2018-002](https://www.drupal.org/SA-CORE-2018-002)
[^kramdown]: [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html)
[^liquid]: [Liquid template language](https://shopify.github.io/liquid/)
*[CMS]: Content Management System
*[SSG]: Statischer Seiten Generator
*[do]: drupal.org
*[LTS]: Long Term Support

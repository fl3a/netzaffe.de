---
tags: []
nid: 1641
permalink: "/installation-und-nutzung-von-drupal-composer-mit-drupal-8"
layout: blog
title: Installation und Nutzung von Drupal-Composer mit Drupal 8
created: 1455825942
---
TLDR: Composer hat sich in der PHP-Welt als Dependency Manager (vergleichbar mit npm aus der Node/JS- oder bundler aus der Ruby-Welt) etabliert und hat schon seit einiger Zeit in die Drupal Welt Einzug erhalten wo die Insel-Lösung drush-make<fn>https://github.com/drush-ops/drush/blob/master/docs/make.md</fn> vorherschte.

So beschäftigt sich dieser Artikel mit Composer<fn>https://getcomposer.org/</fn>, dem Drupal-Composer Projekt-Template<fn>https://github.com/drupal-composer/drupal-project</fn> und Composer als Makefile-Ersatz in Zusammenhang mit Drupal 8.<!--break-->

<h2>Installation von Composer</h2>

Natürlich ist die Installation von Composer die Grundvoraussetzung für Drupal-Composer, hier exemplarisch auf uberspace im bin-Verzeichnis meines Benutzers (<code>--install-dir</code>) und dem Dateinamen composer (<code>--filename</code>, Default <em>composer.phar</em>).

<code>
curl -sS https://getcomposer.org/installer | php -- --install-dir=$HOME/bin --filename=composer 
</code>

<h2>Das Drupal-Composer Template</h2>

Neben dem Composer selbst ist die zweite Zutat das <strong>Composer Template für Drupal-Projekte</strong>,
hierüber ist dann möglich auf drupal.org gehostete Module via Composer zu installieren, das funktioniert über den Drupal Packagist<fn>https://packagist.drupal-composer.org/</fn> als Repository.

Installation einer Drupal-8 Site mit dem Composer-Template im Verzeichnis example.com:
<code>
composer create-project drupal-composer/drupal-project:8.x-dev example.com --stability dev --no-interaction
</code>

<strong>Was macht das Drupal-Composer-Template?</strong>

Neben der Installation von z.B. noch weiterer Vendors wie phpunit oder composer/installers<fn>https://github.com/composer/installers</fn>, welches die Drupal-Pakete direkt ihren passenden  und angedachten Platz läd (s.u.) sorgt es für eine sinnige Struktur und Bereitstellung von Werkzeugen, wie z.B.:

<ul>
<li>Es installiert Drupal in das Verzeichnis web</li>
<li>Drupal-Modules  (Pakete vom Typ drupal-module) werden nach web/modules/contrib/ geladen</li>
<li>Drupal-Themes (Pakete vom Typ drupal-theme) werden nach web/themes/contrib/ geladen</li>
<li>Drupal-installations-Profile (Pakete vom Typ drupal-profile )werden nach web/profiles/contrib/ geladen</li>
<li>Es legt schreibbares Versionen von settings.php und services.yml an</li>
<li>Es legt ein schreibbares sites/default/files Verzeichnis an</li>
<li>Die neuste Version von drush ist installiert und unter vendor/bin/drush verfügbar</li>
<li>Die neuste Version von DrupalConsole ist installiert und unter vendor/bin/console verfügbar</li>
<li><strike>Drupal Packagist</strike><fn>https://packagist.drupal-composer.org/</fn>packages.drupal.org<fn>https://github.com/drupal-composer/drupal-project/commit/49184d678ff0de7f0cda0b597a7b170c6e5261e6</fn> ist als Repository hinterlegt um Drupal-Module, -Themes etc zu verwalten</li>
</ul>
Hier ein Blick in das mit dem Template erzeugte Projekt example.com:
<code>
example.com/
├── composer.json
├── composer.lock
├── drush
├── LICENSE
├── phpunit.xml.dist
├── README.md
├── scripts
├── vendor
│   ├── bin
│   │   ├── drupal -> ../drupal/console/bin/drupal
│   │   ├── drush -> ../drush/drush/drush
│   │   └── [...]
│   ├── drupal
│   │   └── console
│   │       └── bin
│   │          └── drupal
│   └── drush
│       └── drush
│           └── drush
└── web
    ├── core
    │   ├── assets
    │   ├── config
    │   ├── includes
    │   ├── lib
    │   ├── misc
    │   ├── modules
    │   ├── profiles
    │   ├── scripts
    │   ├── tests
    │   └── themes
    ├── modules
    │   └── contrib
    ├── profiles
    │   └── contrib
    ├── sites
    │   └── default
    │       └── files
    └── themes
        └── contrib    
</code>
<small>Abb. 1, Auszug Ausgabe des Befehls "tree" auf das mit Composer-Template erzeugte example.com</small>

<h2>Composer Generate</h2>

Falls ihr eine bestehende Drupal-8-Seite habt, mit der Drush-Erweiterung <em>Composer Generate</em><fn>https://www.drupal.org/project/composer_generate</fn> kann eine <em>composer.json</em> aus aus bereits bestehenden Drupal-Sites erzeugt werden,
die ladet ihr via <code>drush dl composer_generate</code> herunter und führt dann ein <code>drush composer-generate</code> aus der bestehenden Site aus.

<code>
{
    "require": {
        "drupal/big_pipe": "8.1.*",
        "drupal/composer_manager": "8.1.*",
        "drupal/devel": "8.1.*",
        "drupal/drupalmoduleupgrader": "8.1.*",
        "drupal/footnotes": "8.2.*",
        "drupal/geshifilter": "8.1.*",
        "drupal/git_deploy": "8.2.*",
        "drupal/libraries": "8.3.*"
    },
    "minimum-stability": "dev",
    "prefer-stable": true
}
</code>
<small>Abb. 2, Ausgabe drush composer-generate</small>

Die obige Ausgabe, also die verwendeten Pakete vom Type Drupal-Modul könnt ihr dann in der <em>composer.json</em>  in eurem Composer-Template im require-Abschnitt anfügen, 
mit der Ausführung von <code>composer update</code> werden die Pakete heruntergeladen und die Datei <em>composer.lock</em><fn>https://getcomposer.org/doc/01-basic-usage.md#composer-lock-the-lock-file</fn> wird aktualisiert.

<h2>Installation von Drupal-Modulen mit composer</h2> 

Installation von Google Analytics mit exakter Versionsangabe, gewollt ist 8.x-2.0-rc1<fn>https://www.drupal.org/node/2620812</fn>, die Versionsangaben werden in composer allerdings anders notiert<fn>https://getcomposer.org/doc/articles/versions.md</fn>, 8.2.0-rc1<fn>https://packagist.drupal-composer.org/packages/drupal/google_analytics#8.2.0-rc1</fn>.

<code>
composer require drupal/google_analytics:8.2.0-rc1
</code>

<code>
./composer.json has been updated
Loading composer repositories with package information
Updating dependencies (including require-dev)
  - Installing drupal/google_analytics (8.2.0-rc1)
    Downloading: 100%         

Writing lock file
Generating autoload files
</code>


<h2>Drupal Updates mit Composer</h2>

Das Aktualisieren von Drupal und Contribs, bei z.B. anstehenden Sicherheitsupdates auf den Drupal-Kern geht analog zu drush, hier ist ja ebenfalls möglich das Projekt anzugeben (<em>drush up drupal</em>).

Hier der Aufruf für die Aktualisierung des Pakets <em>drupal/core</em>, ohne Spezifizierung des Pakets würden alle Pakete (Contrib, vendor, etc) aktualisiert werden:

<code>
composer update drupal/core
</code>
<code>
Loading composer repositories with package information
Updating dependencies (including require-dev)
  - Removing drupal/core (8.0.3)
  - Installing drupal/core (8.0.4)

Writing lock file
Generating autoload files     
</code>

Ein kleines Bonbon ist, dass an dieser Stelle unser Lock-File die neue Version (8.0.4) für Drupal aktualisiert hat, sprich unser "Make-File" ist nach der Aktualisierung ebenfalls auf dem neusten Stand.

<h2>Patches auf Drupal-Pakete</h2>

Für den Umgang mit Patches auf z.B. Drupal-Pakete ist das Plugin cweagans/composer-patches<fn>https://github.com/cweagans/composer-patches</fn> im Drupal-Composer-Template als Abhängigkeit enthalten und verfügbar. So ist es möglich lokale oder Remote-Patches zu handhaben.

Patches werden in der Sektion <em>extra</em>, <em>patches</em> nach folgendem Schema spezifiziert:

<code>
"extra": {
    "patches": {
        "vendor/project": {
            "Patch description": "URL to patch"
        }
    }
}
</code>
<small>Abb. 3, Schema für Patches</small>

Beispiel, Remote-Patch auf den Drupal-Kern, <em>Remove file lookup in process plugin [d6]</em><fn>https://www.drupal.org/node/2640842</fn>:
<code>
"extra": {
    "patches": {
        "drupal/core": {
            "Remove file lookup in process plugin [d6]": "https://www.drupal.org/files/issues/2640842-8.patch"
        }
    }
}
</code>
<small>Abb. 4, Beispiel Patch auf den Drupal-Kern</small>

Angewendet wird der Patche mit <code>composer update</code> nach dem Ergänzen der composer.json um den Patch in Abb. 4:

<code>
Gathering patches for root package.                                                                                                                           
Removing package drupal/core so that it can be re-installed and re-patched.
Deleting web/core - deleted
Loading composer repositories with package information
Updating dependencies (including require-dev)
Gathering patches for root package.
Gathering patches for dependencies. This might take a minute.
  - Installing drupal/core (8.0.5)
    Loading from cache

  - Applying patches for drupal/core
    https://www.drupal.org/files/issues/2640842-8.patch (Remove file lookup in process plugin [d6])
</code>
<small>Abb. 5, Teil der Ausgabe von composer update mit Drupal-Patch.</small>

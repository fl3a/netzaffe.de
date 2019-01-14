---
tags:
- snippet
- Linux
- Git
- config
nid: 1008
permalink: "/git-gitosis-gitweb-the-debian-way/git-personalisieren.html"
layout: book
title: Git personalisieren
created: 1309284673
---
<h2>Befehl: git config</h2>

<code>
git config --global user.name "Florian Latzel" 
git config --global user.email "floh@netzaffe.de" 
</code>

<h2>Git-Konfigurationsdateien: /etc/gitconfig, ~/.gitconfig, .git/config</h2>
<p>Auswertungsreihenfolge:</p>
<ol>
	<li><code>/etc/gitconfig</code><br>
		Systemweite Git-Konfigurationsdatei</li>
	<li><code>~/.gitconfig</code><br>
		Benutzerweite Git-Konfigurationsdatei</li>
	<li><code>.git/config</code><br>
		Projektspezifische Git-Konfigurationsdatei im jeweiligen Repository</li>
</ol>
<p>Redimentär, nur Name und EMail nach Eingabe des obigen <code>git config</code> Befehls. Die <code>--global</code> Option bewirkt das Schreiben nach <code>~/.gitconfig</code>, ohne diese Option wäre es <code>.git/config</code>. Nach dem abesetzen der beiden <code>git config</code> Befehle hat die Datei <code>~/.gitconfig</code> den folegende Inhalt: 
<code> 
[user] 
     name = Florian Latzel 
     email = floh@netzaffe.de 
</code></p>
<h2>$EDITOR Variable anpassen</h2>
<p>Um z.B. Commit-Messages direkt mit dem gewüschten Editor schreiben zu können, falls man sich die m-Option beim <code>git commit</code> weglässt. <code> export EDITOR='vim' </code></p>
<h2>Git-Branch im Promtersting</h2>
<p>Folgende Funktion für die Anzeige des aktuellen Branches, eingeschlossen in weissen, runden Klammern, zur Plazierung in <code>~/.bashrc</code>. <code> parse_git_branch() { local BRANCH=`git branch 2&gt; /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'` echo -e "\033[m${BRANCH}\033[m" } </code></p>
<h2>Git-Status im Prompterstring</h2>
<p>Die folgende Funktion stellt den Status des Repositories, im Falle von nicht commiteten Dateien bzw. Änderungen wird das <code>±</code> Zeichen in rot, ansonsten in grün angezeigt. Plazierung ebenfalls in <code>~/.bashrc</code>. <code> parse_git_status() { local STATUS=`git status 2&gt;&amp;1` if [[ "$STATUS" != *'Not a git repository'* ]]; then if [[ "$STATUS" == *'working directory clean'* ]]; then echo -e '\033[0;32m±\033[00m' else echo -e '\033[0;31m±\033[00m' fi fi } </code></p>
<h2>Der Angepasste Prompterstring PS1</h2>
<p>Weiter unten in der <code>~/.bashrc</code> die Definition der Variable PS1 im if-Statement eines Debian bzw. Ubuntu Systems, welches greift, wenn <code>force_color_prompt=yes</code> gesetzt ist. <code> PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w $(parse_git_branch)$(parse_git_status)$\[\e[00m\] ' </code> Sieht dann später in einem Git Verzeichnis ohne Farbe so aus: <code> florian@box:~/workspace/drush_multi/drush_multi (master)±$ </code> Siehe auch:</p>
<ul>
	<li><a href="http://kernel.org/pub/software/scm/git/docs/git-config.html">man (1) git-config</a></li>
	<li><a href="http://www.andrewvos.com/2011/07/25/showing-git-status-in-your-bash-prompt">Git Status im BASH Prompt</a></li>
	<li><a href="https://wiki.archlinux.org/index.php/Color_Bash_Prompt">Farbige Prompterstrings</a></li>
</ul>

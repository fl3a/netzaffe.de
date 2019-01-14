---
tags:
- ubuntu
- Linux
- GPS
- Geocaching
- Draussen
nid: 1616
permalink: "/blog/2013/01/14/geocaching-und-garmin-communicator-plugin-unter-ubuntu-linux.html"
layout: blog
title: Geocaching und Garmin Communicator Plugin unter Ubuntu Linux
created: 1358167016
---
Um Geocaches von geocaching.com via Schaltfläche <em>Aufs GPS-Gerät übertragen</em> mit Garmin-Geräten nutzen zu können, ist das <a href="http://software.garmin.com/de-DE/gcp.html">Garmin Communicator-Plug-In</a> nötig, 
welches von Garmin  leider nur für Windows und Mac angeboten wird.

Dank Andreas Diesner gibt es das Plugin auch für Linux!
<!--break-->
<h2>Installation unter Linux</h2>

Nach den folgenden 3 Befehle ist das Garmin Communicator-Plug-In <strong>unter Ubuntu</strong> einsatzbereit:

<code start="1">
sudo add-apt-repository ppa:andreas-diesner/garminplugin
sudo apt-get update
sudo apt-get install garminplugin 
</code>

<strong>Für Debian</strong> gibt es seit November 2012 ein offizielles Paket in Sid, rpm sowie arch sind ebenfalls verfügbar.

<h2>Garmin Communicator Plugin & Google Chrome</h2>

Während das Plugin unter Firefox direkt einsatzbereit ist,
mäkelt Chrome <em>Your browser is not supported by the Garmin Communicator Plug-In.</em> das Plugin an und bietet den Knopf <em>Dieses Mal auführen</em> was leider nichts bringt, da ein Reload des Popup-Fensters erforderlich ist.

Abhilfe schaft unter das Setzen des Häkchens <em>Immer erlaubt</em> unter <code>chrome://plugins/</code> für <strong>Garmin Communicator</strong>.

Mehr:
<ul>
 <li><a href="http://www.andreas-diesner.de/garminplugin/doku.php">Garmin Communicator Plugin for Linux</a></li>
 <li><a href="http://www.andreas-diesner.de/garminplugin/doku.php?id=compiling">Garmin Communicator Plugin selbst komplieren</a></li>
</ul>

---
title: Überprüfung von SSL Zertifikaten bei wget und curl ignorieren
tags:
- wget
- SSL
- Gut zu wissen
- curl
nid: 1636
permalink: "/ueberpruefung-von-ssl-zertifikaten-bei-wget-und-curl-ignorieren"
layout: post
created: 1425213970
---
Oft hat man es mit selbstsignierten SSL-Zerifikaten, also nicht von einem sog. Trusted Issuer beglaubigten SSL-Zertifikaten zu tun, 
das und/oder Hostname und Common-Name im Zertifikat stimmen nicht überein und/oder der Cert ist abgelaufen.

Egal auf welchen Fall man trifft, wget und curl quittieren den Dienst mit einem Exit-Status != 0.

```
wget https://redmine.ociotec.com/attachments/download/302/scrum%20v0.9.1.tar.gz
```

```
--2015-03-01 12:20:08--  https://redmine.ociotec.com/attachments/download/302/scrum%20v0.9.1.tar.gz
Auflösen des Hostnamen »redmine.ociotec.com (redmine.ociotec.com)«... 178.33.112.73
Verbindungsaufbau zu redmine.ociotec.com (redmine.ociotec.com)|178.33.112.73|:443... verbunden.
FEHLER: Dem Zertifikat von »redmine.ociotec.com« wird nicht vertraut.
FEHLER: Das Zertifikat von »redmine.ociotec.com« ist abgelaufen.
Das ausgestellte Zertifikat ist nicht mehr gültig.
Der Zertifikat-Eigentümer paßt nicht zum Hostname »»redmine.ociotec.com««.
```
<!--break-->

Bei wget schaft die Option `--no-check-certificate` Abhilfe.

```
wget https://redmine.ociotec.com/attachments/download/302/scrum%20v0.9.1.tar.gz --no-check-certificate
```

Die Ausgabe unterscheidet sich kaum von der obigen, statt FEHLER wird WARNUNG angezeigt und der Download läuft durch.

Jetzt die gleiche Datei mal mit curl:

```
curl -O  https://redmine.ociotec.com/attachments/download/302/scrum%20v0.9.1.tar.gz
```

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0curl: (60) SSL certificate problem: certificate has expired
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle"
 of Certificate Authority (CA) public keys (CA certs). If the default
 bundle file isn't adequate, you can specify an alternate file
 using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
 the bundle, the certificate verification probably failed due to a
 problem with the certificate (it might be expired, or the name might
 not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
 the -k (or --insecure) option.
```

OK, die Ausgabe von curl ist da ein wenig aufschlussreicher, jetzt mit zusätzlicher `-k` Option: 

```
curl -k -O  https://redmine.ociotec.com/attachments/download/302/scrum%20v0.9.1.tar.gz
```

Im Gegensatz zu wget wird hier auf alles unrelevante in der Ausgabe verzichtet:

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  104k    0  104k    0     0   296k      0 --:--:-- --:--:-- --:--:--  297k
```

So genug gesucht, jetzt halte ich das mal hier fest und hoffe, dass es sich auch durch das Verschriftlichen festigt :D

---
tags:
- Linux
- howto
- config
- gpg
- Datenintegrität
nid: 685
permalink: "/gnupg-micro-howto/konfiguration/konfiguration-des-gpg-agents.html"
layout: book
title: Konfiguration des gpg-agents
created: 1227957277
---
<code>
pinentry-program /usr/bin/pinentry-qt
no-grab
default-cache-ttl 1800

debug-level basic
log-file socket:///home/florian/.gnupg/log-socket
</code>
to be continued.

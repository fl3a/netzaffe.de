---
tags:
- vimrc
- vim
- snippet
- Linux
- config
nid: 587
layout: post
title: vim set pastetoggle
created: 1169454911
---
<p>Um beim Einfügen von mehreren Zeilen aus dem Zwischenspeicher keinen häßlichen Treppeneffekt in vim zu bekommen genügt ein 
<code>
:set paste
</code></p>
<p>Die folgende Zeile in /etc/vim/vimrc oder ~/.vimrc eingetragen verbindet die Taste F9 mit dem <em>Paste-Modus</em> 
<code>
set pastetoggle=<f9>
</code>
</p><!--break-->

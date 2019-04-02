---
tags:
- vimrc
- vim
- snippet
- nützlich
- Linux
- config
nid: 727
layout: post
title: Codefolding für smb.conf in Vim
created: 1240590329
---
<p>Wer kennt das nicht, Freie Software ist für gewöhnlich sehr gut kommentiert, so auch <i>/etc/samba/smb.conf</i>, die Konfigurationsdatei von Samba.</p>
<p>Diese besteht zu über 90% aus Kommentaren...</p>
<p>Um die Direktiven schneller im Blick zu haben, können die folgenden Snippets in <i>~/.vimrc</i> oder <i>/etc/vim/vimrc</i> eingetragen werden, die Kommentare werden gefaltet.</p>

```
let &foldexpr='getline(v:lnum)=~"^.*#"' autocmd FileType samba setlocal foldmethod=expr 
```
<!--break--> 

Oder per Mapping auf F2 

```
map <F2> :let &foldexpr='getline(v:lnum)=~"^.*#"' <CR> 
:set foldmethod=expr
```

<p>Einen Dank an die Entwickler von <a href="http://godot.de">godot</a> für den Tip bei Grillwurst und Bier.<br>
Aus dem Mapping ist die automatische Erkennung entstanden</p>

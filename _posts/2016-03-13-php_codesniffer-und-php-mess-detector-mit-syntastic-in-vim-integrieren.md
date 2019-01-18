---
tags:
- vimrc
- vim
- Linux
- Drupal
- Debian
- Coding Standard
- Code quality
- cleancode
- "<?php ?>"
nid: 1640
permalink: "/php-codesniffer-und-php-mess-detector-mit-syntastic-in-vim-integrieren"
layout: post
title: PHP_CodeSniffer und PHP Mess Detector mit Syntastic in Vim integrieren
created: 1457865294
---
<a href="/sites/netzaffe.de/files/bad-code-php-vim-syntastic.png" rel="lightshow" class="lightbox-processed" title="Abbildung 1, Vim mit Editor Tab und location list.">
<img src="/sites/netzaffe.de/files/bad-code-php-vim-syntastic.png" width=510px" alt="VIM mit Syntastic for PHP  and Drupal development"/>
</a>
<small>Abbildung 1, Vim mit Editor Tab und location list.</small>
Bei der Statischen Code Analyse<fn>https://de.wikipedia.org/wiki/Statische_Code-Analyse</fn> (englisch linting), welche den den White-Box-Test-Verfahren zugeordnet ist wird der Quellcode einer Software auf seine Beschaffenheit überprüft. 
Hierzu gehört z.B. neben dem eigentlichen Linting, in PHP  mit z.B. <code>php -l</code> oder dem Tool <em>phplint</em> die Überprüfung von Coding-Standards<fn>https://de.wikipedia.org/wiki/Programmierstil</fn> oder das Erkennen von potenziellen Problemem bzw. suboptimalen Code wie z.B. ungenutzen Variablen, Properties oder Funktionen, zu hoher Komplexität (z.B. in Zusammenhang mit Wartbarkeit) und die Erkennung möglicher Fehler.  

In der Programmiersprache PHP werden hierfür die Werkzeuge PHP_CodeSniffer<fn>https://pear.php.net/manual/en/package.php.php-codesniffer.php</fn> (squizlabs/PHP_CodeSniffer<fn>https://github.com/squizlabs/PHP_CodeSniffer</fn>) und PHP Mess Detector<fn>http://phpmd.org/about.html</fn> genutzt, welche sich bequem in <acronym title="Integrated Development Envirment">IDE's</acronym> wie PHPStorm integrieren lassen<fn>https://confluence.jetbrains.com/display/PhpStorm/PHP+Code+Quality+Tools</fn>. Aber wie schaut es mit einem scheinbar betagtem und angestaubtem UNIX-Editor wie dem VIM aus?

Natürlich geht das auch im VIM! Wie zeigt dieser Post.<!--break--> 

Als erstes brauchen wie das Syntax-Check-Plugin Syntastic<fn>https://github.com/scrooloose/syntastic</fn> für VIM, welches wir via Paketmanager unserer Distribution (hier Debian) installieren:
<code>
sudo apt-get install vim-syntastic
</code>

Dann brauchen wir noch phpcs, phpmd und phploc, unsere eigentlichen Werkzeuge für die Code-Analyse, die wir über composer installieren:
<code>
composer global require "squizlabs/php_codesniffer=*"
composer global require "phpmd/phpmd"  
composer global require "phploc/phploc" 
</code>

Unsere über composer installierten Tools sollten sich natürlich im Suchpfad für ausführbare Dateien, kurz <em>PATH</em> befinden, hierzu dem Startup-File(<em>~/.bashr</em>, <em>~/.zshrc</em>, usw.) deiner Shell folgendes Statement verpassen:
<code>
export PATH=$PATH:"/home/florian/.composer/vendor/bin"
</code>

Als letztes muss VIM noch konfiguriert werden, hier bearbeiten wir die Datei <em>.vimrc</em> in unserem Home-Verzeichnis mit 
<code>
vi ~/.vimrc
</code>
und fügen die folgenden Zeilen am Ende der Datei hinzu:
<code linenumbers="normal">
" Syntastic
let g:syntastic_aggregate_errors=1
let g:syntastic_sort_aggregate_errors=1
let g:syntastic_id_checkers=1
let g:syntastic_cursor_column=1
let g:syntastic_enable_signs=1
let g:syntastic_always_populate_loc_list=1
let g:syntastic_enable_highlighting=1
let g:syntastic_error_symbol='x'
let g:syntastic_warning_symbol='!'
let g:syntastic_mode='active'
let g:syntastic_php_checkers=1
let g:syntastic_check_on_open=1
let g:syntastic_check_on_wq=1
let g:syntastic_auto_loc_list=1
let g:syntastic_mode_map={
\'mode': 'active',
\'active_filetypes': ['php'],
\'passive_filetypes': []
\}
unlet g:syntastic_php_checkers
let g:syntastic_php_checkers = ["php", "phpcs", "phpmd"]
let g:syntastic_php_phpcs_args='--report=csv --standard=my_standard'

augroup AutoSyntastic
  autocmd!
  autocmd BufWritePost *.php call s:syntastic()
  autocmd BufWritePost *.module call s:syntastic()
  autocmd BufWritePost *.install call s:syntastic()
  autocmd BufWritePost *.profile call s:syntastic()
  autocmd BufWritePost *.inc call s:syntastic()
  autocmd BufWritePost *.test call s:syntastic()
augroup END 
function! s:syntastic()
  SyntasticCheck
endfunction
</code>
<small>Listing 1, ~/.vimrc mit Syntastic Konfiguration für PHP- und Dateinamenserweiterungen für die Drupal-Entwicklung (Z. 28 bis 32)</small>

Die Bedienung gestaltet sich jetzt wie folgt:
Die Editor ist jetzt zweigeteilt, s.o. Abbbildung 1, oben befindet sich das Editor-Tab, hinzugekommen ist das sog.  <em>location list</em> unten:
<code>
  1 UneededHelper.module|7 col 1 error| There must be no blank line following an inline comment [php/phpcs]
  2 UneededHelper.module|15 col 3 error| Whitespace found at end of line [php/phpcs]
  3 UneededHelper.module|16 col 4 warning| @package tag is not allowed in class comment [php/phpcs]
  4 UneededHelper.module|22 error| Avoid unused private fields such as '$foo'. [php/phpmd]
  5 UneededHelper.module|24 col 3 error| Doc comment for parameter \"$bar\" missing [php/phpcs] 
</code>
<small>Listing 2, <em>location list</em> Beispieleinträge</small>

Im Editor-Bereich sind am linken Rand Indikatoren für Fehler und Warnungen, die sog. <em>signs</em> dazugkommen,  bei mir <code>S></code>, entweder Rot hinterlegt für Error oder Gelb für Warning. Mit CRTL und 2xW springt man von Editorfenster in die location list, in der dann mit den Richtungstasten durch die einzelnen Listeneinträge gehen kann, ein ENTER lässt dich dann an die entsprechende Stelle in Code springen. Nach Behebung eines Listeneintrages im Code, und speichen sollte die Liste nun schrumpfen :D

Danke bro für das Teilen dieses Jedi-Vim-Wissens!

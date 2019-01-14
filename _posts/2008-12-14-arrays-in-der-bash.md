---
tags:
- snippet
- Open Source
- nützlich
- Linux
- howto
- Entwicklung
- Arrays
- "#!/bin/bash"
nid: 691
permalink: "/arrays-in-der-bash.html"
layout: blog
title: Arrays in der Bash
created: 1229244988
---
<p>In der <acronym title="Bourne Again SHell">BASH</acronym> ist es möglich mit eindimensionalen Arrays zu arbeiten: 
<code start="1" type="bash">
#!/bin/bash 

declare -a array1 
array1=(zero one two three) 
array1[4]="and four" 
echo ${array1[2]} 
echo ${array1[@]} 
</code> 
In Zeile 3 wird mit <i>declare -a</i> explizit ein Array deklariert.<br>
In Zeile 4 wird mit <i>array1</i> ein Array intitialisiert, der Zugriff auf die Elemente erfolgt über den Index des Array(Zeile 5), welcher wie in den meisten Programmiersprachen von 0 bis Anzahl der Elemente - 1(Zeile 11).<br>
Alternativ kann bei der Initialisierung auch der Index benutzt werden(Zeile 5).</p>
<p>Die Möglichkeit ein assoziatives Array anzulegen, besteht leider nicht.</p>

---
tags:
- snippet
- Drupal
- "<?php ?>"
- drupal-6.x
nid: 858
permalink: "/blog/2009/08/13/block-im-block-bei-drupal.html"
layout: blog
title: Block im Block bei Drupal
created: 1250156083
---
<p>Ähnlich wie <a href="http://www.anelloconsulting.com/drupal_block_within_block">hier</a>, kam auch ich letztens in die Situation einen oder mehrere Blöcke in einem Block anzeigen zu müssen.</p>
<p>Der obige Ansatz hat erst nach hinzufügen eines weiteren Parameters, nähmlich <i>delta</i> funktioniert.</p>
<strong>So kommt man an den Block</strong>
<p>
<code type="php">
$block = module_invoke('module', 'block', 'view', 'delta', 'bid'); 
</code></p>
<!--break-->
<p>Parameter 1, <i>module</i> besagt zu welchem Modul der gewünschte Block zugehörig ist.<br>
Parameter 2, <i>block</i> und 3, <i>view</i> sind in diesem Fall hingegegen fix, da es sich hier ja mit <i>block</i> um Block als Modul dreht und <i>view</i> die Operation ist, die auf den Block angewandt werden soll, siehe auch <a href="http://api.drupal.org/api/function/hook_block">http://api.drupal.org/api/function/hook_block</a>.<br>
	Die Parameter 4,<i>delta</i> und 5, <i>bid</i>, die Block-ID sind wiederrum blockspezifisch, diese werden wie <i>module</i> in der Tabelle <i>blocks</i> festgehalten.</p>
<strong>Zugriff auf den Block</strong>
<p>Die Variable <i>$blocks</i> enthält nun einen assoziativen Array, auf den man über die Keys <i>subject</i> und <i>content</i> zugreifen kann. 
<code type="php"> 
print $block['subject'];
print $block['content'];
</code>
</p>

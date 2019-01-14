---
tags:
- snippet
- jquery
- javascript
- Entwicklung
- Drupal
- Date
- "<?php ?>"
- drupal-6.x
nid: 976
permalink: "/blog/2010/02/20/datepicker-und-drupals-fapi-forms-api.html"
layout: blog
title: Datepicker und Drupal's FAPI (Forms API)
created: 1266665917
---
Bei der Erstellung von Formularelementen,
welche eine Jquery-Datepicker-Funktionalität bereitsstellen sollen 
besteht die Möglickeit auf Date Popup, ein Submodul des <a href="http://drupal.org/project/date" title="Date / Date API Moduls">Date / Date API Moduls</a> zurückzugreifen. 

Der Zugriff auf diese Funktionalität erfolgt über <a href="http://api.drupal.org/api/drupal/developer--topics--forms_api_reference.html" title="Forms API">Drupals FAPI</a>.
<!--break-->
<code>hongomat.info</code> mit Date Popup (date_popup) als Abhängigkeit:

<code>
; $Id$
name = hongomat
description = A hongomatic description
package = example
dependencies[] = date_popup
core = 6.x
</code>

Anlegen eines Datepicker-Elementes (<code>hongomatic_datepicker_element</code>) mit TT.MM.YYYY-Notation, 
der Möglichkeit 0 Jahre in die Vergangenheit und 5 Jahre in die Zukunft zu gehen, vorbelegt mit dem heutigen Datum,
in <code>hongomat.module</code>:
<code language="php">
function hongomat_form(&$form_state) {

  $form = array();

  $form['hongomatic_datepicker_element'] = array(
    '#title' => t('Hongomatic datepicker'),
    '#type' => 'date_popup',
    '#required' =>  TRUE,
    '#date_format' => 'd.m.Y',
    '#date_year_range' => '-0:+5',
    '#default_value' => date('Y-m-d') .' 00:00:00',
  );

  // more form elements [...]

  return $form;
}
</code>

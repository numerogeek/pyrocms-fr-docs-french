# PyroCMS Folder Structure

PyroCMS comporte 4 dossiers root pendant avecle package. Il est important de savoir à quoi ils servent.

## /addons/

Les modules, plugins, widgets et thème que vous ajoutez à PyroCMS vont dans leurs dossiers respectifs : 


1. default (le plus souvent)
2. shared_addons


Depuis que PyroCMS Pro est multisite, même une installation unique possède son propre slug (aussi utilisé comme préfixe dans les noms de tables MySQL). 
PyroCMS Community n'est  _pas_ multi-site, et possède un identifiant unique. L'identifiant par défaut est **default**, c'est pourquoi PyroCMS crée un dossier **default** dans le dossier addons.

**PyroCMS Community Edition users:** put your add-ons in either folder - PyroCMS will look in both.

**PyroCMS Pro users:** all add-ons you wish to be available to all sites go in your shared_addons folder. Add-ons that only belong to specific sites can go in their respective folder (matching the site slug) created on installation of the site.

## /assets/

To optimise site performance. 

## /system/

The system folder contains two main things: a copy of CodeIgniter (the PHP framework that PyroCMS runs on) and PyroCMS itself. You will most likely never have to go inside this folder, but there are two files you should know:

### /system/cms/config/database.php

When PyroCMS installs, it will create this file for you with your MySQL login data. However, if you want to change this data or add another {{ link uri="general/getting-started/environments" title="environment" }}, you'll need to edit this file.

### /system/cms/config/config.php

The CodeIgniter application config file has a whole lot of items you'll never need to touch. In fact, PyroCMS automatically sets your base url so you may never need to look at this file and be fine!

However, if you began without mod_rewriting URLs (i.e. with index.php still in them), and you want to {{ link uri="general/getting-started/removing-indexphp-from-urls" title="remove index.php from links" }} later on, you can remove that easily by finding:

	$config['index_page'] = 'index.php';

and changing it to:

	$config['index_page'] = '';

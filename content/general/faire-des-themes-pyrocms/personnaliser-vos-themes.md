# Personnaliser vos thèmes

PyroCMS supporte les thèmes et vous permet de les modifier facilement.
Le thème se base sur un fichier MASTER LAYOUT sur plusieurs PARTIALS LAYOUTS qui partage la logique entre les différents layouts.

## Créer un theme

Comme les modules, les thèmes sont localisés à 3 endroits : <dfn>addons/shared_addons/themes (pour les thèmes disponibles pour tous les sites) &amp;</dfn><dfn> addons/&lt;site-name&gt;/themes (pour les thèmes spécifiques à un site),&nbsp;</dfn><dfn> system/pyrocms/themes (pour le thème par defaut).</dfn>

Lorsque vous créez un thème, il est bienvenue de jeter un coup d'oeil au thème par défaut et de regarder comment ça fonctionne. Vous devriez le copier et partir de ça comme base pour votre propre thème.

Le thème par defaut est un &quot;core theme&quot; qui est situé <dfn>system/pyrocms/themes/default</dfn>.
Copiez le dans <dfn>addons/</dfn><dfn>shared_addons/</dfn><dfn>themes/custom</dfn> ou un nom qui vous convient.
Si vous modifiez le nom du thème, vous devrez renommer le nom de la classe dans theme.php pour qui corresponde au nom du dossier.

## Les dossiers.

* css
* img
* js
* views
* views/layouts
* views/partials
* views/modules

## theme.php

Chaque thème possède ses propres informations. Auteur, version, siteweb etc.. Ce fichier est situé à la racine du thème :
     addons/shared_addons/themes/my-theme-name/theme.php

ou

     addons/<site-ref>/themes/my-theme-name/theme.php
	 
Pas d'experience particulière est requise pour éditer ce fichier, rappelez vous simplement de changer la dernière partie du &quot;Theme\_Custom&quot; pour que ça corresponde à votre nom de dossier.

Ca doit toujours commencer par &quot;Theme\_&quot; et le nom du dossier avec la première lettre en lettre MAJUSCULE.

Dans la section Theme Options le tableau &quot;public $options&quot; est optionnel. Si vous ne souhaitez pas d'option, supprimez le tableau.

	<?php defined('BASEPATH') OR exit('No direct script access allowed');
	class Theme_Custom extends Theme
	{
	    public $name            = 'My Theme';
	    public $author          = 'John Smith';
	    public $author_website  = 'http://example.com';
	    public $website         = 'http://example.com/themes/mytheme';
	    public $description     = 'An awesome theme in blue and green with two columns and stuff.';
	    public $version         = '1.0';
	
	    public $options         =  array(
	        'show_breadcrumbs' =>   array('title'         => 'Show Breadcrumbs',
	                                      'description'   => 'Would you like to display breadcrumbs?',
	                                      'default'       => 'yes',
	                                      'type'          => 'radio',
	                                      'options'       => 'yes=Yes|no=No',
	                                      'is_required'   => TRUE),
	        'layout' =>             array('title'         => 'Layout',
	                                      'description'   => 'Which type of layout shall we use?',
	                                      'default'       => '2 column',
	                                      'type'          => 'select',
	                                      'options'       => '2 column=Two Column|full-width=Full Width',
	                                      'is_required'   => TRUE),
	     );
	
	 }
	/* End of file theme.php */

## Options du thème

Cette fonction est optionnelle et n'est pas necessaire pour des thèmes simples. Cela peut s'averer plus utile pour les thème un peu complexe.

Les options ici sont accessible dans l'interface d'administration via Design / themes / options.
Si vous créez un thème et ajoutez une nouvelle option au theme/php, cliquez sur le bouton "Re-index" dans la fenetre Options.
Cela va recharger les dernières options de votre theme.php dans la base de données.

Les types disponibles sont :

* radio
* checkbox
* select
* select-multiple
* text
* textarea
* password

Si nous devions utiliser les tags dans notre exemple, ça ressemblerait à : 

    {{ noparse }}{{ theme:options option="layout" }}{{ /noparse }}

Et le resultat serait  &quot;2 column&quot; or &quot;full-width&quot; 

###screenshot.png

Pour avoir une preview de votre theme de l'interface d'admin, vous devez créer un screeshot.png et le placer dans le dossier de votre thème.
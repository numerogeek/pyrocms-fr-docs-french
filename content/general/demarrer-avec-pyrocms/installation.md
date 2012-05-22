# Installation

La première étape pour bien commencer avec PyroCMS est de le télécharger et de l'installer sur votre serveur. 

## Télécharger manuellement PyroCMS


Vous pouvez télécharger la dernière version de PyroCMS  <a href="http://github.com/pyrocms/pyrocms/zipball/v{{ variables:current_version }}">ici</a>. Décompresser les fichiers du zip et copiez les sur votre serveur ou votre environnement de développement. 
 
## Télécharger PyroCMS avec Git

Si vous utilisez [git](http://git-scm.com/), vous pouvez prendre la dernière version de PyroCMS sur le [GitHub repo](https://github.com/pyrocms/pyrocms).  utilisez la bonne branche - {{ link title="Le guide des versions PyroCMS" uri="/general/a-propos/pyrocms-versions" }} explique la différence.

## Installer PyroCMS


Après avoir mis les fichiers à la bonne place, chargez PyroCMS dans votre navigateur et l'installeur devrait apparaitre.
Cette vidéo vous montre tout le processus et ne prends que quelques minutes.

<iframe src="http://player.vimeo.com/video/33693492?title=0&amp;byline=0&amp;portrait=0&amp;color=ff9933" width="700" height="360" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>  
  
 L'installeur va vour montrer toutes les étapes nécéssaire pour installer PyroCMS, et vérifier les éléments requis sur votre serveur.
 Vérifiez la 
{{ link title="pages des requis" uri="/general/demarrer-avec-pyrocms/prerequis-serveur" }} pour le détail de ce dont vous avez besoin.

### Supprimez l'Installeur


Après avoir installé avec succès PyroCMS, il est très important de supprimer le répertoire d'installation de votre installation PyroCMS. Vous n'avez plus besoin de ces fichiers. Le garder serait un problème de sécurité.

### Supprimer la vérification de l'Installer dans index.php

Ce n'est pas nécessaire, mais une fois que vous avez installé PyroCMS, vous pouvez ouvrir votre index.php et supprimerla partie Installation dans le début du fichier. Le bloc de code doit ressembler à ceci:

     # si vous avez déja installé, supprimez ça :
     if ( ! file_exists('system/cms/config/database.php'))
    {
	// Make sure we've not already tried this
	if (strpos($_SERVER['REQUEST_URI'], 'installer/'))
	{
		header('Status: 404');
		exit('PyroCMS is missing system/cms/config/database.php and cannot find installer.');
	}
	
	// Otherwise go to installer
	header('Location: '.rtrim($_SERVER['REQUEST_URI'], '/').'/installer/');
	exit;
    }

Cela n'affecte pas la fonctionnalité PyroCMS (sauf si vous n'avez pas un fichier database.php), mais il supprime une vérification du fichier inutile.
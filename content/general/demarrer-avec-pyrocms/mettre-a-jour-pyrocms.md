# Mettre &agrave; jour votre version PyroCMS 2.x

PyroCMS est en developpement actif, cela signifie qu'il est souvent mis &agrave; jour avec de nouvelles fonctionnalit&eacute;s ou des corrections de bugs.

Vous pouvez suivre le [blog](http://www.pyrocms.fr/blog) ou le [fil Twitter](http://www.twitter.com/pyrocms_france) pour être au courant des nouvelles versions.

Mettre &agrave; jour PyroCMS est rapide et simple, suivez le guide !

## T&eacute;l&eacute;chargez la derni&egrave;re copie de PyroCMS

Vous pouvez t&eacute;l&eacute;charger la derni&egrave;re version de PyroCMS 2.x [ici](https://github.com/pyrocms/pyrocms).


## Sauvegardez le dossier Addons et database.php


Nous allons remplacer l'ensemble du syst&egrave;me, vous aurez donc besoin de sauvegarder les fichiers que vous avez modifi&eacute;s. Tr&egrave;s probablement, ce n'est que le fichier database.php, qui est stock&eacute; dans le system / cms / config / database.php et contient vos informations de connexion de base de donn&eacute;es.

Si vous utilisez une interface graphique, prenez soin de ne pas oublier les fichiers "cach&eacute;s" comme. Htaccess lors de la copie.

En outre, vous devrez sauvegarder tous les addons que vous avez ajout&eacute;s dans le r&eacute;pertoire addons. Nous allons remplacer l'ensemble du dossier.


## Replacer les dossier addons et system

Replacez les dossier addons et system avec les nouvelles versions, et remettez ensuite votre repertoire addons et le fichier database.php

## Replacer index.php avec la nouvelle version.

Ca arrive rarement, mais occasionnelement, il peut y avoir des changements dans le fichier index.php, donc soyez assurer que vous avez la derni&egrave;re version &agrave; jour.

### Assurez vous de rendre ces fichiers accessible en &eacute;criture:

* system/cms/logs
* system/cms/cache
* system/cms/cache/simplepie
* system/cms/config
* uploads

## Profitez  !

C'est tout, tous les changements en base seront automatiquement appliqu&eacute;s (par "migrations") la prochaine fois que vous vous connecterez &agrave; l'interface d'administration. Vous avez maintenant la derni&egrave;re version de PyroCMS.
 

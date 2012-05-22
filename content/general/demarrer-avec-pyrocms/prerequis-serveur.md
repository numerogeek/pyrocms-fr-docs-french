# Prerequis Serveur

Voici les exigences pour l'exécution du serveur PyroCMS 2.0. Si vous n'êtes pas sûr si vous avez tout cela, PyroCMS va vérifier pour vous votre configuration lors de l'installation.

### un serveur HTTP

Apache 2.x, Abyss Web Server, uniforme, Zend Server Community, etc Jusqu'ici PyroCMS ne semble lutter qu'avec IIS.

### MySQL 5.x ou plus elevé

Il y a des plan pour d'autres base de données, mais pour l'instant seul mysql est supporté.

### PHP 5.2.x ou plus elevé

PHP 5.2 et PHP 5.3 sont tout les deux supportés.
 
### GD 2

Cette bibliothèque doit être installé sur votre serveur avec PHP compilé.  Habituellement, votre gestionnaire de paquets se charge de cela pour vous, sinon vous pouvez l'obtenir <a href = "https://bitbucket.org/pierrejoye/gd-libgd/overview" target = "_blank" title = "Découvrez comment pour faire le travail GD2 avec PHP "> ici </ a> (le wiki libgd est actuellement indisponible.)

### cURL

<a href="http://curl.haxx.se/" target="_blank">libcurl 7.10.5 or greater</a> doit être installé sur votre serveur avec PHP compilé. Habituellement, votre gestionnaire de paquets se charge de cela pour vous, sinon vous pouvez l'obtenir <a href="http://curl.haxx.se/libcurl/php/install.html" target="_blank" title="Découvrez comment faire fonctionner cURL avec PHP">here</a>.

### Bundled requirements

PyroCMS utilise ces logiciels tiers afin de fonctionner, mais les inclut dans chaque version de sorte que vous n'avez pas besoin d'installer vous-même:

* <a href="http://codeigniter.com/" target="_blank">CodeIgniter 2.1.x</a>
* <a href="http://jquery.com/" target="_blank">jQuery 1.6.x</a>
* <a href="http://github.com/happyninjas/lex" target="_blank">Lex</a>

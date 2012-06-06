# Environnements

Les développeurs souhaitent disposer de comportements spécifiques en fonction de leurs besoins ou si leur application fonctionne dans un environnement de développement ou de production.
Par exemple, l'affichage des différents messages d'erreur sont important pendant le cycle de développement, ces "informations confidentielles" ne doivent pas s'afficher lorsque le site est en "production" car elle peuvent entrainer des risques de sécurité.

## La constante ENVIRONMENT

Par défaut, PyroCMS est paramétrée avec la constante ENVIRONMENT définie à 'development'. Dans les permières lignes du fichier index.php, vous trouverez:

	define('PYRO_DEVELOPMENT', 'development');
	define('PYRO_STAGING', 'staging');
	define('PYRO_PRODUCTION', 'production');

	define('ENVIRONMENT', (isset($_SERVER['PYRO_ENV']) ? $_SERVER['PYRO_ENV'] : PYRO_DEVELOPMENT));

En plus de donner des comportements spécifiques fonction de l'environnement (voir section suivante), vous pouvez utiliser cette constante pour voir les différences entre les différents environnements que vous utilisez.

## Effets sur le comportement par défaut du Framework

Dans certaines parties du système PyroCMS, la constante <kbd>ENVIRONMENT</kbd> est utilisée. Cette section décrit la façon dont le framework par défaut se comporte.

### Report d'erreurs

Définir la constante <kbd>ENVIRONMENT</kbd> à la valeur `'development'` entrainera l'affichage de l'ensemble des Erreurs PHP lorsqu'elles ont lieu. Passer la valeur de cette constante à `'production'` désactivera l'affichage de l'ensembles des erreurs. Désactiver l'affichage des erreurs PHP lorsqu'on est en production est une bonne pratique.

### Fichiers de configuration

Optionnellement, PyroCMS vous permet de charger des fichiers de configuration spécifiques à un environnement. Ceci peut être utile, par exemple pour gérer des clés API en fonction de l'environnement. Cette partie est décrite de manière détaillée dans la partie Environnements de la section [CodeIgniter Config Class](http://codeigniter.com/user_guide/libraries/config.html#environments).

## Paramétrer $\_SERVER['PYRO\_ENV']

Vous pouvez faire cela simplement si vous utilisez une interface du type PagodaBox ou PHP Fog, ceci peut être plus complexe pour les autres types d'environnement.
Apache supporte la variable setEnv via [mod\_env](http://httpd.apache.org/docs/2.2/mod/mod_env.html), ceci peut être fait via votre fichier principal de configuration Apache ou plus simplement en éditant le fichier .htaccess situé à la racine du site, il suffit de supprimer le **`#`** de cette ligne&nbsp;:

	SetEnv PYRO_ENV production
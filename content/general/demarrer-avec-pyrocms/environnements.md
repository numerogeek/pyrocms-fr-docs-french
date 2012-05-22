# Environnements

Si vous avez déjà utilisé le même code source pour deux environnements différents, vous savez que le passage entre les deux peut être douloureux. Heureusement, PyroCMS a un support intégré pour les environnements multiples

## Automatic Base URL

PyroCMS devine votre URL racine. Cela signifie que vous pouvez lancer le même code sur votre ordinateur local ainsi que votre serveur de production et de ne jamais avoir à changer l'URL.

si vous trouvez que PyroCMS rencontre des difficultés, vous pouvez la modifier manuellement dans **system/cms/config/config.php** en modifiant le **base_url**;

     $config['base_url']	= '';

## Environnements de bases de données multiples

PyroCMS peut également choisir la base de données en fonction de votre environnement. Disons que vous avez deux bases de données - un sur votre machine locale pour le développement, et l'autre sur votre serveur de production. Vous pouvez entrer à la fois les détails de connexion dans le  fichier **system/cms/config/database.php** . Les environnements possibles sont 

* Development
* Staging
* Production

Vous verrez un tableau de configuration de la connexion de base de données pour chacun des environnements:

     // Development
     $db[PYRO_DEVELOPMENT] = array(
	'hostname'		=> 	'localhost',
	'username'		=> 	'root',
	'password'		=> 	'',
	'database'		=> 	'pyrocms',
	'dbdriver' 		=> 	'mysql',
	'dbprefix' 		=>	'',
	'active_r' 		=>	TRUE,
	'pconnect' 		=>	TRUE,
	'db_debug' 		=>	TRUE,
	'cache_on' 		=>	FALSE,
	'char_set' 		=>	'utf8',
	'dbcollat' 		=>	'utf8_unicode_ci',
	'port' 	 		=>	3306,

	// 'Tough love': Forces strict mode to test your app for best compatibility
	'stricton' 		=> TRUE,
     );

Vous pouvez parametrer PyroCMS et lui dire quel environnement il doit charger en settant la variable PYRO_ENV (pas dispo sur tous les serveurs, renseignez vous chez votre hebergeur.

     SetEnv PYRO_ENV production

Une fois que vous avez fait cela, vous aurez besoin de faire attention à ne pas copier votre fichier .htaccess sur votre serveur de développement par erreur (ou vice-versa). Si vous utilisez
git, vous pouvez éviter cela avec. gitignore, tel que décrit ci-dessous.


Si vous utilisez Nginx et php-fpm, vous pouvez ajouter PYRO_ENV au fichier de config Nginx comme décrit ici :

     fastcgi_param PYRO_ENV production;

Ceci définit une variable appelée **PYRO_ENV** qui sera lue par PyroCMS et utilisée pour charger la base de données adaptée à l'environnement actuel.

Vos choix pour les valeurs de **PYRO_ENV** sont:

* development
* staging
* production

Chacun de ces parametres correspond à un une base de données dans votre fichier de configuration database.php.

<div class="tip"><strong>Tip:</strong> If you are versioning your PyroCMS site with git, once you have PyroCMS set up for multiple environments, keep your database.php under version control since you will no longer need separate database.php files for development, staging, and production.</div>

Si vous versionnez votre site PyroCMS avec git, une fois que vous avez mis en place PyroCMS sur des environnements multiples, gardez votre database.php hors des contrôles de version, puisque vous n'aurez plus besoin de fichiers database.php distincts pour le développement, le staging, et la production.

### Verifier les environnements dans les layouts

Si vous souhaitez vérifier conditionnellement l'environnement dans votre mise en page PyroCMS, vous pouvez le faire avec le tag **global:environment**:

	{{ noparse }}{{ if global:environment == 'production' }}
	
	// Production-only content
	
{{ endif }}{{ /noparse }}

## Ignorer des dossiers avec Git:

Si vous avez votre projet avec PyroCMS sur git, vous pouvez ignorer les fichiers que vous ne devez pas partager entre les environnements en créant un <strong>. Gitignore </strong>. Ajoutez les fichiers et dossiers que vous voulez ignorer. Voici un bon début pour un gitignore sur PyroCMS .:


    system/cms/cache/
    system/cms/logs/
    .htaccess
    uploads/

<div class="tip"><strong>Note:</strong> Dans certains cas, vous voudrez peut-être de garder votre dossier upload sous contrôle de version. Ce n'est qu'une suggestion pour les éléments ignorés.</div>

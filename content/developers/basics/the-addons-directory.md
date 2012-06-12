# Le dossier Addons

Le dossier **/addons** est la destination de tout vos codes personnalisés il équivaut au dossier  **"Application Package"** de CodeIgniter. L'objectif de ce dossier est de contenir l'ensemble des développements tiers comme les modules, widgets ou plugins. Il peut être utilisé pour mutualiser des configurations, librairies, helpers et fichiers de langues commun à vos différents développements.

Ci-dessous la liste complète des dossiers que vous pouvez ajout dans le dossier **/addons**&nbsp;:

* config/
* helpers/
* language/
* libraries/
* models/
* modules/
* plugins/
* themes/
* widgets/

All of your custom code should fit into one of those folders and should be developed in the same way as you normally would in a CodeIgniter application.

Un point important à noter cependant, vous ne pouvez pas étendre les helpers ou librairies situées dans le dossier ** system/** (ni system/cms ni system/codeigniter). ceci est du au fonctionnement de la classe <a href="http://codeigniter.com/user_guide/libraries/loader.html" target="_blank">CodeIgniter Loader class</a> qui ne sait pas chercher dans ce dossier est considéré comme une "limitation" de CodeIgniter. Si vous avez besoin d'étendre des fichiers core, vous devez tracker les modifications sur ces fichiers à l'aide de Git, sinon vous pouvez perdre vos modifications si vous faites une mise à jour de PyroCMS.

De la même façon, il y a des limites concernant les fichiers de configuration. Les fichiers de configuration comme autoload.php, database.php ou routes.php n'auront aucun effet ici. Il est recommandé de déposer uniquement vos propres fichiers de configurations qui seront chargés et utilisés dans vos développements spécifiques.
 
Vous pouvez utiliser le dossier **addons/shared\_addons/** exactement comme le dossier **addons/**. La seule différence est que quand vous téléchargez un module ou un thème à partir du panneau d'administration, il sera placé dans le dossier **addons/default/**. Si vous faites une mise à jour vers la version professionnelle de PyroCMS certains thèmes, modules ou widgets seront confinés à un seul site seulement. Si vous faites la mise à jour, les extensions que vous ajoutez seront plaçés dans leurs propres dossier (**addons/__site\_name__**).
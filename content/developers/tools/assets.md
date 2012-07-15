# Ressources CSS et JS (Asset)

La gestion des ressources CSS et JS est pris en charge par la librairie PHP Asset écrite par Antony Male. Cette librairie, facile à utiliser, vous permet d'utiliser les fonctionnalités suivantes:

- Spécifier quelles ressources utiliser pour une page particulière dans votre vue/contrôleur, et les inscrire dans vos templates.
- Regrouper les assets en groupes soit de façon pré-définie soit générés à la volée
- Activer/Désactiver des groupes spécifiques de vos vues/contrôleurs
- Minifier des groupes et les combiner des des fichiers singuliers afin de réduire et minimiser les requêtes serveurs
- Définir vos JS/CSS dans votre vue/contrôleur pour être inclus dans vos templates.
- Utiliser les espaces de noms pour vos ressources

Utilisation de base
-----------

Les fichiers JS et CSS sont pris en charge de la même manière, considérons l'exemple suivant pour les JS (Il suffit de substituer 'js' par 'css' pour les fonctions relatives aux css).

Les fichiers Javascript peuvent être ajoutés en utilisant **monfichier.js** et **monfichier2.js** qui sont les fichiers JS que vous souhaitez utiliser, et sont situés dans **assets/js/monfichier.js** and **assets/js/monfichier2.js** (configurable).

	Asset::js('monfichier.js');
	Asset::js('monfichier2.js');

Par défaut, la librairie minifiera ces deux fichiers en les combinant dans un fichier unique (qui sera écrit dans **assets/cache/&lt;md5 hash&gt;.js**).
Pour inclure ce fichier dans votre page, vous pouvez écrire:

	echo Asset::render_js();

Cela vous retourne quelque chose comme

	<script type="text/javascript" src="http://localhost/assets/cache/d148a723c710760bc62ca3ecc8c50206.js?1307384477"></script>

Si la minification est désactivée (voir section dans ce document), vous aurez alors :

	<script type="text/javascript" src="http://localhost/site/assets/js/monfichier.js"></script>
	<script type="text/javascript" src="http://localhost/site/assets/js/monfichier2.js"></script>

Si vous avez un fichier spécifique **monfichier.min.js** que vous souhaitez que la libraire Asset utilise plutôt que de générer ces propres versions minifiées, vous 
pouvez ajouter ce second argument:

	Asset::js('monfichier.js', 'monfichier.min.js');

Pour pouvoir traiter les fichiers css et js vous pouvez:  

**Asset::render()** est un raccourci qui permet d'appeler **Asset::render_css()** et **Asset::render_js()**.

Images
------

Although the original Asset library provided groups, etc, for dealing with images, I couldn't see the point.

La prise en charge des images est simple, et peut être résumé par la ligne suivante, le troisième argument est optionnel et permet de passer un tableau d'attributs:

	echo Asset::img('test.jpg', 'texte alternatif', array('width' => 200));

Vous pouvez également passer un tableau d'images (qui ont tous des attributs qui leurs sont appliqués):

	echo Asset::img(array('test.jpg', 'test2.jpg'), 'Some thumbnails');

Cette fonctionnalité devient puissante quand vous considérez les namespacing, détaillé plus loin dans ce document.


Groupes
------

Les groupes sont une collection de fichiers js/css.
Un groupe peut être défini dans un fichier de configuration ou à la volée. Ils peuvent être activés et désactivés individuellements, et générés individuellement.

Les CSS et les JS ont leurs propre espace de nom, vous pouvez donc les surcharger.

Les groupes spécifiques peuvent être affichés en utilisant
	
	Asset::render_js('nom_groupe')

Si aucun nom de groupe n'est passé en argument, **tout** les groupes seront générés (**all** groups).

<div class="tip"><strong>Note:</strong> Quand un groupe est généré, il est désactivé. Voir la section "Extra attributes" pour voir une application de ce fonctionnement.</div>

Les fichiers peuvent être ajoutés à un groupe en passant le nom du groupe en troisième argument à **Asset::js** ou **Asset::css**, respectivement:

	Asset::js('monfichier.js', 'monfichier.min.js', 'nom_groupe');
	Asset::css('monfichier.css', false, 'nom_groupe');

<div class="tip"><strong>Note:</strong>Vous pouvez également passer une valeur non-string à la place de 'false' dans le second exemple, Asset se comportera de la même façon: il génèrera et mifiniera le fichier pour vous.</div>

Si le nom de groupe n'existe pas, le groupe est créé et activé.

Vous pouvez également ajouter des groupes à la volée en utilisant **Asset::add\_group($group\_type, $group\_name, $files, $options)**, ou **$options** est un tableau avec **aucune** des clés suivantes:

	$options = array(
		'enabled' => true/false,
		'min' => true/false,
		'combine' => true/false,
		'inline' => true/false,
		'attr' => array(),
		'deps' => array(),
	);

Cette méthode est fournie uniquement pour permettre d'ajouter de nombreux fichiers à un groupe en une seule fois.
Vous n'avez pas besoin de créer un groupe avant d'ajouter des fichiers dedans - le groupe sera créé si il n'existe pas.

Vous pouvez changer n'importe laquelle de ces options à la volée en faisant 

	Asset::set_group_option($type, $group, $key, $value)
	
ou des versions spécifiques de fichiers CSS et JS

	Asset::set_js_option($group, $key, $value)
	Asset::set_css_option($group, $key, $value)
	
**$group** comporte des valeurs spéciales: une chaine de caractère vide correspond à un raccourci au groupe 'global' (groupe auquel les fichiers sont ajoutés si aucun groupe n'est spécifié) et '\*' est un raccourci pour tout les groupes.

Des noms de groupes multiples peuvent également être spécifiés en utilisant un tableau.

Exemples :
	
	// Ajouter un dep à mon groupe my_plugin
	Asset::set_js_option('my_plugin', 'deps', 'jquery');

	// Permet que tout les fichiers ajoutés à la page courante utilisant la méthode Asset::add_css() s'afiche en ligne (display inline):
	Asset::set_css_option('', 'inline', true);

	// Désactive la minification pour tout les groupes,  quelque soit les paramaètres per-group, pour la page courante:
	Asset::set_js_option('*', 'min', false);

Lorsque vous appelez la méthode **Asset::render()**  (ou les variantes spécifiques js et css), l'ordre des groupes générés est déterminé par l'ordre dans lequel ils ont été créés, avec les groupes présents dans le fichiers de configuration apparaissant en premier.

Similairement (pour les fichiers JS seulement), l'ordre dans lequel les fichiers vont apparaître va déterminer l'ordre dans lequel ils vont être ajoutés.

Ceci vous permet un degré de contrôle supplémentaire pour contrôler l'ordre d'inclusion des fichier dans votre page, ce qui peut être nécessaire pour satisfaire certaines dépendances.

Si ceci ne fonctionne pas pour vous, ou que vous voulez quelque chose de plus explicite, essayez ceci : Si un fichier A dépend de B, ajouter B à son propre groupe et traitez le en premier.

<div class="tip"><strong>NOTE:</strong> Appeler <strong>Asset::js('fichier.js')</strong> ajoutera ce fichier au groupe "global". Utilisez ceci autant que vous pouvez!</div>

<div class="tip"><strong>NOTE:</strong> Les arguments pour <strong>Asset::add_group</strong> sont différents. Les rétro-compatbilités sont assurées pour le moment, mais nous vous encourageons à utiliser la nouvelle syntaxe.</div>

Chemins et espaces de noms
---------------------

La librairie Asset effectue une recherche parmi tout les éléments jusqu'à ce qu'il trouve un premier fichier correspondant.
Cette approche n'est pas souhaitable, car elle signifie que si vous avez la structure de répertoires ci-dessous, et que vous essayez d'inclure 'index.js', le fichier que sera inclu sera déterminé par l'ordre des dossiers.

	themes/
		theme_name/
			css/
			js/
				index.js
		  img/

La librairie Asset permet par l'intermédiaire des espaces de noms de résoudre ce problème. Vous pouvez spécifier le code suivant dans votre fichier de configuration:

	'paths' => array(
		'core' => 'assets/',
		'admin' => 'assets/admin/',
	),

Vous pouvez également ajouter des chemins à la volée en utilisant **Asset::add\_path($key, $path)**:

	Asset::add_path('admin', 'assets/admin/');

Le répertoire à utiliser est déterminé en préfixant le fichier ressource avec la clé du chemin à utiliser. Notez que si vous oubliez le chemin clé, le chemin par défaut est utilisé (initialement 'core').


	Asset::js('index.js');
	// où
	Asset::js('module::index.js');
	// Permet d'ajouter assets/js/index.js

	Asset::js('admin::index.js');
	// Permet d'ajouter assets/admin/js/index.js

	echo Asset::img('test.png', 'Une image');
	// <img src="...assets/img/test.png" alt="Une image" />

	echo Asset::img('admin::test.png', 'Une image');
	// <img src="...assets/admin/img/test.png" alt="Une image" />

Si vous le souhaitez, vous pouvez changer la clé du chemin par défaut en utilisant **Asset::set\_path('path_key')**. Ceci peut-être pratique si par exemple toutes les ressources pour un fichier donnée proviennent d'un chemin donné. Par exemple:

	Asset::set_path('admin');
	Asset::js('index.js');
	// Permet d'ajouter assets/admin/js/index.js

le chemin "core" peut être restoré en appelant la fonction **Asset::set\_path()** et en ne passant aucun argument (vous pouvez également appeler **Asset::set\_path('core')**).

De la même manière, Vous pouvez également utiliser un espace de nom pour les fichiers listés dans le fichier de configuration 'groups'.
Note que ceux-ci sont chargé avant l'espace de nom soit changé de 'core' à une autre valeur, les fichiers n'étant pas dans l'espace de nom core devrons être explicitement prefixés avec le nom de l'espace de nom.

En outre, vous pouvez surcharger les options de configuration **js\_path**, **css\_path** et **img_path** sur la base d'un nom de chemin.
 Dans ce cas, le tableau comprenant les options de configuration **paths**  prends la forme suivante les options **js\_path**, **css\_path** et 
**img\_path** sont optionnelles. Si elles ne sont pas spécifiées, les valeurs par défaut seront utilisées.

	array (
		'une_cle' => array(
			'path' => 'plus_de_librairies/',
			'js_dir' => 'javascript/',
			'css_dir' => 'styles/',
			'img_dir' => 'images/',
			),
		),
	),

Ceci est particulièrement utile quand vous utilisez des modules personnalisés (addons), Et que vous n'avez pas de contrôle sur l'emplacement des librairies.

Noter également que vous pouvez ajouter une ressource dont le chemin n'est pas encore défini.
Les ressources requièrent uniquement que le chemin soit défini au moment ou le fichier est utilisé. 


Globbing
--------

Comme pour les nom de fichiers, vous pouvez spécifier le [masque glob pattern](http://php.net/glob), 
ceci retournera un tableau contenant les fichiers et dossiers correpondant au masque recherché

Par exemple:

	Asset::css('*.css');
	// Exécute glob('assets/css/*.css') et ajoute tout les fichiers css correspondants.

	Asset::css('admin::admin_*.css');
	// (En utilisant les paramètres des chemin présent dans la section "Chemins et Espaces de noms"Paths and namespacing")
	// Exécute glob('adders/admin/css/admin_*.css') et ajoute tout les fichiers correspondants

	Asset::js('*.js', '*.js');
	// Ajoute tout les fichiers JS dans assets/js, en assurant qu'aucun des fichiers n'est pre-minifié.

Une exception est renvoyée si aucun fichier ne corresponds.

Minification et combinaison
--------------------------

La Minification utilise la librairie de Stephen Clay [Minify library](http://code.google.com/p/minify/).

The **min** and **combine** config file keys work together to control exactly how Asset operates:

**Combiner et minifier:**Quand un groupe activé est généré, les fichiers de ce groupe sont minifiés (ou la version minifiée sera utilisé, si indiqué dans le second paramètre cf. la fonction Asset::js()**),
et seront combinés dans un fichier dans **assets/cache** (configurable).

**Combiner seulement:**Quand un groupe activé est généré, les fichiers dans ce groupe sont combiné en un seul fichier dans **assets/cache** (configurable). Les fichiers ne sont pas minifiés.

**Minifier seulement:** Quant un groupe activé est généré, des balises séparées &lt;script&gt; ou &lt;link&gt; sont créés pour chaque fichier.
Si une version minifié d'un fichier est présent, il sera utilisé en lien. les versions non-minifiées seront également ajoutés en lien.
ATTENTION CE COMPORTEMENT PEUT NE PAS ETRE SOUHAITE. Il est utile, lors de l'utilisation de ressources à distance (cf. la section ressources à distance).

**Ni combinées ni minifiées** Qun groupe activé est généré, des balises &lt;script&gt; ou &lt;link&gt; sont créés pour chaque fichier.
La version non-minifiée de chaque fichier est utilisé dans chacun des cas.

Vous pouvez choisir d'inclure un commentaire au dessus de chaque balise &lt;script&gt; ou &lt;link&gt; affichant le nom du groupe contenu en définissant la clé de configuration **show\_files** à TRUE dans le fichier de configuration.
De la même façon, vous pouvez choisir d'inclure ces commentaires à l'intérieur de chaque fichier minifié, il suffit de définir  **show\_files\_inline** à **true**.

Vous pouvez contrôler si la librairie Asset minifie ou combine individuellment les groupes (voir la section "Groupes").

Quand vous minifiez des fichier CSS, les urls sont réécrites pour prendre en compte le fait que vos fichiers CSS ont été déplacés dans **assets/cache**.

Autant pour les fichiers CSS que JS, quand un fichier en cache est utilisé, lorsqu'on change l'ordre d'utilisation de ces fichiers dans le groupe 
le fichier en cache est regénéré pour prendre en compte leurs nouvelles positions. L'ordre des fichiers peut être important pour assurer les différentes dépendances.
Gardez bien ceci à l'esprit, quand vous ajouter des fichiers dynamiquement à des groupes, si vous décidez de changer l'ordre des fichiers dans un groupe identique, vous ne permettez pas au navigateur d'utiliser proprement son cache.

<div class="tip"><strong>NOTE:</strong> Si vous changez le contenu d'un groupe, et qu'un fichier cache est utilisé, un nouveau fichier cache sera généré. L'ancien fichier ne sera pas supprimé (les groupes sont modifiables, la librairie Asset ne sait pas définir si une page utilise encore l'ancien fichier en cache).
Il est conseillé de vider le cache régulièrement <strong>assets/cache/</strong>. Voir la section ci-dessous concernant le nettoyage du cache.</div>

Vider le cache
------------------
Les fichies en cache ne sont pas automatiquement supprimés (la librairie ne permet pas de savoir si les fichiers en cache sont encore utilisés ou non), voici donc quelques méthodes pour supprimer les fichiers en cache.

**Asset::clear\_cache()** permet de supprimer l'ensemble de fichiers en cache. **Asset::clear\_js\_cache()** et **Asset::clear\_css\_cache()** permettent de supprimer respectivement les fichiers JS et CSS en cache.
Ces fonctions acceptent en arguement un paramètre, permettant de supprimer les fichiers en cache qui ont été modifié depuis un certain temps. 
Ce temps est spécifié par une chaîne de caractère comme un [strtotime](http://php.net/strtotime), par exemple : "2 hours ago", "last Tuesday" ou "20110609".

Par exemple:

	Asset::clear_js_cache('2 hours ago');
	// Supprime tout les fichier JS modifié depuis plus de 2 heures

	Asset::clear_cache('yesterday');
	// Supprime tout les fichiers en caches modifiés depuis hier

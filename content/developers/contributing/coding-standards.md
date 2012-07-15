# Conventions de codage

Ces normes de formatage de code et de documentation doivent être respectées par toute personne qui voudra contribuer à PyroCMS. Tous les apports qui ne répondent pas à ces lignes directrices ne seront pas acceptées.

## File Formatting

### Closing PHP Tag

Les fichiers contenant que du code PHP doivent toujours omettre la balise de fermeture PHP. Cela empêche la plupart des fameux écrans blancs causée par un espace après la balise de fermeture PHP.

### Indentation

Tout retrait doit être effectué en utilisant des tabulations, PAS D’ESPACES. L’alignement des éléments après le retrait doit être effectué en utilisant des espaces, et non des tabulations.

	// retrait de 2 tabulation
	$var       = 'something';  // Retrait avec tabulation valeur & commentaires aligné.
	$variable  = 'else';       // Avec les régules ci-dessus en utilisant les espaces

### Line Endings

Les fins de ligne doivent être de type Unix LF.

### File Naming

Tous les noms de fichiers doivent être en minuscules. Sans aucunes exceptions.

### Encoding

Les fichiers doivent être enregistrés avec encodage UTF-8 et la marque d'ordre des octets (BOM) ne devraient pas être utilisée.

## Naming Conventions

### Classes

Les noms des classe doivent utiliser le tiret bas pour séparer les mots, et chaque mot dans le nom de la classe doit commencer par une lettre majuscule. L'utilisation de CamelCase est déconseillée, mais ne peut être évité dans certains cas.

	class Theme
	{

	}

 or 

	class Theme_Bubbles extends Theme
	{

	}

### Methods

Comme les noms des classes, les noms des méthodes doivent utiliser le tiret bas pour séparer les mots, et non pas CamelCase. Les noms de méthode devraient également être en minuscules. La visibilité devrait toujours être incluse (public, protégé, privé). Un tiret bas peut être utilisé au début du nom pour préciser si la méthode est protégée  privé ou pour signifier qu'elle doit être considérée comme public

	class Session
	{
		public function get_flash($name, $data)
		{
			// Votre code ici
		}
	}

or

	class View
	{

		// Tableau de données de vue global
		protected $_global_data = array();

		protected function capture($view_filename, array $view_data)
		{
			// Votre code ici
		}

	}

### Variables

Les noms de variables doivent être concises et contenir seulement des lettres en minuscules et des tirets bas. Les itérateurs de boucle doivent être court, de préférence un caractère unique.

	$first_name
	$buffer
	for ($i = 0; $i &lt; $max; $i++)

### Constants

Les constantes suivent les mêmes régules des variables à la seule exception que les constantes doivent être toutes en majuscule.

	MY_CONSTANT
	TEMPLATE_PATH
	TEXT_DEFAULT

## Keywords

Les mots-clés tels que <kbd> true </ kbd>, <kbd> false </ kbd>, <kbd> null </ kbd>, <kbd> as </ kbd>, etc. doivent être en minuscules, étant les majuscules sont réservé pour les constantes. En va de même pour les types primitifs comme <kbd>array </ kbd>, <kbd> integer</ kbd>, <kbd> string</ kbd>.

	$var = true;
	$var = false;
	$var = null;
	foreach ($array as $key => $value)
	public function my_function(array $array)
	function my_function($arg = null)

## Control Structures

Les structures des mots clés tels que <kbd>if</kbd>, <kbd>for</kbd>, <kbd>foreach</kbd>, <kbd>while</kbd>, <kbd>switch</kbd> doivent être suivi d'un espace de même que les  listes et les valeurs de paramètre / argument. Les accolades doivent être placés sur une nouvelle ligne, et <kbd>break</kbd> doit avoir le même onglet que son cas.

	if ($arg === true)
	{
		// Faire quelque chose ici
	}
	elseif ($arg === null)
	{
		//Faire quelque chose d'autre ici
	}
	else
	{
		// Mettez ici votre instruction else pour les conditions ci-dessus
	}
	
	foreach ($array as $key => $value)
	{
		// Votre boucle ici
	}
	
	for ($i = 0; $i < $max; $i++)
	{
		// Votre boucle ici
	}
	
	while ($i < $max)
	{
		// Votre boucle ici
	}
	
	switch ($var)
	{
		case 'value1':
		// Faire quelque chose ici
		break;
		default :
		// Faire quelque chose ici
		break;
	}

## Alternative if statements

Dans certains cas, une complète déclaration de <kbd>if</kbd> nécessite trop de code  pour une simple affectation conditionnelle ou un appel à une fonction. Dans ces cas, vous pouvez utiliser la logique d'exécution de PHP pour utiliser des opérateurs booléens plus court basé sur la syntaxe.

L'utilisation du <kbd>and</kbd> signifie que la deuxième partie sera évaluée uniquement si la première partie est valide, l'utilisation de <kbd>or</kbd> signifie que la deuxième partie sera exécutée uniquement si la première partie est fausse. 

Ne pas utiliser cela lorsque les deux <kbd>if</kbd> et <kbd>else</kbd> sont nécessaires, seulement dans des cas comme les simples instructions conditionnelles.

	// au lieu de if (isset($var)) { Config::set('var', $var); }
	isset($var) and Config::set('var', $var);

	// au lieu de if ( ! isset($var)) { $var = Config::get('var'); }
	isset($var) or $var = Config::get('var');

	// NE FAITE JAMAIS CELA
	$this->uri->segment(3) and $var = $this->uri->segment(3);
	$this->uri->segment(3) or $var = 'default';

	// Cela est mieux:
	if ($this->uri->segment(3))
	{
		$var = $this->uri->segment(3);
	}
	else
	{
		$var = 'default';
	}

	// ou bien comme ça:
	$var = $this->uri->segment(3) ? $this->uri->segment(3) : 'default';

## Comparisons, Logical operators

En comparant la fonction / méthode, les retours  et les variables doivent être de type courant, par exemple, certaines fonctions peuvent retourner
	<kbd>false</kbd>, et en comparant cela on  retourne les opérateurs de type sensibles tels que les <kbd>===</kbd> ou <kbd>!==</kbd>. En outre, l'utilisation de
	<kbd>and</kbd> ou <kbd>or</kbd>  est préférable sur <kbd>&&</kbd> ou <kbd>||</kbd>  pour plus de lisibilité. Dans certains cas, cela ne peut pas être évité et 
	<kbd>&&</kbd> ou <kbd>||</kbd> peuvent être utilisés. <kbd>!</kbd> doit  avoir des espaces des deux côtés quand il est utilisé.


	if ($var == false and $other_var != 'some_value')
	if ($var === false or my_function() !== false)
	if ( ! $var)

## Class/Interface Declarations

Dans la déclaration d'une classe/interface l’accolade s’ouvre après un retour chariot::

	class Session
	{

	}

## Function/Method Declarations

L’accolade ouvrante d’une fonction/méthode doit toujours commencer dans une nouvelle ligne et doit avoir la même indentation que sa structure.

	class Session
	{
		public static function get_flash($name, $data)
		{
			// Votre code ici
		}
	}

### Variables

Lors de l'initialisation des variables, On doit déclarer une et une seule variable par ligne. Pour améliorer la lisibilité du code, les valeurs et commentaires doivent entre aligner si nécessaire.

	$var        = ''; // do each on its own line
	$other_var  = ''; // do each on its own line

## Brackets and Parenthesis

No space should come before or after the initial bracket/parenthesis. There should not be a space before closing bracket/parenthesis.

	$array = array(1, 2, 3, 4);
	$array['my_index'] = 'something';
	for ($i = 0; $i < $max; $i++)

### String quotation

Les simples guillemets  sont préférables  aux doubles guillemets.

### Concatenation

La concaténation d'une chaîne ne doit pas contenir d'espaces autour des pièces concaténer.

	// Oui
	$string = 'my string '.$var.' the rest of my string';

	// Non
	$string = 'my string ' . $var . ' the rest of my string';

### Operators

	$var = 'something';
	if ($var == 'something') //space before and after logical operator
	$var = $some_var + $other_var; //space before and after math operator
	$var++; // no space before increment
	++$var; //no space after increment
	
## Documentation
Avoir une bonne documentation d'une API est une condition essentielle pour tout projet réussi. Lors du développement de votre module, s'il vous plaît prenez le temps pour documenter votre code ou même écrire des articles d'aide (mais c'est une autre histoire).

La plupart des composants du core de PyroCMS sont [documentés ici](http://www.pyrocms.fr/docs)

La documentation actuelle de l'API est généré par [DocBlox](http://www.docblox-project.org/). Cela donne la possibilité de refléter l'approche HMVC utilisé lors du développement de PyroCms dans la documentation actuelle de l'API. Voici comment les paquets de la documentation de l'API sont structurés dans PyroCms:

	* Bibliothèques externes utilisants leurs paquets respectifs (none of our business)
	* Tout ce qui est relié à PyroCMS est sous le paquet * PyroCMS *.
	* A l'intérieur du paquet * PyroCMS * il y a deux sous-paquet distincts:
	  * *Core*, tout ce qui vient avec la publication du  PyroCMS.
	  * *Addon*, 3rd party modules, thèmes, etc.
	* Each of *Core* & *Addon* peuvent éventuellement avoir les sous-paquets suivants:
	  * *Controllers*
	  * *Models*
	  * *Modules*
	  * *Libraries*
	  * *Plugins* 
	  * *Widgets*
	* En outre les  *Modules* peuvent avoir:
	  * *Controllers*
	  * *Models*
	  * *Libraries*
	  * *Plugins*
	  * *Widgets*

Dans la distribution PyroCMS vous trouverez un fichier de configuration pour générer localement la documentation de l'API et examiner votre travail. Rappelez-vous, vous pouvez toujours vous référer à la source PyroCMS pour voir comment les choses sont faites.
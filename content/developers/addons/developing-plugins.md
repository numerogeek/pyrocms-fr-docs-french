# Developing Plugins

L'un des concepts centraux des fonctionnalités est PyroCMS balises. Si vous êtes familier avec PyroCMS vous avez certainement déjà des plugins auparavant. Voici un exemple d'une balise simple qui retourne l'URL en cours:

	{{ noparse }}{{ url:current }}{{ /noparse }}
	
Le code derrière une balise comme celles-ci est appelé un plugin. Les plugins sont des fichiers spéciaux en PHP qui ont la capacité d'être appelé via des tags PyroCMS, et peut faire des choses comme mettre un paramètres de la balise d'appui. Ils sont simples à écrire et à faire intégrer des fonctionnalités complexes dans les layouts PyroCMS propre et bien organisé.

## Plugins modulaires vs autonomes

Bien qu'ils soient identiques dans leur structure, un plugin peut être soit fichier autonome, ou être un fichier <def>plugin.php</def> dans un module plus grand.

Un plugin à l'intérieur d'un module serait quelque chose qui complète un module personnalisé que vous avez construit, tandis qu'un plugin autonome serait quelque chose de général, comme un plugin Google Maps ou un moyen de lister les Tweets dans votre propre syntaxe. Un plugin autonome n'a pas besoin d'une structure plus grand module, il peut être utilisé sur son propre.

## Exemple de Plugin

C'est le plugin session qui peut être trouvé dans <def>system/pyrocms/plugins/session.php</def>.

	&lt;?php defined('BASEPATH') or exit('No direct script access allowed');
	/**
	 * Session Plugin
	 *
	 * Read and write session data
	 *
	 * @package		PyroCMS
	 * @author		PyroCMS Dev Team
	 * @copyright	Copyright (c) 2008 - 2012, PyroCMS
	 *
	 */
	class Plugin_Session extends Plugin
	{ 
		/**
		 * Data
		 *
		 * Loads a piece of session data
		 *
		 * Usage:
		 * {{ noparse }}{{ session:data name=&quot;foo&quot; }}{{ /noparse }}
		 *
		 * @param	array
		 * @return	array
		 */
		function data()
		{ 
			$name = $this->attribute('name');
			$value = $this->attribute('value');
	
			// Mo vaue? Just getting
			if ($value !== NULL)
			{
				$this->session->set_userdata($name, $value);
				return;
			 }
	
			return $this->session->userdata($name);
		}
	
		/**
		 * Flash
		 *
		 * Loads a piece of flashdata
		 *
		 * Usage:
		 * {{ noparse }}{{ session:flash name="foo" }}{{ /noparse }}
		 *
		 * @param	array
		 * @return	array
		 */
		function flash()
		{
			$name = $this->attribute('name');
			$value = $this->attribute('value');
	
			// No value? Just getting
			if ($value !== NULL)
			{
				$this->session->set_flashdata($name, $value);
				return;
			 }
	
			return $this->session->flashdata($name);
		}
	}

	/* End of file theme.php */
	
Dans le code ci-dessus, s'il vous plaît noter quelques nouveaux éléments importants:

* Le nom de la class **Plugin_** suivie par le nom du plugin en minuscules.
* La classe du plugin étend la classe **Plugin**.
* Chaque fonction tag correspond directement à une fonction de classe.
* Les données de chaque fonction est retourné, pas un echo.
	
## Obtenir les attributs de tag du plugin

Ce qui rend les balises vraiment puissant, c'est qu'ils peuvent prendre des attributs qui vous donnent la liberté de modifier la sortie tag sur la base de données d'entrée. Voici un exemple:

	{{ noparse }}{{ session:data name="foo" }}{{ /noparse }}

Dans le code ci-dessus, nous pouvons accéder au paramètre nom dans la fonction de données comme ceci:

	$this->attribute('name');

Au cas où aucun attribut est défini, vous pouvez spécifier une valeur par défaut:

	$this->attribute('name', 'a default value');
	
Si aucune valeur n'a été spécifiée, $this->attribute sera utilisé la valeur par défaut.

## Tag Pairs

Tags ne sont pas toujours en une seule ligne qui renvoie une chaîne simple. Les Tags peuvent également être des paires, ce qui signifie qu'ils ont une ouverture et de fermeture de balise et de contenu entre eux.

Les plugins ont quelques fonctionnalités intégrées afin de gérer facilement les paires de balises. Par exemple, voici le blog:posts tag: 

    {{ noparse }}
{{ blog:posts limit="5" order-by="title" }}
    &lt;h2>{{ title }}</h2>
    &lt;p>Written by: &lt;a href="/users/profile/{{ author_id }}">{{ author_name }}&lt;/a>&lt;/p>
{{ /blog:posts  }}
    {{ /noparse }}

Le premier tag prend des paramètres, et il ya une balise de fermeture en bas.A l'intérieur de la balise, il ya des variables dont nous avons besoin afin de remplacer des données.

Dans de tels cas, nous pouvons retourner un tableau associatif de structure de données à partir de notre fonction de plugin, et les variables seront remplacées par les données que nous renvoyons. Dans ce cas, nous pouvons retourner un tableau d'entrées de blog à cette balise dans le fichier plugin et provoquer l'analyseur tag pour boucler à travers chaque noeud array (chaque billet de blog dans notre cas) et de remplacer les variables entre l'ouverture et la balise fermante avec le variables que vous avez défini.

Voici un exemple de ce que nous pourrions revenir:

	return array(
		array(
			'title'			=> 'First Blog Post',
			'author_id'		=> 1,
			'author_name'	=> 'Phil Sturgeon',
		),
		array(
			'title'			=> 'Second Blog Post',
			'author_id'		=> 2,
			'author_name'	=> 'Jerel Unruh',
		)
	);

Vous voulez interroger la base de données pour obtenir des billets du bon blog , mais c'est l'idée générale.

Il est même possible d'envoyer des variables qui sont des tableaux associatifs et ceux-ci peuvent être bouclée dans l'intérieur des balises:

	{{ noparse }}
{{ categories }}
	{{ category_name }}
{{ /categories}}
    {{ /noparse }}

### Tag Pair Raw Content

Vous pouvez également obtenir et utiliser le contenu complet entre les balises dans un plugin en appelant dans votre fichier de plugin:

	$this->content();
	
Le contenu de tag pair peut être modifié avant l'analyse en appelant l'analyseur Lex lui-même et de retourner une chaîne:

	$parser = new Lex_Parser();
	$parser->scope_glue(':');
	
	return $parser->parse($this->content(), $data = array(), array($this->parser, 'parser_callback'));
# Librairie Template

La librarie Template permet de générer les vues du front et du back office de PyroCMS. La librairie est chargée automatiquement, vous n'avez pas besoin de la charger dans vos contrôleurs.

## Méthodes de référence

### title(<var>$title1, [$title2, $title3, …]</var>)

La fonction title permet de définir le titre de la page. Vous pouvez envoyer autant de paramètres titre que vous souhaitez, seul le premier est requis. Vos titres seront séparés par le séparateur de titre (| par défaut).

#### Exemple:

	$this->template->title('La Page Actuelle');

### build(<var>$view, [$data]</var>)

La fonction build permet de construire le template de sortie et est utilisé au lieu de simplement charger une vue. Il permet de regrouper automatiquement les paramètres de thèmes, le layout et les données transmises à la vue et construit ces éléments automatiquement, votre vue ne comportant que les contenus de la page.

#### Exemple:

	$this->template->build('form', $this->data);

### set(<var>$var_name, $var_value</var>)

La fonction set permet de définir et réutiliser des variables dans vos vues. Vous pouvez ainsi transmettre des chaînes de caractères ou des tableaux.

#### Exemple:

Chaîne de caractères:

	$this->template->set('foo', $bar);
	
Tableau de données:	
	
	$this->template->set(array('foo' => $bar, 'foo2' => $bar2));
	
### prepend_metadata(<var>$string</var>)

Cette méthode permet d'ajouter une chaîne de caractère au début de la sortie metadata.

#### Exemple:

	$this->template->prepend_metadata('<script src="/js/jquery.js"></script>');
	
### append_metadata(<var>$string</var>)

Cette méthode permet d'ajouter une chaîne de caractère à la fin de la sortie metadata.

#### Exemple:

	$this->template->append_metadata('<script src="/js/jquery.flot.js"></script>');
	
### set\_layout(<var>$layout\_name</var>)

Cette méthode permet de sélectionner un gabarit de page (layout) présent dans votre dossier **mon_theme/views/layouts**.

#### Exemple:

	// Ceci utilisera mon_theme/views/layouts/two_col.html
	// Comme gabarit de page.
	$this->template->set_layout('two_col');
	
<div class="tip"><strong>Note:</strong> Lorsque vous utilisez les contrôleurs Public\_Controller et Admin\_Controller, le gabarit est déjà défini. Cependant, dans certains cas, vous pouvez préférer surcharger ce gabarit par un gabarit personnalisé.</div>

### set\_theme(<var>$theme\_name</var>)

Cette méthode vous permet de définir un thème.

#### Exemple:

	$this->template->set_layout('my_theme');
	
<div class="tip"><strong>Note:</strong> Comme pour set_layout, Le thème est déjà défini lorsque vous étendez les contrôleurs Public\_Controller et Admin\_Controller.</div>

### enable\_parser(<var>bool</var>)

Cette méthode permet d'authoriser/refuser l'utilisation des Tag PyroCMS Lex. Lorsque le parseur de Tag est défini à off, les tags PyroCMS présents dans vos vues ne seront pas fonctionnels.

#### Exemple

	$this->template->enable_parser(true);

### enable_minify(<var>bool</var>)

Activer/désactiver la minification des éléments ajouté via la librairie Template.

#### Exemple

	$this->template->enable_minify(true);

### get\_theme\_path()

Cette méthode retourne le chemin du thème courant.

## Chaînage

Les méthodes de la librairie Template sont souvent chaînées dans PyroCMS, vous pourrez fréquement les voir appelées comme suit:

	$this->template
		->title($this->module_details['name'], lang('keywords:add_title'))
		->set('keyword', $keyword)
		->build('admin/form', $this->data);

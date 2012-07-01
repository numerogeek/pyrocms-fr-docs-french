# Couche GUI du Panneau d'administration (Control Panel GUI)

PyroCMS dispose d'un grand nombre d'outils pour développer des panneau d'aministration simples, ergonomiques et normalisés. Les paragraphes suivants décrivent les différents outils GUI et les standards utilisés pour faire fonctionner le panneau d'administration de PyroCMS.

Pour rester cohérent, cette page contient des informations sur la nomenclature GUI - du nommage des boutons au positionnement des wording. Nous vous recommandons fortement de suivre ces nomenclatures, vous pouvez cependant les ignorer mais garder à l'esprit l'expérience utilisateur et de réuitilisabilité.

## Page de Module Basique

Une page de module basique contient une boite constituée d'une barre de titre gris, un corps blanc, il sera défini comme suit :

	<section class="title">
		<h4>Titre dans la barre</h4>
	</section>
	
	<section class="item">
		
		Le contenu de votre Module.
	
	</section>

Comme vous pouvez le voir, vous avez deux sections two _section_ elements: titre et objet. Très simple! Tout le contenu de votre module peut aller dans cette section objet.

### Convention de Nommage des Titres

* Les Sections Titre doivent être exclusivement réservé aux titres, pas d'instructions, filtres de contrôles ou autres contenus.
* Les Sections Titre doivent contenir une seule et unique balise h4 avec le titre à l'intérieur. Pas d'instructions, filtres de contrôles ou autres contenus.
* Les Sections Titre ne doivent pas être vide. Empty states should be left to empty state messages.
* Les Sections Titre doivent être des Noms ("Variables" instead of "Liste de Variables").

## Boutons

Les boutons du paneau d'administration de PyroCMS sont disponibles sous deux formats: Les petits boutons gris (boutons secondaires) et les gros boutons (boutons primaires) qui peuvent être colorés.

Les boutons secondaires recquièrent une classe *button*. Les boutons primaires requièrent une classe *btn* et une classe couleur comme *blue* où *gray* (bleu et gris).

### Guide des Couleurs

L'utilisation des couleurs doit au possible suivre la nomenclature des couleurs suivantes:

* Bleu: Sauver, Sauvegarder, Sauvegarder et Quitter
* Gris: Annuler
* Orange: Lien Neutre (comme éditer ou une action qui n'est pas un lien)

### Boutons d'Action

Les boutons d'action comme Sauvegarder, Sauvegarder et Fermer, Annuler, etc. doivent être des boutons primaires et suivre la nomenclature de couleurs ci-dessus.

### Informations diverses

* Les boutons sur une même ligne doivent être de la même taille (nb: ne mettez pas des boutons primaires et secondaires côte à côte).

## Affichage de données

Les Sections sont des blocs de contenus pour l'interface PyroCMS 2.0. Ils sont composé d'un titre et d'une section item (objet):

lister des données et les afficher dans un tableau est souvent nécessaire lorsqu'on développe un menu. PyroCMS applique un formatage de style automatique aux tableaux.

### Boutons d'Action

Plusieurs lignes de tableau peuvent nécéssiter une colonne contenant des boutons d'action (comme Editer, Supprimer, etc.). Ces boutons doivent être dans une colonne contenant la classe **actions**. Les boutons seront ainsi flottants à droite. Les boutons d'actions seront généralement des boutons secondaires.

	<td class="actions">
		<?php echo
			anchor('sample', lang('sample:view'), 'class="button" target="_blank"').' '.
			anchor('admin/sample/edit/'.$item->id, lang('sample:edit'), 'class="button"').' '.
			anchor('admin/sample/delete/'.$item->id, 	lang('sample:delete'), 'class="button"');
		?>
	</td>
	
Le heading de la colonne contenant les boutons d'action ne nécessite pas de titre. Il peut être laissé vide.
	
### Cas vides ou inexistant

Les pages ne retournant aucun résultat doivent contenir une simple ligne de texte expliquant qu'il n'y a pas de résultat dans une div avec une classe **no_data**:

	<div class="no_data">
		<?php echo lang('sample:no_items'); ?>
	</div>
	
### Batch Actions

Certaines listes nécessitent la possibilité de sélectionner plusieurs élements de la liste à l'aide de case à cocher pour chaque ligne. Il y a quelques étapes pour pouvoir le réaliser. Tout d'abord, il faut ajouter une case à cocher à chaque ligne, ce qui peut être fait de la façon suivante:

	<td><?php echo form_checkbox('action_to[]', $item->id); ?></td>
	
Après avoir changé la variable en modifiant **$item->id** avec la valeur que vous souhaiter donner au tableau action\_to, cela vous permet d'avoir une case à cocher pour chaque ligne.

Dans le header, vous pouvez disposer d'une case à cocher permettant de séléctionner toutes les cases à cocher des ligne du tableau. Ceci peut être fait en ajoutant la classe **check-all**:

	<th><?php echo form_checkbox(array('name' => 'action_to_all', 'class' => 'check-all'));?></th>

PyroCMS est doté d'une logique intégrée permettant d'activer/désactiver des boutons d'actions sur les lignes sélectionnées. Vous pouvez utiliser cette logique en ajout des boutons d'action dans une div contenant une classe **table\_action\_buttons**:

	<div class="table_action_buttons">
		<?php $this->load->view('admin/partials/buttons', array('buttons' => array('delete'))); ?>;
	</div>
	
### Filtrer et Chercher

Si vous souhaitez ajouter la possibilité de filtrer et chercher dans votre table, vous devez suivre le format suivant:

	<fieldset id="filters">
		
		<legend><?php echo lang('global:filters'); ?></legend>
		
		<?php echo form_open(); ?>
	
		<?php echo form_hidden('f_module', $module_details['slug']); ?>
			<ul>  
				<li>
	        		<?php echo lang('blog_status_label', 'f_status'); ?>
	        		<?php echo form_dropdown('f_status', array(0 => lang('global:select-all'), 'draft'=>lang('blog_draft_label'), 'live'=>lang('blog_live_label'))); ?>
	    		</li>
			
				<li>
	        		<?php echo lang('blog_category_label', 'f_category'); ?>
	        		<?php echo form_dropdown('f_category', array(0 => lang('global:select-all')) + $categories); ?>
	    		</li>
				
				<li><?php echo form_input('f_keywords'); ?></li>
				<li><?php echo anchor(current_url() . '#', lang('buttons.cancel'), 'class="cancel"'); ?></li>
			</ul>
		<?php echo form_close(); ?>
	</fieldset>

Les filtres utilisés peuvent être personnalisés. L'exemple ci-dessus peut vous donner une idée des possibilités données par PyroCMS.

### Pagination

La pagination est un élément important pour afficher des tableau de données, PyroCMS possède un système permettant de générer des paginations and PyroCMS has a built-in pagination generation function that has all of the PyroCMS pagination styles preset.

	create_pagination($uri, $total_rows, $limit = NULL, $uri_segment = 4, $full_tag_wrap = TRUE)
	
Exemple d'utilisation :

	$this->data->pagination = create_pagination(
									'admin/sample/index',
									$total_items,
									$this->settings->item('records_per_page'),
									4);

## Formulaires

Voici un exemple de code pour insérer un formulaire :

	<div class="form_inputs">
	
	<ul>
		<li>
			<label for="name"><?php echo lang('sample:name'); ?> <span>*</span></label>
			<div class="input"><?php echo form_input('name', set_value('name', $name), 'class="width-15"'); ?></div>
		</li>
	
		<li>
			<label for="slug"><?php echo lang('sample:slug'); ?> <span>*</span></label>
			<div class="input"><?php echo form_input('slug', set_value('slug', $slug), 'class="width-15"'); ?></div>
		</li>
	</ul>
	
	</div><!-- /.form_inputs -->
	
	<div class="buttons">
		<?php $this->load->view('admin/partials/buttons', array('buttons' => array('save', 'cancel') )); ?>
	</div><!-- /.buttons -->

<div class="tip"><strong>Note :</strong> PyroCMS prends en charge l'affichage de tout les messages flash (comme les notifications d'erreurs), tant que vous utilisez la classe Form Validation de CodeIgniter, vous ne vous préocupez pas d'afficher les messages d'erreurs dans vos formulaires.</div>

## Messages Flash

Coming soon.
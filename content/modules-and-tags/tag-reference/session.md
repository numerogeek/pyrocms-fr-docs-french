# Session Tags

Le plugin _session_  vous donne la possibilité de définir et de lire les données de session.

## session:data

	{{ noparse }}{{ session:data }}{{ /noparse }}
	
Affiche ou définit un morceau de données de session.

Si vous fournissez une *value*, elle fixera les données de session et de ne rien afficher, sinon, la valeur actuelle de *name* qui sera affiché.

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Defaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">name</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name of the data you want to display or set.</td>
		</tr>
		<tr>
			<td width="100">value</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>Add a value to set data instead of displaying it.</td>
		</tr>
	</tbody>
</table>

### Exemples

#### Configuration

	{{ noparse }}{{ session:data name="color_preference" value="red" }}{{ /noparse }}

#### Affichage des données

	{{ noparse }}{{ session:data name="color_preference" }}{{ /noparse }}

Retourne:

	red
	
## session:flash	

Identique à la fonction de données, mais utilise les données flash.

Les données Flash sont des données qui sont disponible uniquement pour le chargement de la page suivante, puis elle sont détruites.

### Exemples

#### Configuration

	{{ noparse }}{{ session:flash name="color_preference" value="blue" }}{{ /noparse }}

#### Affichage des données

	{{ noparse }}{{ session:data name="color_preference" }}{{ /noparse }}

Retourne:

	blue

## session:messages

Displays a flashdata message.

PyroCMS a des messages normalisés qui appartiennent à l'une des trois catégories:

* success
* notice
* error

Chacun a un sens différent et, par défaut apparaît avec un nom de classe qui lui est associé.

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Defaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">success</td>
			<td>success</td>
			<td>No</td>
			<td>Set your own class name for success messages.</td>
		</tr>
		<tr>
			<td width="100">notice</td>
			<td>notice</td>
			<td>No</td>
			<td>Set your own class name for notice messages.</td>
		</tr>
		<tr>
			<td width="100">error</td>
			<td>error</td>
			<td>No</td>
			<td>Set your own class name for error messages.</td>
		</tr>
	</tbody>
</table>

### Exemples

#### Sortie standard

	{{ noparse }}{{ session:messages }}{{ /noparse }}

Retourne:

	<div class="error">There was an error.</div>

#### Classes personnalisées

	{{ noparse }}{{ session:messages success="my_success_class" }}{{ /noparse }}

Retournes: 
	
	<div class="my_success_class">Success!</div>

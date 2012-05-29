# Pages Tags

La balise _pages_ affiche les infos des pages .

## pages:url

	{{ noparse }}{{ pages:url }}{{ /noparse }}
	
Obtient URL d'une page en fonction de son ID.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Defaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">id</td>
			<td width="100">None</td>
			<td width="100"Oui</td>
			<td>Id de la page dont vous voulez l'url</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ pages:url id="4" }}​{{ /noparse }}

Retourne:

	http://www.example.com/about
	
## pages:children	
	
	{{ noparse }}{{ pages:children }}{{ /noparse }}

Paire de balises qui parcourt les enfants d'une page parent.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Defaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">id</td>
			<td width="100">None</td>
			<td width="100">Oui</td>
			<td>Id de la page parent dont vous voulez les enfants.</td>
		</tr>
		<tr>
			<td width="100">limit</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>Nombres de pages à retourner</td>
		</tr>
	</tbody>
</table>

### Example

	{{ noparse }}{{ pages:children id="1" limit="2" }}
	&lt;h2>{{ title }}&lt;/h2>
	{{ body }}
{{ /pages:children }}{{ /noparse }}

Returns:

	<h2>Child One</h2>
	Body Content One
		
	<h2>Child Two</h2>
	Body Content Two
	
## pages:display

	{{ noparse }}{{ pages:display }}{{ /noparse }}

Afficher une page à l'intérieur d'autre contenu. Peut être utilisé comme une seule étiquette pour sortir le corps de la page uniquement, ou une paire de tags pour le contrôle total.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Défaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">id</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>ID de la page que vous voulez afficher.</td>
		</tr>
		<tr>
			<td width="100">slug</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>Slug de la page que vous voulez afficher.</td>
		</tr>
	</tbody>
</table>

### Exemples

	{{ noparse }}{{ pages:display slug="home" }}
	&lt;h2>{{ title }}&lt;/h2>
	{{ body }}
{{ /pages:display }}{{ /noparse }}

Retourne :

	<h2>Page Title</h2>
	<p>Page Body</p>

## pages:chunk

	{{ noparse }}{{ pages:chunk }}{{ /noparse }}

Un tag qui permet à n'importe quel morceau d'une page d'être affiche n'importe ou sur le site, même à l'intérieur une autre page de contenu.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Défaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">id</td>
			<td width="100">None</td>
			<td width="100">Oui</td>
			<td>ID de la page auquel appartient le morceau</td>
		</tr>
		<tr>
			<td width="100">name</td>
			<td width="100">None</td>
			<td width="100">Oui</td>
			<td>Nom du morceau de la page que vous voulez afficher</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ pages:chunk id="1" name="default" }}{{ /noparse }}

Retourne:

	<p>Bienvenue sur notre site. Nous n'avons pas encore tout à fait terminé la mise en place de notre site, mais s'il vous plaît , ajoutez nous à vos favoris et revenez bientôt.</p>

## pages:is

	{{ noparse }}{{ pages:is }}{{ /noparse }}

Un tag qui confirme, si une page est un enfant direct d'une autre page, ou est un descendant d'une autre page.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Default</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">child</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>ID ou Slug de la page dont vous voulez vérifier le rapport.</td>
		</tr>
		<tr>
			<td width="100">children</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>Enfant séparé par une virgule.</td>
		</tr>
		<tr>
			<td width="100">parent</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>ID oui Slug dont vous voulez vérifier s'il est le parent de l'enfant.</td>
		</tr>
		<tr>
			<td width="100">descendent</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>ID or Slug de la page pour vérifier si il est un descendant de l'enfant.</td>
		</tr>
	</tbody>
</table>

### Exemple A

	{{ noparse }}{{ if {pages:is child="ingredients" parent="cookbook"} == true }}
	&lt;p>Click here to see table of contents cookbook&lt;/p>
{{ endif }}{{ /noparse }}

Returns:

	<p>Cliquez ici pour voir le tableau du livre de cuisine </p>
	
### Exemple B
	
	{{ noparse }}{{ if {pages:is child="terms-and-conditions" parent="information"} == true }}
&lt;body class="terms information">
{{ else }}
&lt;body class="">
{{ endif }}{{ /noparse }}

Retourne :

	<body class="terms information">

## pages:page_tree

	{{ noparse }}{{ pages:page_tree }}{{ /noparse }}
	
A tag that displays a tree of pages starting from the id specified.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Défaut</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">start-id</td>
			<td width="100">None</td>
			<td width="100">Oui</td>
			<td>ID de la page dont vous voulez afficher les enfants</td>
		</tr>
		<tr>
			<td width="100">disable-levels</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>Liste des slugs de page séparé par le caracères |. Exemple: secret|super-secret|nuclear-codes</td>
		</tr>
		<tr>
			<td width="100">order-by</td>
			<td width="100">title</td>
			<td width="100">Non</td>
			<td>colonne de la base qui sera utilisé pour le tri.</td>
		</tr>
		<tr>
			<td width="100">order-dir</td>
			<td width="100">asc</td>
			<td width="100">Non</td>
			<td>Sens de tri </td>
		</tr>
	</tbody>
</table>

### Exemples

	{{ noparse }}{{ pages:page_tree start-id="20" }}{{ /noparse }}
	
Returns:

	<ul>
	     <li><a href="http://example.com/page">Nom de page</a>
	          <ul>
	               <li><a href="http://example.com/page/child">Child Name</a></li>
	          </ul>
	     </li>
	</ul>

# URL Tags

Le plugin URL vous donne l'accès à toutes les informations de l'URL.

## url:current

Affiche l'URL courante

### Exemple

	{{ noparse }}{{ url:current }}{{ /noparse }}

Retourne:

	http://www.example.com/current/uri/

## url:site

Affiche l'url du site en entier. Utilisez  ça pour générer des liens dans vos sites. Passez des paramètres pour avoir des urls construites avec tous les segments.

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">uri</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>URI segments passed to the site_url function.</td>
		</tr>
	</tbody>
</table>

### Example

Sans URI spécifié : 

	{{ noparse }}{{ url:site }}{{ /noparse }}

Retourne:

	http://www.example.com

Avec une URI spécifié :

	{{ noparse }}{{ url:site uri="contact" }}{{ /noparse }}

Retourne:

	http://www.example.com/contact

<div class="tip"><strong>Note:</strong>  La fonctione retourne l'url avec index.php si vous n'utilisez pas using mod_rewrite pour le retirer et que vous n'avez pas changé le <strong>$config['index_page']</strong> dans <em>/system/cms/config/config.php</em>. Pour plus d'infos voir  {{ link title="Retirer index.php des url" uri="/general/demarrer-avec-pyrocms/supprimer-indexphp-des-urls" }}.</div>

## url:base

Affiche la base de l'URL sans prendre en compte le mod_rewrite.

### Example

	{{ noparse }}{{ url:base }}{{ /noparse }}

Retourne:

	http://www.example.com/

## {{ noparse }}url:segments{{ /noparse }}

Affiche un segment spécifique : 

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Name</th>
			<th>
				Default</th>
			<th>
				Required</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				segment</td>
			<td width="100">
				None</td>
			<td width="100">
				Yes</td>
			<td>
				Number of segment (left to right, first segment is 1).</td>
		</tr>
		<tr>
			<td width="100">
				default</td>
			<td width="100">
				None</td>
			<td width="100">
				No</td>
			<td>Default value if selected segment does not exist/is not in use.</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ url:segments segment=&quot;1&quot; default=&quot;home&quot; }}{{ /noparse }}

Si l'url est :

	http://www.example.com/products
	
Le tag retournera : 

	products

## {{ noparse }}url:anchor{{ /noparse }}</h5>

Génère une balise <a></a> avec l'url absolue a partir des segments URI.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Name</th>
			<th>
				Default</th>
			<th>
				Required</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				segments</td>
			<td width="100">
				None</td>
			<td width="100">
				Yes</td>
			<td>
				Segments passed to the anchor function.</td>
		</tr>
		<tr>
			<td width="100">
				title</td>
			<td width="100">
				None</td>
			<td width="100">
				No</td>
			<td>
				Text displayed between &lt;a href&gt;&lt;/a&gt; tags. If omitted, URL is duplicated.</td>
		</tr>
		<tr>
			<td width="100">
				class</td>
			<td width="100">
				None</td>
			<td width="100">
				No</td>
			<td>
				Optional CSS class.</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ url:anchor segments=&quot;users/login&quot; title=&quot;Login&quot; class=&quot;login&quot; }}{{ /noparse }}
	
Retuourne:

	<a href="http://www.example.com/users/login" class="login">Login</a>

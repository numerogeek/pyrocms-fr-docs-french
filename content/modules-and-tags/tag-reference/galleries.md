# Tags Galleries

**Note:** Sur PyroCMS 2.1, Le module *Galleries* n'est plus inclus dans le code du noyau PyroCMS, même si elle peut être téléchargé gratuitement à partir du [store](http://www.pyrocms.com/store/details/galleries).

Le Tag <em>galleries</em> affiches les images d'une gallerie.

## galleries:images
	
	{{ noparse }}{{ galleries:images }}{{ /noparse }}
	
Affiche toutes les images de toute la galerie ci.

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Nom</th>
			<th>
				Defaut</th>
			<th>
				Requis</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				slug</td>
			<td width="100">
				None</td>
			<td width="100">
				Yes</td>
			<td>
				The gallery to display images from.</td>
		</tr>
		<tr>
			<td width="100">
				limit</td>
			<td width="100">
				All</td>
			<td width="100">
				No</td>
			<td>
				Limit the number of displayed images.</td>
		</tr>
		<tr>
			<td width="100">
				offset</td>
			<td width="100">
				0</td>
			<td width="100">
				No</td>
			<td>
				Offset the images when retrieving them with a limit set.</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{&nbsp;galleries:images slug=&quot;test-gallery&quot; limit=&quot;5&quot; }}
	&lt;h2&gt;{{&nbsp;title }}&lt;/h2&gt;
	&lt;a href=&quot;http://yoursite.com/galleries/{{&nbsp;gallery_slug }}/{{&nbsp;file_id }}&quot;&gt;
		&lt;img src=&quot;http://yoursite.com/files/thumb/{{&nbsp;file_id }}/100/75&quot; alt=&quot;{{&nbsp;name }}&quot;/&gt;
		100/75 is desired thumbnail width/height respectively
	&lt;/a&gt;
	&lt;p&gt;{{&nbsp;description }}&lt;/p&gt;
{{&nbsp;/galleries:images }}{{ /noparse }}

## galleries:exists

	{{ noparse }}{{&nbsp;galleries:exists }}{{ /noparse }}

Vérifie que la galerie existe.

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Nom</th>
			<th>
				Defaut</th>
			<th>
				Requis</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				slug</td>
			<td width="100">
				None</td>
			<td width="100">
				Yes</td>
			<td>
				The gallery to check for.</td>
		</tr>
	</tbody>
</table>
<p>
	&nbsp;</p>

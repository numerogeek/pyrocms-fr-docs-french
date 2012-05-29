# Blog Tags

## blog:posts

	{{ noparse }}{{ blog:posts }}{{ /noparse }}

Afficher tous les messages de blog ou les blogs par catégorie.

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
				category</td>
			<td width="100">
				Toutes les catégories</td>
			<td width="100">
				No</td>
			<td>
				Afficher les messages de cette seule catégorie.</td>
		</tr>
		<tr>
			<td width="100">
				limit</td>
			<td width="100">
				10</td>
			<td width="100">
				Non</td>
			<td>
				Le nombre maximum de messages à afficher.</td>
		</tr>
		<tr>
			<td width="100">
				order-by</td>
			<td width="100">
				created_on</td>
			<td width="100">
				n</td>
			<td>
				Choisissez la colonne à trier. (category_title, le titre, id_auteur, created_on, updated_on)</td>
		</tr>
		<tr>
			<td width="100">
				order-dir</td>
			<td width="100">
				asc</td>
			<td width="100">
				No</td>
			<td>
				Le sens du tri les résultats. (asc, desc)</td>
		</tr>
	</tbody>
</table>

### Exemple</strong>

	{{ noparse }}{{ blog:posts limit=&quot;5&quot; order-by=&quot;title&quot; order-dir=&quot;desc&quot; category=&quot;pyrocms&quot; }}
	&lt;h2&gt;{{ title }}&lt;/h2&gt;
	&lt;p&gt;{{ intro }} &lt;a href=&quot;{{ url }}&quot; title=&quot;Read more about: {{ title }}&quot;&gt;Read more&lt;/a&gt;&lt;/p&gt;
	&lt;p&gt;Written by: &lt;a href=&quot;/users/profile/{{ author_id }}&quot;&gt;{{ author_name }}&lt;/a&gt;&lt;/p&gt;
{{ /blog:posts }}{{ /noparse }}
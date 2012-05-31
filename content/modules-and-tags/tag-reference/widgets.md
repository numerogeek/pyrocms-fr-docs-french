# Widgets

Le tag _widgets_ affiche le données de widget définies dans la section Contenu  &gt; Widgets du panneau de controle.

## Tags

## widgets:area

	{{ noparse }}{{ widgets:area }}{{ /noparse }}

Affiche tout les widgets d'une zone de widget.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">slug</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Slug for the widget area as defined in CP &gt; Content &gt; Widgets</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ widgets:area slug="sidebar" }}{{ /noparse }}

## widgets:instance

	{{ noparse }}{{ widgets:instance }}{{ /noparse }}

Affiche une instance spécifique de widget.

### Attributes

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">id</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>ID of the widget instance given to you after installing a widget in CP &gt; Content &gt; Widgets.</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ widgets:instance id="5" }}{{ /noparse }}

# Navigation Tags

Le tag _navigation_  crée une liste de lien de navigation basé sur les groups de navigation dans le panneau de controle dans CP &gt; Design &gt; Navigation.

## navigation:links

	{{ noparse }}{{ navigation:links }}{{ /noparse }}

Crée une list de lien pour un groupe.

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
			<td width="100">group</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>The navigation group the tag should use.</td>
		</tr>
		<tr>
			<td>list-tag</td>
			<td>ul</td>
			<td>No</td>
			<td>Choose between ol and ul lists. The value of this is wrapped in brackets on either end.</td>
		</tr>
		<tr>
			<td>tag</td>
			<td>li</td>
			<td>No</td>
			<td>Type of tag that surrounds each navigation item. The value of this is wrapped in brackets on either end.</td>
		</tr>
		<tr>
			<td>class</td>
			<td>current</td>
			<td>No</td>
			<td>The CSS class to add when an element is the current page.</td>
		</tr>
		<tr>
			<td>more-class</td>
			<td>has_children</td>
			<td>No</td>
			<td>The class applied to a parent li when it contains a ul or ol.</td>
		</tr>
		<tr>
			<td>first-class</td>
			<td>first</td>
			<td>No</td>
			<td>The class applied the first in a list of dropdown links.</td>
		</tr>
		<tr>
			<td>last-class</td>
			<td>last</td>
			<td>No</td>
			<td>The class applied to the last in a list of dropdown links.</td>
		</tr>
		<tr>
			<td>more-class</td>
			<td>None</td>
			<td>No</td>
			<td>The class to use when an element has child elements.</td>
		</tr>
		<tr>
			<td>separator</td>
			<td>None</td>
			<td>No</td>
			<td>String that separates each navigation item.</td>
		</tr>
		<tr>
			<td>items-only</td>
			<td>true</td>
			<td>No</td>
			<td>true or false. Set if the output source code should be wrapped with an optional list-tag.</td>
		</tr>
		<tr>
			<td>indent</td>
			<td>None</td>
			<td>No</td>
			<td>tab or space. Character used to indent the output of source code.</td>
		</tr>
		<tr>
			<td>link-class</td>
			<td>None</td>
			<td>No</td>
			<td>The class names to apply in all anchor elements.</td>
		</tr>
		<tr>
			<td>wrap</td>
			<td>None</td>
			<td>No</td>
			<td>Html that that you wish to wrap the link title in. Most likely a span element</td>
		</tr>
		<tr>
			<td>top</td>
			<td>link</td>
			<td>No</td>
			<td>Set to &quot;text&quot; and the top level menu items will be rendered as plain text instead of links.</td>
		</tr>
	</tbody>
</table>

### Usage Tag simple

Vous pouvez utiliser une approche simple pour afficher un morceau de HTML. 
Cela va appliquer les noms de classe au <kdb>&lt;li&gt;</kdb> (par défaut) et les balises <kdb>&lt;a&gt;</kdb> pour les ancres.

	{{ noparse }}{{ navigation:links group="header" }}{{ /noparse }}
	
Retourne:

	<li class="first current"><a href="http://localhost/pyrocms/index.php">Home</a></li><li class="last"><a href="http://www.google.com">About Us</a></li>

et

	{{ noparse }}{{ navigation:links group="header" indent="tab" link-class="foo" }}{{ /noparse }}
	
Retourne:

	<li class="first current">
		<a href="http://localhost/pyrocms/index.php" class="foo">Home</a>
	</li>
	<li class="last">
		<a href="http://www.google.com" class="foo">About Us</a>
	</li>
	

Si vous utilisez des liens imbriqués le tag par défaut affichera le code HTML suivant lorsque les éléments de menu sont disposés dans un menu à plusieurs niveaux.

	{{ noparse }}{{ navigation:links group="header" indent="tab" }}{{ /noparse }}
	
Retourne:
	
	<li class="first current">
		<a href="http://example.com/home">Home</a>
	</li>
	<li class="">
		<a href="http://example.com/about-us">About Us</a>
		<ul>
			<li class="first">
				<a href="http://example.com/contact">Contact</a>
			</li>
			<li class="last">
				<a href="http://example.com/staff">Staff</a>
				<ul>
					<li class="single">
						<a href="http://example.com/history">History</a>
					</li>
				</ul>
			</li>
		</ul>
	</li>
	<li class="last">
		<a href="http://example.com/blog">Blog</a>
	</li>

### Tag Pair Usage

Si vous souhaitez un contrôle complet sur votre balisage de navigation, vous pouvez utiliser la fonction de liens comme une paire de balises:

	{{ noparse }}&lt;ul>
{{ navigation:links group="header" }}
&lt;li><a href="{{ url }}" class="{{ class }}">{{ title }}</a>
	{{ if children }}
	&lt;ul>
	{{ children }}
		&lt;li>&lt;a href="{{ url }}">{{ title }}&lt;/a>&lt;/li>
	{{ /children }}
	&lt;/ul>
	{{ endif }}
&lt;/li>
{{ /navigation:links }}
&lt;/ul>{{ /noparse }}

### Variables

Les variables suivantes sont à votre disposition dans la paire de balise:

<table cellpadding="0" cellspacing="0">
	<thead>
		<tr>
			<th>Name</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td width="150">{{ noparse }}{{ url }}{{ /noparse }}</td>
			<td>Full URL of the link.</td>
		</tr>
		<tr>
			<td width="150">{{ noparse }}{{ title }}{{ /noparse }}</td>
			<td>Link title.</td>
		</tr>
		<tr>
			<td width="150">{{ noparse }}{{ class }}{{ /noparse }}</td>
			<td>Link class.</td>
		</tr>
		<tr>
			<td width="150">{{ noparse }}{{ target }}{{ /noparse }}</td>
			<td>Link target.</td>
		</tr>
		<tr>
			<td width="150">{{ noparse }}{{ children }}{{ /noparse }}</td>
			<td>Tag pair of child link elements. Each child element has all the same above variables as the main elements.</td>
		</tr>
	</tbody>
</table>

### Advanced Options

Vous pouvez utiliser une combinaison de params pour sortir un morceau de code HTML qui affiche un court paragraphe de la navigation, using `<p>` as list\_tag to wrap all items by disabling items_only and using the tag `<span>` to wrap each anchor link.

	{{ noparse }}{{ navigation:links group="header" tag="span" class="active" separator="|" list-tag="p" items-only="false" }}{{ /noparse }}
	
Retourne:

	<p><span class="first active"><a href="http://localhost/pyrocms/index.php">Home</a></span> | <span class="last">...
	<a href="http://www.google.com">About Us</a></span></p>

# Theme

Le plugin _theme_  vous donne accès au assets du thème (layout partial entre autres). C'estun point important dans la construction de module.

Le slug du thème du plugin est __theme__,  et il doit être appelé comme ça:

	{{ noparse }}{{ theme:<em>function</em> }}{{ /noparse }}

#### Fonctions

#### &#123;&#123; theme:options &#125;&#125; ####

Afficher une option pour le thème courant. POur plus d'infos sur son usage referez vous à : 
Displays an option for the current theme. To read more about this tag and its usage refer to the {{ link uri="/general/faire-des-themes-pyrocms/personnaliser-vos-themes" title="La documentation des thèmes" }}.</a>

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">option</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Option slug to request from theme.</td>
		</tr>
	</tbody>
</table>

**Exemple:**

	{{ noparse }}&#123;&#123; if theme:options:layout == 'full-width' &#125;&#125;{{ /noparse }}
			
		{{ noparse }}&lt;div class="full-width"&gt;{{ /noparse }}
				
			{{ noparse }}{{ template:body }}{{ /noparse }}
			
		{{ noparse }}&lt;/div&gt;{{ /noparse }}
		
	{{ noparse }}{{ endif }}{{ /noparse }}

#### {{ noparse }} {{ theme:partial }} {{ /noparse }} ####

Charge un layout partial du theme courant.

**Attributs**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">name</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name slug of the theme to be loaded.</td>
		</tr>
	</tbody>
</table>

**Exemple:**

	{{ noparse }}&#123;&#123; theme:partial name="header" &#125;&#125;{{ /noparse }}

#### {{ noparse }}{{ theme:css }}{{ /noparse }} ####

Generates a &lt;link&gt; to a css file in the current theme.

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">file</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name of the css file.</td>
		</tr>
		<tr>
			<td width="100">type</td>
			<td width="100">text/css</td>
			<td width="100">No</td>
			<td>The type attribute.</td>
		</tr>
		<tr>
			<td width="100">title</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>The title attribute.</td>
		</tr>
		<tr>
			<td width="100">media</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>The media attribute.</td>
		</tr>
	</tbody>
</table>

**Example:**
	
	{{ noparse }}&#123;&#123; theme:css file="style.css" &#125;&#125;{{ /noparse }}
	
	{{ noparse }}&lt;link href="themes/default/css/style.css" type="text/css" rel="stylesheet" /&gt;{{ /noparse }}

#### {{ noparse }}{{ theme:image }}{{ /noparse }} ####

Genere une balise &lt;img&gt; pour un fichier dans le thème courant.

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">file</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name of the image file.</td>
		</tr>
		<tr>
			<td width="100"><em>misc</em></td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>This function will take any other image tag attributes and pass them along to the image tag.</td>
		</tr>
	</tbody>
</table>

**Exemple:**
	
	{{ noparse }}&#123;&#123; theme:image file="fun.jpg" alt="Fun!" &#125;&#125;{{ /noparse }}

	{{ noparse }}&lt;img href="themes/default/img/fun.jpg" alt="Fun!" /&gt;{{ /noparse }}

#### {{ noparse }}{{ theme:js }}{{ /noparse }} ####

Genère un lien script &lt;js&gt; du thème courant.

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">file</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name of the javascript file.</td>
		</tr>
	</tbody>
</table>

**Exemple:**
	
	{{ noparse }}&#123;&#123; theme:js file="extra.js" &#125;&#125;{{ /noparse }}
	
	{{ noparse }}&lt;script type="text/javascript" src="themes/default/js/extra.js"&gt;{{ /noparse }}

#### {{ noparse}}{{ theme:favicon }}{{ /noparse }} ####

Genere un lien pour un fichier favicon dans le thème courant.

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th width="100">Name</th>
			<th width="100">Default</th>
			<th width="100">Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td>file</td>
			<td>favicon.ico</td>
			<td>No</td>
			<td>Favicon file.</td>
		</tr>
		<tr>
			<td>rel</td>
			<td>shortcut icon</td>
			<td>No</td>
			<td>Favicon rel.</td>
		</tr>
		<tr>
			<td>type</td>
			<td>image/x-icon</td>
			<td>No</td>
			<td>Favicon type.</td>
		</tr>
		<tr>
			<td>xhtml</td>
			<td>true</td>
			<td>No</td>
			<td>Need a W3C valid link tag xhtml? Enter false if you use HTML5.</td>
		</tr>
		<tr>
			<td>base</td>
			<td>path</td>
			<td>No</td>
			<td>"path" or "url".</td>
		</tr>
	</tbody>
</table>

**Exemple:**
	
	{{ noparse }}&#123;&#123; theme:favicon file="favicon.png" &#125;&#125;{{ /noparse }}

	{{ noparse }}&lt;link href="/system/pyrocms/themes/default/img/favicon.png" rel="shortcut icon" type="imagem/x-icon"&gt;{{ /noparse }}

#### &#123;&#123; theme:variables &#125;&#125; ####

Set ou retrouve une variable pour le thème de votre choix. Les variables peut etre initialisé dans un layout et utilisé ni'mporte ou.

**Attributes**
<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Name</th>
			<th>Default</th>
			<th>Required</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">name</td>
			<td width="100">None</td>
			<td width="100">Yes</td>
			<td>Name of variable.</td>
		</tr>
		<tr>
			<td width="100">value</td>
			<td width="100">None</td>
			<td width="100">No</td>
			<td>Value to set. Leave blank to retrieve a previously set variable.</td>
		</tr>
	</tbody>
</table>

**Exemple (Variable Setting - nothing displayed):**

	{{ noparse }}{{ theme:variables name="day_or_night" value="day" }}{{ /noparse }}

**Exemple (Variable Retrieval):**

	{{ noparse }}{{ theme:variables name="day_or_night" }}{{ /noparse }}
	{{ noparse }}day{{ /noparse }}

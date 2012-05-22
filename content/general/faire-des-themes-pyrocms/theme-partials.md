# Les partie de thème (Theme Partials)

Les "Partials" vous permet d'organiser votre code html en de petites sections.
Les sections peuvent être chargées dans différents fichiers layout. Cela vous évite de taper le même code dans plusieurs layouts.

Les Partials sont créés <dfn>addons/&lt;site-ref&gt;/themes/&lt;theme-name&gt;/views/partials/partialname.html</dfn> et sont chargés avec : 

<pre>{{ noparse }}{{ theme:partial name="partialname" }}{{ /noparse }}</pre>

Vous pouvez mettre de la syntaxe, du Html, ou ce que vous voulez, comme dans un layout, il sera interpreté de la même manière.

## Example

Un simple exemple d'un layout utilisant un partial : 

<pre class="prettyprint">{{ noparse }}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
	{{ theme:partial name=&quot;header&quot; }}
&lt;/head&gt;
&lt;body&gt;
	&lt;h1&gt;{{ template:title }}&lt;/h1&gt;
	{{ template:body }}
&lt;/body&gt;
&lt;/html&gt; {{ /noparse }}</pre>

Dans l'exemple ci dessus, tout le code du header est dans  le fichier header.html. il peut être chargé dans le default.html, en utilisant ce code. si vous souhaitez créer un fichier blog.html, tout ce que vous devez ajouter est  : {{ noparse }}{{ theme:partial }}{{ /noparse }} tag. 

# Tags PyroCMS 

Une des caractéristiques uniques de PyroCMS est le système de Balises, alimentés par le [Parser Lex](https://github.com/happyninjas/lex). Mots-clés qui vous permettent de puiser dans les fonctionnalités les plus avancées en utilisant une syntaxe simple à l'intérieur même de vos layouts, partials, et même des pages elles-mêmes. Les tags peuvent vous permettre de faire des choses vraiment puissantes sans supprimer vos layouts avec du code PHP désordre.

Le guide suivant vous enseignera les rudiments des tags et comment les utiliser dans vos designs.

<ul id="doc_sub_nav">
<li><a href="{{ url:current_url }}#basic">Tags de base</a></li>
<li><a href="{{ url:current_url }}#attributes">Attribut de Tag</a></li>
<li><a href="{{ url:current_url }}#pairs">Tag Pairs</a></li>
<li><a href="{{ url:current_url }}#conditionals">Tag Conditionnelles</a></li>
</ul>

<div id="basic"></div>

## Tags de base

Commençons par un exemple très simple, une balise qui retourne l'un de nos paramètres du site:

    {{ noparse }}{{ settings:site_name }}{{ /noparse }}

_Side note:</strong> L'espace blanc à l'intérieur des accolades est facultatif, mais il aide à l'esthétique et la lisibilité._

Cette balise a quelques éléments de base: deux accolades sur les deux sites, et deux chaînes de texte séparés par deux points. La première chaîne, **settings** dans ce cas, le tag dit que ce plugin pour référencer, puis la deuxième chaîne, **site_name** dans ce cas, le tag dit quelle fonction ou variable est appelé.

Donc, si nous mettons le tag ci-dessus dans notre mise en page, et notre site_name variable" a été réglé "Bill's Bagels", donc il retournera:

     Bill's Bagels

## Comments

Si vous souhaitez mettre des commentaires, vous pouvez les intégrer à l'intérieur **&#123;&#123;#** and **#&#125;&#125;**. Ex: **&#123;&#123;# c'est un commentaire #&#125;&#125;**. 
C'est un avantage sur les conventions [HTML comment tags](http://www.w3.org/TR/html4/intro/sgmltut.html#h-3.2.4) qu'il ne sera pas visible pour les utilisateurs qui visualisent le code source de votre site Web.

<div id="attributes"></div>

## Tag Attributes

Ce qui rend les tags vraiment puissant, c'est qu'ils peuvent prendre des attributs qui vous donnent la liberté de modifier la sortie tag sur la base de données. Voici un exemple:

     {{ noparse }}{{ url:segments segment="1" }}{{ /noparse }}

Dans l'exemple ci-dessus, nous appelons le url plugin qui présente une function  **segments**. C'est bien beau, mais on peut aussi passer les paramètres de la balise afin de modifier la sortie. Dans ce cas, nous tapons le mot-clé pour obtenir le premier segment. Donc, si votre URL est _http://www.example.com/bills/bagels_, cette balise sera remplacée par:
     bills

Vous pouvez avoir plusieurs paramètres ainsi. Par exemple, le fonction  **segments**  vous permet de spécifier une valeur par défaut via un second paramètre:

     {{ noparse }}{{ url:segments segment="1" default="home" }}{{ /noparse }}

Si le premier segment est vide, l'étiquette sera de retour «home».

<div class="tip"><strong>Astuce:</strong> Certains paramètres sont obligatoires et d'autres sont facultatives. Assurez-vous de vérifier le tag reference pour s'assurer que  tous les passages de paramètres sont bons, et s'il ya des ceux qui sont optionnels qui vous donneront une fonctionnalité supplémentaire dont vous avez besoin.</div>

<div id="pairs"></div>

## Tag Pairs

Une autre fonctionnalité très puissante des tags PyroCMS est la capacité à utiliser les données entre les balises. Prenez cet exemple d'un tag messages de blog:

    {{ noparse }}{{ blog:posts limit="5" order-by="title" order-dir="desc" }}
     &lt;h2>{{ title }}&lt;/h2>
{{ /blog:posts }}{{ /noparse }}

Comme vous le remarquerez, nous avons un tag d'ouverture et de clôture ici. Dans le cas du blog, la fonction **posts ** va rechercher sur le blog ,les postes correspondant aux paramètres que nous avons fourni , la réimpression du HTML entre les balises pour chacune et toutes les autres balises substitué  avec des données en provenance de ce poste particulier, dans ce cas le titre.

Paires de tags ne sont pas nécessairement en boucle grâce à un contenu, cependant. Prendre l'exemple d'un tag qui entoure un bloc de texte et limite la sortie dudit texte à un certain nombre de mots. Dans ce cas, le texte entre les balises est tout simplement agir comme un autre paramètre - même si elle est plus grande et plus souple.

### Variable Loops

Parfois, les étiquettes contiennent des tableaux de données que vous pouvez parcourir. Vous pouvez le faire en utilisant une syntaxe de la balise même paire:

    {{ noparse }}{{ images }}
     &lt;img src="{{ url }}" />
{{ /images }}{{ /noparse }}

<div id="conditionals"></div>

## Tags Conditionnels

Plusieurs fois dans vos layouts, vous voulez montrer quelque chose, sous certaines conditions. Par exemple, si un utilisateur est connecté ou si un segment url a une certaine valeur.Les tags PyroCMS vous permettent de faire cela avec un syntaxe de balise if / else.

### Basic Conditionals

Voici un exemple simple d'une déclaration de tag conditionnel:

    {{ noparse }}{{ if user:logged_in }}
     &lt;p>You are logged in.&lt;/p>
{{ endif }}{{ /noparse }}

Cette structure générale sera très familier si vous familiariser avec [conditionals in languages like PHP](http://php.net/manual/en/control-structures.if.php). Le tag if si la valeur de **user:logged_in** est vrai, et retourne ce qui est entre cette balise et le tag **endif**.

### Operateurs conditionnels

Vous pouvez utiliser des opérateurs pour comparer des valeurs dans une instruction if. Ils sont utilisés pour comparer deux valeurs. Voici un exemple:

    {{ noparse }}{{ if {url:segments segment="2"} == 'categories' }}
    &lt;p>Looks like you are in the categories section.&lt;/p>
{{ endif }}{{ /noparse }}

<div class="tip"><strong>Note:</strong> les fonction tags PyroCMS peut être utilisé lors des conditionnels, mais il doit être enveloppé dans de simples accolades s'ils en ont un ou plusieurs paramètres, comme dans l'exemple ci-dessus.</div>

Voici les opérateurs conditionnels disponibles:

<table>
<tr>
<td>==</td>
<td>Equals. Values equal each other.</td>
</tr>
<tr>
<td>!=</td>
<td>Does not equal. Values do not equal each other.</td>
</tr>
<tr>
<td>===</td>
<td>Values equal each other in value and type. For instance, if one value is a true boolean value, the other value must also be in order to fufill this operator.</td>
</tr>
<tr>
<td>!==</td>
<td>Same concept as above but checks that values do not equal each other and are not the same type.</td>
</tr>
<tr>
<td>></td>
<td>Greater than</td>
</tr>
<tr>
<td><</td>
<td>Less than</td>
</tr>
<tr>
<td>>=</td>
<td>Greater than or equal to</td>
</tr>
<tr>
<td><=</td>
<td>Less than or equal to</td>
</tr>
</table>

Vous pouvez aussi utiliser le raccourci   **!** comme opérateur logique:

{{ noparse }}{{ if !user:logged_in }}
    &lt;p>You are not logged in.&lt;/p>
{{ endif }}{{ /noparse }}

### Conditionnels multiples

Vous pouvez avoir des conditionnelles multiples pour certaines déclarations les plus avancées :

{{ noparse }}{{ if variables:custom_var == 'foo' }}
    &lt;p>Looks like a foo.&lt;/p>
{{ elseif variables:custom_var == 'bar' }}
    &lt;p>Looks like a bar.&lt;/p>
{{ endif }}{{ /noparse }}

### opérateurs logiques

Vous pouvez aussi utiliser les opérateurs logiques comme ceci :

{{ noparse }}{{ if variables:custom_var != 'foo' and variables:custom_var != 'bar' }}
     &lt;p>No foos and no bars!&lt;/p>
{{ endif }}{{ /noparse }}

Les opérateurs logiques disponibles sont les suivants:

<table>
<tr><td>and / &&</td></tr>
<tr><td>or / ||</td></tr>
</table>

# Widgets, Plugins, et Modules

Les modules ,plugins et widgets sont une façon d'obtenir des fonctionnalités plus complexes dans vos sites  en vous aidant du {{ link uri="/general/les-basiques/pyrocms-tags" title="tag system" }}. PyroCMS vient avec ses propres modules, widgets et plugins de base mais vous pouvez également en télécharger des gratuits ou payants via le store PyroCMS [add-on store](http://www.pyrocms.com/store).

<div class="tip"><strong>Note:</strong> si vous êtes un développeur et intéressé pour développer vos propres widgets, plugins et modules. Vous pouvez trouver comment le faire dans notre guide des developpeurs.</div>

Voici un aperçu de chacun.

## Widgets

Les widgets sont de petits morceaux de code qui font des choses spécifique. Par exemple, vous pouvez créer un simple widget HTML  qui contient du code HTML, ou vous pouvez créer un widget de connexion qui affiche un formulaire de connexion.

Vous pouvez créer et modifier des widgets dans la section widgets du panneau de contrôle (dans le menu **Contenu &rarr; Widgets**). Une fois que vous les avez créé, vous pouvez facilement les ajouter dans vos layouts en utilisant les tags PyroCMS:

	{{ noparse }}{{ widgets:instance id="6"}}{{ /noparse }}

Vous pouvez même grouper des widgets pour les commander, ce qui est pratique si vous avez une barre latérale que vous voulez gérer à partir du panneau de contrôle.
	
	{{ noparse }}{{ widgets:area slug="blog-right" }}{{ /noparse }}

## Plugins

Les plugins sont simples : ils permettent d'afficher ou manipuler des données dans vos layout en utilisant les tags PyroCMS.
Ils suivent la syntaxe suivantes : 

	{{ noparse }}{{ plugin:function parameter="value" }}{{ /noparse }}

PyroCMS est lviré avec un tableau de plugin qui rend les choses usuelles plus facile à faire, comme recuperer un segment d'url :

	{{ noparse }}{{ url:segments segment="1" }}{{ /noparse }}

Vous pouvez aussi afficher une arborescence des pages : 

	{{ noparse }}{{ pages:page_tree start="about" }}{{ /noparse }}

vous pouvez aussi utiliser desz boucles : 

	{{ noparse }}{{ blog:posts limit="5" order-by="title" }}
     &lt;h2>&lt;a href="{{ url }}">{{ title }}&lt;/a>&lt;/h2>
{{ /blog:post }}{{ /noparse }}

_Pour plus d'informations sur les tags PyroCMS, consultez le "tag reference" ._

## Modules

De nombreux add-ons besoin de plus que des fonctionnalités accessible via des tags PyroCMS. Parfois vous avez besoin d'une interface dans le panneau de contrôle, ainsi que d'autres ressources comme les fichiers javascript.

Les modules sont le plus grand type des add-on PyroCMS. Ils ont une place dans le menu du panneau de contrôle (en général), des contrôles du panneau de contrôle, leurs propres widgets, et leurs propres plugins.

Par exemple, le module Pages contient la zone de panneau de commande qui vous permet de créer et organiser les pages, et aussi le plugin de pages  , qui vous permet de faire des choses comme afficher une arborescence des pages avec des tags PyroCMS.

Ce qui rend les modules PyroCMS unique est le fait qu'ils se customise tout seul sur vos pages selon vos thèmes.

Par exemple, le module Blog vous permet de gérer les messages dans le panneau de contrôle, mais yoursite.com/blog affiche les messages en utilisant votre thème.
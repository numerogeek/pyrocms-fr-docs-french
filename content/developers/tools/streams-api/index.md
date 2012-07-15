# Streams Core API

Depuis la version PyroCMS 2.1, le noyau de PyroStreams est maintenant un module intégré à PyroCMS et appelé Streams Core. Ceci signifie que tout les modules dans PyroCMS peuvent maintenant bénéficier des avantages fournis par les fonctions de flux. Pour rendre ceci facile, une API Streams à été développée dans le but de rendre simple l'usage des Flux.

## Pré-requis API

### Chargement de l'API

L'API Streams est un driver, vous pouvez la charger ainsi:

	$this->load->driver('Streams');
	
Une fois l'API chargée, vous pouvez utiliser chaque driver ainsi:

	$this->streams->driver_name->function();
	
### Drivers API

L'API Streams contient cinq drivers:

* Flux (Streams)
* Champs (Fields)
* Entrées (Entries)
* CP
* Utilitaires (Utilities)

Nous rentrons plus en détail pour chacun de ces drivers, mais dans un premier temps nous allons vous donner un aperçu plus général des fonctionnalités fournies par les Flux (Streams).

## Généralité sur les Flux

Les "Flux" sont une couche d'abstraction de base de données.

### Espace de Noms et Préfixage

Maintenant que les modules peuvent utiliser les flux pour toute interaction sur les données, dans le but de prévenir les conflits de noms entre les tables, les Flux peuvent utiliser des espaces de noms et être préfixés. Par exemple, le module Utilisateur (system/cms/modules/users) peut préfixer tout ses champs et flux avec **users**. Ainsi un champ appelé _first\_name_ peut exister à la fois pour le module Users ou un autre module.

Dans certains cas, vous pouvez également souhaiter préfixer vos table. Ce préfixe viens en addition du prefixe SITE_REF utilisé par PyroStreams. Ceci est pratique pour être sur de ne pas avoir de conflit entre les noms de tables.

### Noyau Streams vs. PyroStreams

PyroStreams est toujours vendu comme un extension séparée et peut être utilisée avec PyroCMS (l'extension est fournie avec la version professionnelle de PyroCMS), Quelle sont les différences alors ? PyroStreams surcharge le fonctionnement du noyau streams et fourni une couche GUI pour créer des structures de données. Il inclut également le plugin PyroStream pour afficher des données.

### Pourquoi utiliser l'API Streams ?

Vous pouvez utiliser les interactions avec la base de donnée comme bon vous semble pour vos modules, le noyau Streams Core vous permet de gagner un temps précieux et certains avantages comme:

* Vous n'avez plus besoin d'écrire des système de validation CRUD, l'API s'en charge pour vous.
* Vous pouvez utiliser des type de Champs et intégrer leurs fonctionnalités dans votre module.
* Vous disposez d'une façon simple d'installer et désinstaller vos modules.

## Notre Exemple

Un exemple serait certainement plus explicite, voici notre exemple:

_Notre module de démonstration est un simple module permettant de gérer une FAQ. Les utilisateurs peuvent ajouter des FAQs et les voir sous forme de liste. Le seul flux est le flux faq et notre espace de nom est streams\_sample._

Le code source du module FAQ peut être téléchargé en suivant le lien suivant : [https://github.com/pyrocms/streams-enabled-module-sample](https://github.com/pyrocms/streams-enabled-module-sample)     
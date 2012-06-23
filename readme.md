# Documentation PyroCMS test

Ce dépôt est la page d'accueil de la Documentation PyroCMS. 

* [PyroCMS Documentation](http://pyrocms.com/docs)

## Statut de la documentation

La Documentation est taggée et générée après la sortie de chaque version stable, quand la version 2.1.1 arrive la branche "2.1"  est mise à jour à la dernière version. Les documents de Développement sont également enregistrés ici, actuellement la version "2.2" existe en anglais mais nécessite des contributeurs et des contributions.

## Contribuer la Documentation

Pour contribuer à la documentation PyroCMS, il faut forker le dépôt dans votre environnement local. La documentation PyroCMS fonctionne avec Fizl[Fizl](https://github.com/parse19/Fizl), qui est un CMS basé sur fichiers écrit avec CodeIgniter. Il ne nécessite pas de base de données pour fonctionner, vous pouvez ainsi facilement charger la documentation.

Les fichiers de la documentation actuelle sont contenus dans le dossier **content**, la structure des dossiers représente la structure des URL. Chaque page est un fichier markdown, par exemple, le fichier **Constantes et Globales** est nommé **constantes-et-globales.md**.

## Aider à mettre à jour la Documentation

Les parties de la documentation à améliorer sont nombreuses. Certaines sont prioritaires&nbsp;:

* Détecter et supprimer les liens internes cassés
* Vérifier les tags des différentes pages
* Documenter les modules
* Effectuer les corrections orthographique etgrammaticales. Vérifier la clareté des phrases

Si vous avez des remarques à nous faire, merci de laisser vos commentaires grâce à GitHub inline code commenter.

## Guide des Styles pour la Documentation

### Format

Tout les fichiers doivent être des fichiers inscriptibles .md en Markdow (à l'exception des tableaux HTML qui peuvent être écrits en texte plein HTML).

Les liens internes à la documentation doivent être formatés en utilisant le plugin de Fizl Lien. Par exemple :

	{{ link uri="general/basics/organisation" title="Organisation" }}
	
La boite info Jaune (as seen on such pages as the Lex Parser developer guide) doit suivre la structure HTML suivante:

	<div class="tip"><strong>Note&nbsp;:</strong> Votre Contenu ici</div>
	
Ces boites doivent êtres utilisées pour afficher des informations importantes que l'utilisateur doit connaitre.

### Organisation

La Documentation est articulée autour de 4 sections:

* Généralités
* Modules & Tags
* Développeurs
* PyroCMS Pro

Ces sections contiennent des sous-sections séparés en colonnes.

Si vous crééz une nouvelle page, elle devrait normalement trouver place dans une section existante.. Si vous pensez que nous devons ajouter une nouvelle section ou si vous avez des suggestions d'organisation merci de nous contacter par email [contact@pyrocms.fr](mailto:contact@pyrocms.fr).
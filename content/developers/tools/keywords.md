# Mots-Clés



Les Mots-Clés correspondent à ce que peut s'appeler des Tags sur d'autres systèmes. Nous utilisons déjà ce terme, donc nous utilisons à la place Mots-Clés. Ils sont utilisés dans le système pour ajouter des META Mots-Clés sur vos pages et d'ajouter des Mots-Clés à vos articles de blog.

## Utilisez des Mots-Clés dans vos modules

Ajoutez simplement un champ **char(32)** dans votre base de données. Cela permet d'enregistrer la chaîne MD5 qui représente la combinaison de mot-clés que vous avez utilisé.

<script src="https://gist.github.com/1777448.js"> </script>

Dans l'exemple ci-dessus, <kdb>Keywords::process('foo, bar, baz')</kdb> prend des chaines de caractères séparées par des virgules et converti le résultat en une chaîne MD5, qui est un identifiant unique résultant de la combinaison des mots-clés utilisés.

## Schéma

Chaque mot-clé est ajouté et enregistré dans une table nommée "default\_keywords", ce qui permet de disposer d'une petite table facilement exploitable pour compter les mots-clés les plus populaires.

	+-------+------------------+------+-----+---------+----------------+
	| Field | Type             | Null | Key | Default | Extra          |
	+-------+------------------+------+-----+---------+----------------+
	| id    | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
	| name  | varchar(50)      | NO   |     | NULL    |                |
	+-------+------------------+------+-----+---------+----------------+

Il seront reliés à la table "default\_keywords\_applied" pour faire concorder le hash du mot clé et sont identifiant unique keyword_id.

	+------------+------------------+------+-----+---------+----------------+
	| Field      | Type             | Null | Key | Default | Extra          |
	+------------+------------------+------+-----+---------+----------------+
	| id         | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
	| hash       | char(32)         | NO   |     | NULL    |                |
	| keyword_id | int(10) unsigned | NO   |     | NULL    |                |
	+------------+------------------+------+-----+---------+----------------+
	
## Afficher des mots-clés

Dans vos contrôleurs public, vous pouvez l'utiliser pour construire les lien vers une liste de mot-clés.

	Keywords::get_links($hash, 'blog/tagged')
	
Vous pouvez également retourner un tableau ou une chaine de caractère en utilisant les méthodes suivantes :

	Keywords::get_array($hash);
	Keywords::get_string($hash);

Pour plus d'information consultez la page "Mots-Clés" dans [la documentation de l'API](/2.1/api).
# Routage Modulaire (Modular Routing)

Le Routage est un outil puissant qui permet au développeur de créér des URL personnalisées qui ne doivent pas nécessairement répondre aux standards modules/[contrôleur/]méthode/paramètres. Les fichiers de configuration Route peuvent être ajouté dans chaque module pour gérer les URL au sein d'un module. Cependant PyroCMS ne sait utiliser le fichier routes.php d'un module donné que si le nom de ce module est égal au premier ségment de l'URI.

Par exemple&nbsp;:

	/artists/top-10
	
Cette URL signifiera à PyrCMS de charger le fichier /addons/modules/artists/config/routes.php.

	/top-10-artists

Essayer d'acheminer cette URL ne suggère pas quel module est à utilise, la route doit alors être spécifiée dans **system/pyrocms/config/routes.php**.

Editer le fichier principal route de PyroCMS peut être considéré comme une mauvaise pratique mais si avant d'effectuer une mise à jour vous faites la sauvegarde du fichier routes.php en même temps que config.php et database.php vous ne rencontrerez pas de régressions en cas de mise à jour. Le routage est effectué de cette façon, car si l'application comprends de nombreux modules possédant leur propre fichier routes.php, il faut tous les charger, ceux qui peut être lourd de conséquences en terme de performances.
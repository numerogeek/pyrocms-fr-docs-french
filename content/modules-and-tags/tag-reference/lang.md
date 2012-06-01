# Tags Lang 

Le Tag _lang_  permet d'accéder aux paramètres de langue pour l'utilisateur connecté. Si aucun utilisateur n'est connecté, la langue du site par défaut est utilisée.

## lang:name

	{{ noparse }}{{ lang:name }}{{ /noparse }}

Retourne le nom complet de la langue courante.

### Exemple Output:

	English

## lang:folder

	{{ noparse }}{{ lang:folder }}{{ /noparse }}

Retourne le nom du dossier de la langue courante.

### Exemple Output:

	english
	
## lang:code

Retourne le code de langue du langage courant.

	{{ noparse }}{{ lang:code }}{{ /noparse }}

### Exemple Output:

	en
	
## lang:direction

Retourne le sens des langues de la langue courante.

	{{ noparse }}{{ lang:direction }}{{ /noparse }}

### Exemple:

	ltr
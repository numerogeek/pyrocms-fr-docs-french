# Fichiers

Le Module Fichiers est un module principal pour le stockage des médias et fichiers que vous utiliser comme contenus du site. il permet de gérer
le téléchargement et peut s'interconnecter avec des services de cloud computing. Il dispose d'une librairie puissante permettant de standardiser les téléchargements.

Pour utiliser cette librairie vous devez tout d'abord la charger <kbd>$this->load->library('files/files');</kbd> Vous pouvez alors l'utiliser dans votre module.

*Note : vous devez d'abord renseigner dans le Panneau d'administration (PA) vos paramètres de fournisseur cloud en vous rendant dans PA > Paramètres > Fichiers avant de pouvoir exploiter les données cloud*

## Résultats

Première chose à noter, chaque action effectuée par la librairie renvoie un tableau qui sera au format suivant :

	array('status' => true, 'message' => 'Un message dans la langue courante', 'data' => $any_available_data);

## Créer un dossier

#### Usage

	Files::create_folder($parent_id, $folder_name);

#### Paramètres

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Description</th>
			<th>Requis</th>
			<th>Type</th>
		</tr>
		<tr>
			<td>$parent_id</td>
			<td>l'id du dossier parent. Utilisez 0 pour définir la racine.</td>
			<td>Oui</td>
			<td>Integer</td>
		</tr>
		<tr>
			<td>$folder_name</td>
			<td>Le Nom à donner à ce dossier. Par défaut 'Untitled Folder'</td>
			<td>Non</td>
			<td>String</td>
		</tr>
		<tr>
			<td>$location</td>
			<td>L'emplacement (local, rackspace-cf où amazon-s3). Par défaut il est défini à local</td>
			<td>Non</td>
			<td>String</td>
		</tr>
		<tr>
			<td>$remote_container</td>
			<td>Si l'emplacement de destination est un fournisseur Cloud alors vous devez spécifier le nom du conteneur.</td>
			<td>Non</td>
			<td>String</td>
		</tr>
	</tbody>
</table>

## Télécharger un fichier

#### Usage

Pour télécharger un fichier, vous devez insérer un formulaire dans votre vue. Ce formulaire va permettre à l'utilisateur de séléctionner le fichier qu'il souhaite télécharger il doit être de type multipart form.

	< ?php echo form_open_multipart('your-module/upload');? >
		<input type="file" name="userfile" />
	< ?php echo form_close(); ? >

Maintenant dans votre contrôleur :

	Files::upload($folder_id, $name);

Maintenant la partie agréable : si le dossier dans lequel vous télécharger votre fichier est un dossier hébergé par un fournisseur cloud, le fichier sera téléchargé sur cet espace sans effort de votre part.

#### Paramètres

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Description</th>
			<th>Requis</th>
			<th>Type</th>
		</tr>
		<tr>
			<td>$folder_id</td>
			<td>l'id du dossier cible.</td>
			<td>Oui</td>
			<td>Integer</td>
		</tr>
		<tr>
			<td>$name</td>
			<td>Le nom donné au fichier. Par défaut le fichier chargé prend le nom du fichier.</td>
			<td>Non</td>
			<td>String</td>
		</tr>
		<tr>
			<td>$field</td>
			<td>Le nom du champ input. Par défaut 'userfile'.</td>
			<td>Non</td>
			<td>String</td>
		</tr>
		<tr>
			<td>$width</td>
			<td>Si vous souhaitez redimensionner l'image pendant le téléchargement vous pouvez passer la largeur souhaitée.</td>
			<td>Non</td>
			<td>Integer</td>
		</tr>
		<tr>
			<td>$height</td>
                        <td>Si vous souhaitez redimensionner l'image pendant le téléchargement vous pouvez passer la largeur souhaitée.</td>
			<td>Non</td>
			<td>Integer</td>
		</tr>
		<tr>
			<td>$ratio</td>
			<td>En redimensionnant l'image est-ce que l'outil doit essayer de garder le même ratio largeur/hauteur?</td>
			<td>Non</td>
			<td>Boolean</td>
		</tr>
	</tbody>
</table>

## Méthodes disponibles

    // Créer un dossier virtuel
    create_folder($parent = 0, $name = 'Untitled Folder', $location = 'local', $remote_container = '')

    // Vérifier qu'un conteneur est disponible sur l'espace de stockage à distance
    check_container($name, $location)

    // Créer un conteneur dans un espace de stockage à distance
    create_container($container, $location, $folder_id = 0)

    // Récupérer le contenu d'un dossier
    folder_contents($folder_id = 0)

    // Récupérer un tableau multidimensionnel de tout les dossiers virtuels
    folder_tree()

    // Renommer un dossier virtuel
    rename_folder($id = 0, $name)

    // Supprimer un dossier virtuel
    delete_folder($id)

    // Télécharger un fichier
    upload($folder_id, $name = FALSE, $field = 'userfile', $width = FALSE, $height = FALSE, $ratio = FALSE)

    // Renommer un fichier local (default) ou déplacer des fichiers entre un emlacement local et un espace de stockage à distance
    move($file_id, $new_name = FALSE, $location = FALSE, $new_location = 'local', $container = '')

    // Récupérer un fichier par nom ou par id
    get_file($identifier = 0)

    // Récupérer tout les enregistrements de fichiers enregistrés en base de données
    get_files($location = 'local', $container = '')

    // Lister tout les fichiers physiques. Ne dépend pas des données enregistrées en base
    list_files($location = 'local', $container = '')

    // Rafraîchir les entrées en base de données pour ce dossier. Récupères les nouveaux fichier de l'espace de stockage distant et supprime les fichiers qui n'existent plus.
    synchronize($folder_id)

    // Renommer un fichier simultanément en base de données et physiquement si c'est fichier local. Change l'enregistrement si c'est un fichier sur un espace cloud
    rename_file($id = 0, $name)

    // Supprimer un fichier
    delete_file($id = 0)

    // Rechercher un dossier ou un fichier par termes. Retourne [limit] pour chaque
    search($search = '', $limit = 5)
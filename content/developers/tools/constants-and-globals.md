# Constantes et Globales

Un nombre de constantes et de propriétés sont accessibles sous PyroCMS.

## Constantes PHP

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Nom</th>
			<th>
				Sorties</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				ADDONPATH</td>
			<td>
				addons/default/</td>
			<td>
				le chemin au dossier Extensions Utilisateur.&nbsp;</td>
		</tr>
		<tr>
			<td width="100">
				APPPATH</td>
			<td>
				system/pyrocms/</td>
			<td>
				Le chemin au dossier application.</td>
		</tr>
		<tr>
			<td width="100">
				APPPATH_URI</td>
			<td>
				/system/pyrocms/</td>
			<td>
				Le chemin vers le dossier application avec un slash de début.</td>
		</tr>
		<tr>
			<td width="100">
				BASE_URL</td>
			<td>
				http://site.com/</td>
			<td>
				L'équivalent de la fonction base_url() pour CodeIgniter. Reste la même avec ou sans mod_rewrite.</td>
		</tr>
		<tr>
			<td width="100">
				BASE_URI</td>
			<td>
				/</td>
			<td>
				La Racine relative.</td>
		</tr>
		<tr>
			<td width="100">
				CURRENT_LANGUAGE</td>
			<td>
				fr</td>
			<td>
				Affiche le code de langue du langage actuellement sélectionné..</td>
		</tr>
		<tr>
			<td width="100">
				FCPATH</td>
			<td>
				/var/www/site_folder/</td>
			<td>
				Le chemin vers index.php</td>
		</tr>
		<tr>
			<td width="100">
				ADMIN_THEME</td>
			<td>
				pyrocms</td>
			<td>
				Affiche le slug du thème d'administration qui est actuellement utilisé.</td>
		</tr>
		<tr>
			<td width="100">
				SHARED_ADDONPATH</td>
			<td>
				addons/shared_addons/</td>
			<td>
				Le chemin vers les dossiers addons qui sont partagés parmis tout les sites. Les extensions sont également disponibles au site par défaut dans la version gratuite.</td>
		</tr>
		<tr>
			<td width="100">
				SITE_REF</td>
			<td>
				default</td>
			<td>
				Peut être utilisé pour trouver quel site fonctionne actuellement. Ne peut pas être utilisé pour l'installation ou la désinstallation ceci ne fonctionnerait pas pour la version professionnelle. Utilisez $this-&gt;site_ref ici pour assurer une compatibilité complète.</td>
		</tr>
		<tr>
			<td width="100">
				UPLOAD_PATH</td>
			<td>
				uploads/default/</td>
			<td>
				Le chemin vers le dossier uploads. Ne peut pas être utilisé pour l'installation ou la désinstallation ceci ne fonctionnerait pas pour la version professionnelle. Utilisez $this-&gt;upload_path ici pour assurer une compatibilité complète.</td>
		</tr>
	</tbody>
</table>

## Variables Globales PHP

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Nom</th>
			<th>
				Sortie</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;controller</td>
			<td>
				admin, blog, rss, etc</td>
			<td>
				Le nom du contrôleur courant.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;method</td>
			<td>
				index, create, etc</td>
			<td>
				Le nom de la méthode courante.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;module</td>
			<td>
				blog</td>
			<td>
				Le slug du module courant ou une chaîne de caractère vide si la page courante est une page du panneau d'administration, fonctions d'authentification, etc.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;permissions</td>
			<td>
				array</td>
			<td>
				La liste des modules que l'utilisateur peut consulter. Si des rôles sont définis pour un module il contiendrons des permissions paramétrables.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;current_user</td>
			<td>
				un objet</td>
			<td>
				Toutes les informations utilisateurs (groupes, utilisateurs et profils) de l'utilisateur courant ou un tableau vide (empty array) si aucun utilisateur n'est connecté.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;theme_options</td>
			<td>
				un objet</td>
			<td>
				Toutes les options du Thème pour le Thème d'administration. Disponible uniquement sur la version professionnelle.</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;site_ref</td>
			<td>
				default</td>
			<td>
				<strong>Disponible uniquement dans un fichier details.php d'un module.</strong> Dans vos modules utilisez la constante PHP SITE_REF</td>
		</tr>
		<tr>
			<td width="100">
				$this-&gt;upload_path</td>
			<td>
				uploads/default/</td>
			<td>
				<strong>Disponible uniquement dans un fichier details.php d'un module.</strong> Dans vos modules utilisez la constante PHP UPLOAD_PATH</td>
		</tr>
	</tbody>
</table>

## Variables Globales JavaScript

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>
				Nom</th>
			<th>
				Sortie</th>
			<th>
				Disponible</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td width="100">
				APPPATH_URI</td>
			<td>
				/system/pyrocms/</td>
			<td>
				administration et site</td>
			<td>
				Le chemin vers le dossier système</td>
		</tr>
		<tr>
			<td width="100">
				BASE_URI</td>
			<td>
				/</td>
			<td>
				administration et site</td>
			<td>
				Le racine relative.</td>
		</tr>
		<tr>
			<td width="100">
				BASE_URL</td>
			<td>
				http://site.com</td>
			<td>
				admin</td>
			<td>
				L'adresse du site. N'est pas modifié par mod_rewrite.</td>
		</tr>
		<tr>
			<td width="100">
				DEFAULT_TITLE</td>
			<td>
				Un-named Website</td>
			<td>
				administration</td>
			<td>
				Le nom du site.</td>
		</tr>
		<tr>
			<td width="100">
				DIALOG_MESSAGE</td>
			<td>
				Etes-vous sûr de bien vouloir supprimer ceci&nbsp;? Vous ne pourrez plus revenir en arrière.</td>
			<td>
				administration</td>
			<td>
				Le message de suppression dans la langue courante. Si vous ajoutez votre propre message. Si vous ajouter un message personnalisé au titre du bouton, il sera utilisé à la place.</td>
		</tr>
		<tr>
			<td width="100">
				SITE_URL</td>
			<td>
				http://site.com/ où http://site.com/index.php/</td>
			<td>
				administration</td>
			<td>
				Change en fonction des paramètres mod_rewrite. Identique à la fonction CodeIgniter site_url()</td>
		</tr>
		<tr>
			<td width="100">
				UPLOAD_PATH</td>
			<td>
				uploads/default/</td>
			<td>
				administration</td>
			<td>
				Le chemin vers les fichier téléchargés sur le site courant.</td>
		</tr>
	</tbody>
</table>
<p>
	&nbsp;</p>

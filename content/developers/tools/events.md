# Événements (Events)

Les Événements permettent d'ajouter vos propres fonctionnalités au noyau de PyroCMS en utilisant des hook à des moments déterminés appelés des déclencheurs (Triggers).
Il existe plusieurs triggers déjà en place dans le noyau PyroCMS qui vous permettent d'exécuter vos propres codes alors que d'autres parties de PyroCMS fonctionnent.

## Utiliser les événement dans vos modules

Créez un fichier events.php à la racine de votre module (il sera pré-chargé quand PyroCMS commence à fonctionner). Ci-dessous, un exemple issue du module "Sample":

<script src="https://gist.github.com/1373989.js?file=gistfile1.aw"></script>

Dans l'exemple ci-dessus, la classe **Events\_Sample** exécute la fonction 'run' quand le contrôleur public **public\_controller** est appelé dans PyroCMS.

Il est important de noter, que certains triggers passent des données que vous pouvez utiliser également dans vos fonctions.

## Délencheurs PyroCMS (PyroCMS Triggers)

PyroCMS inclus les triggers suivants:

### Triggers Système (Dans les emplacements autres que les modules)

<table>
<tr>
<td class="one_third">Events::trigger('<b>public_controller</b>')</td>
<td>est déclenché quand le Public_Controller commence à être utilisé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>admin_controller</b>')</td>
<td>est déclencé quand le Admin_Controller commence à être utilisé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>admin_notification</b>')</td>
<td>Est déclenché quand une erreur, une notice ou un message sont affichés dans la zone d'administration.</td>
</tr>
</table>

### Triggers Blog

<table>
<tr>
<td class="one_third">Events::trigger('<b>blog_article_deleted</b>', $deleted_ids)</td>
<td>Est déclenché quand un ou plusieurs post du blog ont été supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>blog_article_published</b>', $id)</td>
<td>Est déclenché quand un post de blog est publié.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>blog_category_deleted</b>', $deleted_ids)</td>
<td>Est déclenché quand une ou plusieurs catégories sont supprimées.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>blog_category_updated</b>', $id)</td>
<td>Est déclenché quand une catégorie de blog est mise à jour.</td>
</tr>
</table>

### Triggers du module Contact

<table>
<tr>
<td class="one_third">Events::trigger('<b>email</b>', $data, 'array')</td>
<td>Ce trigger est utilisé pour envoyer un email. Le second paramètre contient les données à envoyer, le troisième paramètre est le type de réponse que vous attendez. L'envoi est effectué par l'intermédiaire d'un événements enregistré dans system/cms/modules/templates/events.php mais vous pouvez le déclencer depuis n'impote ou dans l'application.</td>
</tr>
</table>

### Triggers Commentaires

<table>
<tr>
<td class="one_third">Events::trigger('<b>comment_approved</b>', $comment)</td>
<td>Est déclenché quand un commentaire à été approuvé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>comment_deleted</b>', $comments)</td>
<td>Est déclenché quand un ou plusieurs commentaires sont supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>comment_unapproved</b>', $id)</td>
<td>Est déclenché quand un commentaire est non approuvé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>comment_updated</b>', $id)</td>
<td>est déclenché quand un commentaire est mis à jour.</td>
</tr>
</table>

### Triggers Fichiers

<table>
<tr>
<td class="one_third">Events::trigger('<b>file_deleted</b>', $deleted)</td>
<td>Est déclenché quand un ou plusieurs fichier sont supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>file_updated</b>', $id)</td>
<td>Est déclenché quand un fichier est mis à jour.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>file_uploaded</b>', $data)</td>
<td>Est déclenché quand un fichier est chargé dans un dossier.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>file_folder_created</b>', $id)</td>
<td>Est déclenché quand un nouveau dossier est créé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>file_folder_deleted</b>', $deleted_ids)</td>
<td>Est déclenché quand un ou plusieurs dossiers ont été supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>file_folder_updated</b>', $id)</td>
<td>Est déclenché quand un quand un dossier est mis à jour.</td>
</tr>
</table>

### Triggers Groupes

<table>
<tr>
<td class="one_third">Events::trigger('<b>group_created</b>', $id)</td>
<td>Est déclenché quand un nouveau groupe est créé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>group_deleted</b>', $id)</td>
<td>Est déclenché quand un groupe est mis à jour.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>group_updated</b>', $id)</td>
<td>Est déclenché quand un groupe à été supprimé.</td>
</tr>
</table>

### Keywords Triggers

<table>
<tr>
<td class="one_third">Events::trigger('<b>keyword_created</b>', $id)</td>
<td>Est déclenché quand un Mot-Clé à été ajouté.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>keyword_deleted</b>', $id)</td>
<td>Est déclenché quand un Mot-Clé à été supprimé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>keyword_updated</b>', $id)</td>
<td>Est déclenché quand un Mot-Clé est mis à jour.</td>
</tr>
</table>

### Triggers Modules

<table>
<tr>
<td class="one_third">Events::trigger('<b>module_disabled</b>', $slug)</td>
<td>Est déclenché quand un module à été désactivé, désinstallé ou supprimé (en cliquant sur <em>désactiver</em>, <em>désinstaller</em> ou <em>supprimer</em> dans la section Extensions du panneau d'administration).</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>module_enabled</b>', $slug)</td>
<td>Est déclenché quand un module est uploadé, installé ou activé (en cliquant sur <em>installer</em> or <em>activer</em> dans la section Extensions du panneau d'administration).</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>module_upgraded</b>', $slug)</td>
<td>Est déclenché quand le module a été mis à jour.</td>
</tr>
</table>

### Triggers Navigation

<table>
<tr>
<td class="one_third">Events::trigger('<b>navigation_group_created</b>', $id)</td>
<td>Est déclenché quand le groupe de navigation a été créé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>navigation_group_deleted</b>', $deleted_ids)</td>
<td>Est déclenché quand un ou plusieurs groupes de navigation on été supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_navigation_create</b>', $input)</td>
<td>Est déclenché quand un nouvel élément de navigation a été créé.</td>
</tr>
<tr>
<tr>
<td class="one_third">Events::trigger('<b>post_navigation_delete</b>', $deleted_ids)</td>
<td>Est déclenché quand un ou plusieurs éléments de navigation ont été supprimés.</td>
</tr>
<td class="one_third">Events::trigger('<b>post_navigation_edit</b>', $input)</td>
<td>Est déclenché quand un nouveau élément de navigation a été édité.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_navigation_order</b>', array($order, $group))</td>
<td>Est déclenché quand un élément de navigation a été réordonné au sein d'un groupe.</td>
</tr>
</table>

### Triggers Pages

<table>
<tr>
<td class="one_third">Events::trigger('<b>post_page_create</b>', $input)</td>
<td>Est déclenché quand une page a été créée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_page_edit</b>', $input)</td>
<td>Est déclenché quand une page a été éditée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_page_delete</b>', $deleted_ids)</td>
<td>Est déclenché quand une ou plusieurs pages on été supprimées.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_page_order</b>', array($order, $root_pages))</td>
<td>Est déclenché quand une page est réordonnée.</td>
</tr>
</table>

### Triggers Permissions

<table>
<tr>
<td class="one_third">Events::trigger('<b>permissions_saved</b>', array($group_id, $modules, $roles))</td>
<td>Est déclenché quand des Permissions sont sauvegardées.</td>
</tr>
</table>

### Triggers Settings

<table>
<tr>
<td class="one_third">Events::trigger('<b>settings_updated</b>', $settings_stored)</td>
<td>Est déclenché quand les Paramètres sont mis à jour.</td>
</tr>
</table>

### Triggers Templates

<table>
<tr>
<td class="one_third">Events::trigger('<b>email_template_created</b>', $id)</td>
<td>Est déclenché quand un nouveau modèle d'email a été créé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>email_template_deleted</b>', $id)</td>
<td>Est déclenché quand un modèle d'email à été supprimé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>email_template_updated</b>', $id)</td>
<td>Est déclenché quand un modèle d'email a été mis à jour.</td>
</tr>
</table>

### Triggers Themes

<table>
<tr>
<td class="one_third">Events::trigger('<b>theme_deleted</b>', $deleted_names)</td>
<td>Est déclenché quand un ou plusieurs thèmes ont été supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>theme_options_updated</b>', $options_array)</td>
<td>Est déclenché quand les options du Thème sont mise à jour.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>theme_set_default</b>', $theme)</td>
<td>Est déclenché quand un thème par défaut est défini.</td>
</tr>
</table>

### Triggers Users

<table>
<tr>
<td class="one_third">Events::trigger('<b>post_user_activation</b>', $id)</td>
<td>Est déclenché quand un utilisateur active son compte en cliquant sur le lien d'activation reçu dans l'email d'activation du compte. L'ID utilisateur est passé dans votre événement.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_user_login</b>')</td>
<td>Est déclenché immédiatement après qu'un utilisateur se soit connecté via nomdedomaine.com/users/login</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_user_register</b>', $id)</td>
<td>Est déclenché immédiatement après qu'un utilisateur se soit enregistré. L'ID du nouvel utilisateur créé est passé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>post_user_update</b>')</td>
<td>Est executé après qu'un profil utilisateur à été édité et sauvegardé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>pre_user_logout</b>')</td>
<td>Est executé juste avant q'une session utilisateur soit détruite.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>user_created</b>', $user_id)</td>
<td>Est executé quand un nouvel utilisateur a été créé.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>user_deleted</b>', $deleted_ids)</td>
<td>Est exécuté quand un ou plusieurs utilisateurs ont été supprimés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>user_updated</b>', $id)</td>
<td>Est déclenché quand un utilisateur a été mis à jour.</td>
</tr>
</table>

### Triggers Widgets

<table>
<tr>
<td class="one_third">Events::trigger('<b>widget_area_created</b>')</td>
<td>Est déclenché quand une zone Widget a été créée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_area_deleted</b>', $id)</td>
<td>Est déclenché quand une zone Widget a été supprimée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_area_updated</b>', $id)</td>
<td>est déclenché quand une zone Widget a été mise à jour.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_disabled</b>', $ids)</td>
<td>Fired when one or more widget instances have been disabled.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_enabled</b>', $ids)</td>
<td>Est déclenché quand une ou plusieurs instances de Widget ont été activés.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_instance_created</b>', $id)</td>
<td>Est déclenché quand une instance de Widget a été créée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_instance_deleted</b>', $id)</td>
<td>Est déclenché quand une instance de Widget a été supprimée.</td>
</tr>
<tr>
<td class="one_third">Events::trigger('<b>widget_instance_updated</b>', $id)</td>
<td>Est déclenché quand une instance de Widget a été mis à jour.</td>
</tr>
</table>
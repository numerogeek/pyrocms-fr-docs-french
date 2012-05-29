# Tags user

Le plugin <em>user</em> vous permet d'accéder aux données des utilisateurs et la logique.

## user:logged_in

	{{ noparse }}{{ user:logged_in }}{{ /noparse }}

Vérifie si l'utilisateur est connecté ou non. Peut être utilisé comme un tag pair pour limiter l'affichage de certain code d'utilisateurs enregistrés, ou un tag unique qui renvoie TRUE ou FALSE selon que l'utilisateur est connecté po

### Attributs

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Nom</th>
			<th>Default</th>
			<th>Requis</th>
			<th>Description</th>
		</tr>
		<tr>
			<td width="100">group</td>
			<td width="100">None</td>
			<td width="100">Non</td>
			<td>Group slug. Vérifie si un utilisateur est non seulement connecté, mais aussi un membre du groupe spécifié.</td>
		</tr>
	</tbody>
</table>

### Exemple

	{{ noparse }}{{ if user:logged_in }}
	&lt;p&gt;This is just for logged in users.&lt;/p&gt;
{{ endif }}{{ /noparse }}

## user:not\_logged\_in

	{{ noparse }}{{ user:not_logged_in }}{{ /noparse }}

Identique à la fonction précédente, mais au lieu vérifier si un utilisateur n'est pas connecté. Prend également le paramètre _group_. Doivent être utilisés dans un tag pair.

## Variables simples de profil utilisateur

Le plugin user vous donne également accès à des variables des différents users utilisant la syntaxe suivante:

	{{ noparse }}{{ user:<em>variable</em> }}{{ /noparse }}

Ces appels par défaut au user connecté, mais vous pouvez également spécifier l'ID d'un user avec le paramètre <em>user_id</em>:

	{{ noparse }}{{ user:<em>variable</em> user_id="4" }}{{ /noparse }}

Si vous utilisez des champs de flux personnalisés qui retournent plusieurs enregistrements, vous pouvez accéder aux valeurs à l'intérieur comme des tag pairs:

	{{ noparse }}{{ user:country }}{{ name }} {{ /user:country }}{{ /noparse }}

Voici un tableau de variables qui sont codées en dur dans le système et toujours disponible.

<table cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<th>Variable</th>
			<th>Notes</th>
		</tr>
		<tr>
			<td width="200">id</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">group_id</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">ip_address</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">active</td>
			<td>1 or 0.</td>
		</tr>
		<tr>
			<td width="200">activation_code</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">created_on</td>
			<td>Unix epoch format.</td>
		</tr>
		<tr>
			<td width="200">last_login</td>
			<td>Unix epoch format.</td>
		</tr>
		<tr>
			<td width="200">username</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">display_name</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">forgotten_password_code</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">remember_code</td>
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td width="200">group</td>
			<td>Group slug.</td>
		</tr>
		<tr>
			<td width="200">group_description</td>
			<td>Group name.</td>
		</tr>
	</tbody>
</table>

## user:profile

Mis à part l'accès à des champs du profil utilisateur individuel, vous pouvez également y accéder en utilisant la fonction de profil. A l'intérieur du tag pair, vous pouvez accéder à l'une des variables de profil utilisateur, y compris vos champs personnalisés.

	{{ noparse }}{{ user:profile }}

	{{ display_name }}

	{{ custom_field }}

	{{ custom_field:sub_value }}

{{ /user:profile }}{{ /noparse }}

La balise de profil prend également une valeur facultative user_id.

	{{ noparse }}{{ user:profile user_id="4" }}{{ /noparse }}

## user:profile\_fields

Dans le cas où vous voulez juste vous montrer toutes les données de profil utilisateur dans une liste, vous pouvez le faire avec cette fonction. Chaque élément de données utilisateur peuvent être accessibles via les variables suivantes:

<table>
	<tr>
		<td>value</td>
		<td>La valeur du champs. Pour les champs du profil utilisateur qui retournent plusieurs valeurs, ce sera l'affichage alternatif canonique que les types de terrain peut et doit fournir.</td>
	</tr>
	<tr>
		<td>name</td>
		<td>Nom du champs .</td>
	</tr>
	<tr>
		<td>slug</td>
		<td>champs slug.</td>
	</tr>
</table>

	{{ noparse }}{{ user:profile_fields }}

	&lt;p>&lt;strong>{{ name }}: {{ value }}&lt;/strong>&lt;/p>

{{ /user:profile_fields }}{{ /noparse }}

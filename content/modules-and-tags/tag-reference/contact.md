# Contact

Cette balise affiche un formulaire de contact où les visiteurs peuvent vous envoyer un email sans voir votre adresse e-mail

	{{ noparse }}{{ contact:form }}{{ /noparse }}
    
### Attributes

<table cellpadding="0" cellspacing="0">
    <tbody>
        <tr>
			<th>
				Nom</th>
			<th>
				Default</th>
			<th>
				Requis</th>
			<th>
				Description</th>
		</tr>
        <tr>
			<td width="100">
				wildcard</td>
			<td width="100">
				None</td>
			<td width="100">
				Non</td>
			<td>
				Vous devez spécifier les noms des champs que vous
                 voulez dans le formulaire. Ils doivent être dans la suivante
                 format: field-name = "type | rules».
                 Les types valides sont les suivants: text, textarea, fila, et dropdown.
            </td>
		</tr>
        <tr>
			<td width="100">
				max-size</td>
			<td width="100">
				None</td>
			<td width="100">
				Non</td>
			<td>
                La taille en ko de pièces jointes permise
            </td>
		</tr>
        <tr>
			<td width="100">
				reply-to</td>
			<td width="100">
				None</td>
			<td width="100">
				Non</td>
			<td>
                L'adresse email à utiliser pour la réponse au message. Si un champ email est ajouté , il sera utilisé à la place
            </td>
		</tr>
        <tr>
			<td width="100">
				button</td>
			<td width="100">
				Send</td>
			<td width="100">
				Non</td>
			<td>
                Le texte à afficher sur le bouton submit.
            </td>
		</tr>
        <tr>
			<td width="100">
				template</td>
			<td width="100">
				contact</td>
			<td width="100">
				Non</td>
			<td>
                Email template slug à utiliser pour envoyer l'e-mail de contact.
            </td>
		</tr>
        <tr>
			<td width="100">
				lang</td>
			<td width="100">
				en</td>
			<td width="100">
				Non</td>
			<td>
                 version de modèle d'email à utiliser pour
                 cette instance du formulaire de contact.
            </td>
		</tr>
        <tr>
			<td width="100">
				to</td>
			<td width="100">
				Site Contact Email</td>
			<td width="100">
				Non</td>
			<td>
                L'adresse email de l'envoi. Par défaut, le contact
                 e-mail dans CP> Paramètres.
            </td>
		</tr>
        <tr>
			<td width="100">
				from</td>
			<td width="100">
				Site Server Email</td>
			<td width="100">
				Non</td>
			<td>
               Cette adresse sera dans le from.
            </td>
		</tr>
        <tr>
			<td width="100">
				sent</td>
			<td width="100">
				Translated string found in lang file</td>
			<td width="100">
				Non</td>
			<td>
                Ce message est affiché à l'utilisateur après avoir
                envoyé un message. Utilisez cette option pour définir un message personnalisé.
            </td>
		</tr>
        <tr>
			<td width="100">
				error</td>
			<td width="100">
				Traduction trouvé dans le fichier de langue</td>
			<td width="100">
				Non</td>
			<td>
                Définir un message d'erreur personnalisé ici. Il permet d'afficher si
                 il ya une erreur de serveur lors de l'envoi de l'email.
            </td>
		</tr>
        <tr>
			<td width="100">
				success-redirect</td>
			<td width="100">
				Page Courante</td>
			<td width="100">
				Non</td>
			<td>
                Définir les segments url ici si vous souhaitez que l'utilisateur soit envoyé à
                 sur autre page après un envoi avec succès.
            </td>
		</tr>
    </tbody>
</table>

### Exemple

    {{ noparse }}{{ contact:form
    name = &quot;text|required&quot;
    email = &quot;text|required|valid_email&quot;
    subject = &quot;dropdown|required|hello=Say Hello|support=Support Request|Something Else&quot;
    message = &quot;textarea|required&quot;
    attachment = &quot;file|jpg|png|zip&quot;
}}
    {{ name }}
    {{ email }}
    {{ subject }}
    {{ message }}
    {{ attachment }}
{{ /contact:form }}{{ /noparse }}

### Exemple Avancé

    {{ noparse }}{{ contact:form
    name = &quot;text|required&quot;
    email = &quot;text|required|valid_email&quot;
    subject = &quot;dropdown|required|hello=Say Hello|support=Support Request|Something Else&quot;
    message = &quot;textarea|required&quot;
    attachment = &quot;file|jpg|png|zip&quot;
    max_size = &quot;10000&quot;
    reply-to = &quot;visitor@somewhere.com&quot; * Read note below *
    button = &quot;send&quot;
    template = &quot;contact&quot;
    lang = &quot;en&quot;
    to = &quot;contact@site.com&quot;
    from = &quot;server@site.com&quot;
    sent = &quot;Your message has been sent. Thank you for contacting us&quot;
    error = &quot;Sorry. Your message could not be sent. Please call us at 123-456-7890&quot;
    success-redirect = &quot;home&quot;
}}
    {{ name }}
    {{ email }}
    {{ subject }}
    {{ message }}
    {{ attachment }}
{{ /contact:form }}{{ /noparse }}

Si il ya un champ "email" dans le formulaire, il sera utilisé pour la réponse à aborder. Votre formulaire doit avoir une
adresse de réponse ou bien le formulaire doit contenir un champ "email".
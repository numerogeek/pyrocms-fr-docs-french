# Driver Flux (Streams Driver)

Le driver streams est utilisé pour créer et manipuler des flux. les flux représentent des tableaux de données dans la base de données.

Vous pouvez appeler le driver streams ainsi:

	$this->streams->streams->function();
	
## Champs Prédéfinis

Quand vous créer un flux, les champs suivants sont créé automatiquement.

<table>
	<tr>
		<td width="25%"><strong>id</strong>
		<td>une clé primaire auto-incrémentée ID.</td>
	</tr>
	<tr>
		<td><strong>created</strong>
		<td>Un champ MySQL de type DATETIME qui enregistre la date de création de l'entrée.</td>
	</tr>
	<tr>
		<td><strong>updated</strong>
		<td>Un champ MySQL de type DATETIME qui enregistre la date de mise à jour de l'entrée.</td>
	</tr>
	<tr>
		<td><strong>created_by</strong>
		<td>id de l'utlisateur qui a initialement créé cette entrée.</td>
	</tr>
	<tr>
		<td><strong>ordering_count</strong>
		<td>Incrément numérique qui permet d'ordonner les éléments.</td>
	</tr>
</table>

## add_stream(<var>$stream\_name, $stream\_slug, $namespace, $prefix = NULL, $about = NULL</var>)

La fonction **add_stream** permet de créer un flux. Il créera la table en base de données, ainsi que les métadonnées du flux dans la table streams.
	
### Paramètres

<table>
	<tr>
		<td width="25%"><strong>stream_name</strong>
		<td>Le nom complet du flux.</td>
	</tr>
	<tr>
		<td><strong>stream_slug</strong>
		<td>Le slug du flux.</td>
	</tr>
	<tr>
		<td><strong>namespace</strong>
		<td>L'espace de nom de votre flux.</td>
	</tr>
	<tr>
		<td><strong>prefix</strong>
		<td>Optionnel. Un préfixe de flux. Sera utilisé comme nom de table dans la base de données.</td>
	</tr>
	<tr>
		<td><strong>about</strong>
		<td>Optionnel. Une description courte du flux.</td>
	</tr>
</table>

### Exemple:

Dans cet exemple, nous ajoutons un flux FAQ. Le module s'appelant "faqs", notre espace de nom sera appelé "faq". Nous ne fournissons pas de préfixe dans ce cas, nous créons ainsi une table **default_faqs**. Si nous paramétrons un préfixe par exemple 'faq_' la table créée sera **default\_faq\_faqs**.

	$this->streams->streams->add_stream('FAQ', 'faqs', 'stream_sample', 'faq_', null);

## get_stream(<var>$stream\_slug, $namespace</var>)

Récupère les données d'un flux. Cette fonction ne récupère pas les entrées, seulement les métadonnées du flux.
	
### Exemple:

	$this->streams->streams->get_stream('faqs', 'streams_sample');

Retourne:
	
	stdClass Object
	(
	    [id] => 18
	    [stream_name] => FAQs
	    [stream_slug] => faqs
	    [stream_namespace] => streams_sample
	    [stream_prefix] => sample_
	    [about] => 
	    [view_options] => Array
	        (
	            [0] => id
	            [1] => created
	        )
	
	    [title_column] => question
	    [sorting] => title
	)
	
<div class="tip"><strong>Note:</strong> The view options column is an array of the columns that are shown when listing entries in a table. 'id' and 'created' are the default values.</div>

## get_streams(<var>$namespace</var>)

Gets basic data about all the streams in a namespace.

### Example:

	$this->streams->streams->get_streams('streams_sample');
	
Returns:

	Array
	(
	    [0] => stdClass Object
	        (
	            [id] => 18
	            [stream_name] => FAQs
	            [stream_slug] => faqs
	            [stream_namespace] => streams_sample
	            [stream_prefix] => sample_
	            [about] => 
	            [view_options] => Array
	                (
	                    [0] => id
	                    [1] => created
	                )
	
	            [title_column] => question
	            [sorting] => title
	        )
	)

## update_stream(<var>$stream, $namespace, $data</var>)

Allows you to update basic stream metadata. You can pass any stream metadata value and it will handle the necessary changes, so you can give it a new stream slug and it will update the metadata and update the table name. Returns BOOL.

### Example:

	$update_data = array(
		'stream_slug'	=> 'the_faqs',
		'about'			=> 'A list of frequently asked questions.',
		'view_options'	=> array('question')
	);
	
	$this->streams->streams->update_stream('faqs', 'streams_sample', $update_data);

## delete_stream(<var>$stream\_slug, $namespace</var>)

Deletes a stream. This will delete all the entries associated with this stream as well, as well as run all of the field destruct functions for fields assigned to this stream.

This streams returns TRUE or FALSE, based on whether the streams was successfully deleted.
		
### Example:

	$this->streams->streams->delete_stream('faqs', 'streams_sample');

## get_assignments(<var>$stream, $namespace</var>)

Gets assignments for a stream. More information forthcoming.

### Example:

	$this->streams->streams->get_assignments('faqs', 'streams_sample');
	
Returns:

	Array
	(
	    [0] => stdClass Object
	        (
	            [id] => 10
	            [stream_name] => FAQs
	            [stream_slug] => faqs
	            [stream_namespace] => streams_sample
	            [stream_prefix] => sample_
	            [about] => 
	            [title_column] => question
	            [sorting] => title
	            [stream_view_options] => a:2:{i:0;s:2:"id";i:1;s:7:"created";}
	            [stream_id] => 18
	            [field_id] => 10
	            [field_name] => Question
	            [field_slug] => question
	            [field_namespace] => streams_sample
	            [field_type] => text
	            [field_data] => a:1:{s:10:"max_length";i:200;}
	            [field_view_options] => 
	        )
	
	    [1] => stdClass Object
	        (
	            [id] => 11
	            [stream_name] => FAQs
	            [stream_slug] => faqs
	            [stream_namespace] => streams_sample
	            [stream_prefix] => sample_
	            [about] => 
	            [title_column] => question
	            [sorting] => title
	            [stream_view_options] => a:2:{i:0;s:2:"id";i:1;s:7:"created";}
	            [stream_id] => 18
	            [field_id] => 11
	            [field_name] => Answer
	            [field_slug] => answer
	            [field_namespace] => streams_sample
	            [field_type] => textarea
	            [field_data] => a:0:{}
	            [field_view_options] => 
	        )
	)
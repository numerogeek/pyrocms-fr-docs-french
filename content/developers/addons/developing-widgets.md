# Developing Widgets

Les widgets sont assez semblables aux Plugins href="/docs/glossary#plugins"> </ a> dans la façon dont ils sont insérés dans le contenu, mais ils sont un peu plus "intelligent". Ils permettent au client ou de l'administrateur de gérer des morceaux de contenu "intelligent" sur ​​leur site sans avoir à apprendre des tas de tags, HTML ou si vous appelez à la rescousse.

<a href="/docs/glossary#widget-areas">Widget Areas</a> can be defined (header, sidebar, blog page footers, etc) then Widget Instances can be added in them. Available Widgets currently include HTML blocks, Twitter Feeds, RSS Feeds, Google Maps and Social Bookmarks. More will be included over time, and you can make your own very easily.


<a href="/docs/glossary#widget-areas">Les domaines Widget </ a> peut être définie (en-tête, encadré, pieds de page de blog, etc), alors des instances Widget peut être ajouté en eux. Les Widgets disponibles actuellement comprennent des blocs HTML, flux Twitter, flux RSS, Google Maps et Social Bookmarks. Plus ils seront inclus dans le temps, et vous pouvez faire votre propre widget très facilement.


##Où puis-je mettre mes widgets?

Les widgets peuvent être stockés directement dans trois endroits

* Dans le dossier /addons/widgets
* Dans le dossier /addons/widgets/*&lt;widget-name&gt;* 
* ou à l'intérieur d'un dossier de module par exemple: /addons/modules/*&lt;module-name&gt;/widgets/&lt;widget-name&gt;*

## Quelles sont les principales composantes d'un widget

Les principaux composants d'un widget sont:

* la classe du widget.
* views/form.php &ndash; une vue qui sera rendue dans l'interface d'admin widget.
* views/display.php &ndash; une vue qui sera utilisé pour rendre la production dans le contenu du site frontend.

## Comment doit être structuré un widget?

Par exemple, disons que nous voulons créer un widget appelé "awesome_sauce". Notre structure serait en tant que telle:

    - awesome_sauce (folder)
      * awesome_sauce.php (widget class)
      - views (folder)
          * form.php (admin view)
          * display.php (frontend view)

Nous allons maintenant expliquer chaque composant de façon plus détaillée:

### La classe du widget

S'il vous plaît saisissez cette occasion pour lire le code ci-dessous et prendre note des commentaires.

    <?php if (!defined('BASEPATH')) exit('No direct script access allowed');

    class Widget_Awesome_sauce extends Widgets
    {
	    // The widget title,  this is displayed in the admin interface
	    public $title = 'Awesome Sauce';

	    //The widget description, this is also displayed in the admin interface.  Keep it brief.
	    public $description =  'Display sauce that is awesome.';

	    // The author's name
	    public $author = 'Some Guy';

	    // The authors website for the widget
	    public $website = 'http://example.com/';

	    //current version of your widget
	    public $version = '1.0';

    	/**
    	 * $fields array fore storing widget options in the database.
	     * values submited through the widget instance form are serialized and
	     * stored in the database.
	     */
	    public $fields = array(
		    array(
		    	'field'   => 'field_name',
		    	'label'   => 'field_label',
		    	'rules'   => 'required'
		    )
	    );
    
	    /**
	     * the $options param is passed by the core Widget class.  If you have
	     * stored options in the database,  you must pass the paramater to access
	     * them.
	     */
	    public function run($options)
	    {
		    if(empty($options['field_name']))
    		{
	    		//return an array of data that will be parsed by views/display.php
                return array('output' => '');
	        }
        
            // Store the feed items
		    return array('output' => $options['html']);
	    }

        /**
	     * form() is used to prepare/pass data to the widget admin form
	     * data returned from this method will be available to views/form.php
	     */
	    public function form()
	    { 
	        $stuff = $this->db->get_stuff();
            return array('stuff' => $stuff);
	    }
    }

Si vous êtes arrivé à ce point et avez  lu les commentaires du code ci-dessus qui devraient à peu près vous mettre sur la bonne voie pour la création de votre premier widget. Cependant, je tiens à souligner une chose avant de passer à la suite.

Le nom de la classe widget doit être dans le format suivant: "**Widget_Awesome_sauce**" and doit étendre de la class core "**Widgets**" .

### Les fichiers vues

Pas grand chose à dire ici d'autre que les fichiers de vues doivent être des vues partielles seulement. Les vues ne doivent pas inclure html, body, header. Les fichiers de vues doit aussi être nommé respectivement **form.php** et **display.php**.

## Exemple d'utilisation

Tout ce que vous devez faire pour que cela fonctionne, c'est d'ouvrir une présentation thématique ou la mise en page et entrez:

    {{ noparse }}
{{ pyro:widgets:area slug="sidebar" }}
    {{ /noparse }}
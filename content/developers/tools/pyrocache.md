# PyroCache


PyroCMS takes Caching very seriously as it can make a massive difference between a quick site and something that takes so long to load people give up. We use the library PyroCache (renamed recently to avoid conflicting with the <a href="http://codeigniter.com/user_guide/libraries/caching.html" target="_blank">Cache class</a> added in CodeIgniter Reactor). The benefit of using PyroCache over the built in Cache class is that it had simple model and library call modes.

Vous ne comprennez pas à quoi ça sert ? regardez l'exemple. Voici un appel à module sans utilisation du cache:

	$this->blog_m->get_posts($category_id, 'live');

Voici un appel à un module avec prise en charge du cache:

	$this->pyrocache->model('blog_m', 'get_posts', array($category_id, 'live'), 120); // garder 2 minutes 

	// Garder définitivement
	$this->pyrocache->library('some_library', 'calculate_something', array($foo, $bar, $bla)); // garder pour un temps donné par défaut (0 = unlimited)

	// Vider / Supprimer le cache pour une librairie ou un modèle
	$this->pyrocache->delete_all('some_library');


This is basically a really simple way to wrap your model and library calls with cache logic to save you having to manually check expiry dates and the like. If you feel like doing it manually or are dealing with caching that is not inside a model or library method then you can do things the old fashioned way too:

    if ( ! $data = $this->pyrocache->get('cached-name'))
    { 
        $data = $this->some_library->massive_query();
        $this->pyrocache->write($data, 'cached-name');
    }

    $this->pyrocache->delete('cached-name');

### Where is the cache saved?

This cache data is saved in **system/pyrocms/cache** and will have a name that matches the model or library that is provided. The actual cache file will be an encryption of the method name, the parameters passed to the method and a few other things. The file will not be web readable so no data could be read by unauthorised people. It can only be added and edited by PHP, or by you as a root user.</p>

### How can I clear the cache?</h4>

If you are using a *nix system then you will want to use the following command:</p>
	
	sudo rm -rf systems/pyrocms/cache/*_m</pre>

This will remove any cached models. To remove a library, mention the name instead of *_m.</p>

### Puis-je utiliser Memcache, XCache, etc. quand j'utilise PyroCache ?

Non, pour cela vous devez utiliser la <a href="http://codeigniter.com/user_guide/libraries/caching.html" target="_blank">classe Cache</a> de CodeIgniter.
Nope, for that you need to work with the <a href="http://codeigniter.com/user_guide/libraries/caching.html" target="_blank">Cache class</a> in CodeIgniter Reactor. It does not have the model/library call features, but will let you work with multiple caching mechanisms very easily.
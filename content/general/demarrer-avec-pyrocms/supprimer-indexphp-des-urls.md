# Supprimer index.php des URLs

Pendant l'installation, PyroCMS vous demandera si vous avez Apache [mod_rewrite](http://httpd.apache.org/docs/current/mod/mod_rewrite.html) installé. Ceci fait partie des options du Framework 
[CodeIgniter](http://www.codeigniter.com).

Dans CodeIgniter, tout transite par le fichier index.php, donc votre url devrait ressembler à :

     http://www.example.com/index.php/about

Evidemment, vous souhaitez retirer index.php, et vous pouvez le faire dans le .htaccess avec le mod_rewriter activé.

Pour retirer l'index.php, créez un fichier .htaccess à la racine de votre PyroCMS.
[En savoir plus sur .htaccess](http://httpd.apache.org/docs/current/howto/htaccess.html), dans notre cas on va juste retirer l'index.php de l'addresse url.

Tous les serveurs web ne fonctionnent pas de la même façon, mais quelque chose dans ce genre devrait fonctionner :

    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ /index.php?/$1 [L]



Votre URL parait plus belle : 

     http://www.example.com/about

Si vous avez choisi de ne pas activer le mod_rewrite pendant l'installation et que vos url continue d'ajouter l'index.php, ouvrez le fichier **system/cms/config/config.php** et changez:

     $config['index_page'] = 'index.php';

avec:

     $config['index_page'] = '';

PyroCMS ne prefixera plus l'index.php :)

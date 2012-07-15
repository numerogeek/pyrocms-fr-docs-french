# Structure de base d'un Module

PyroCMS est conçu pour être modulaire, et créer des modules avec PyroCMS est un processus assez simple.
Les modules de bases se trouvent dans <def>system/pyrocms/modules</def> et vous pouvez en installer de nouveau dans <def>addons/default/modules</def> ou <def>addons/shared_addons/modules</def>.
tous les modules que vous créez doivent se trouver dans un de ces deux répertoires. Surtout pas dans system/cms/modules.


Chaque module peut contenir les répertoires suivants :

* config
* controllers
* helpers
* libraries
* models
* views
* js
* css
* img

Si un module a besoin d'avoir un front-end (quelque chose qui s'affiche pour les internautes), alors il doit avoir au moins un controlleur etg il doit être nommé comme le module. Exemple : 

	addons/<site-ref>/modules/blog/controllers/blog.php

## Le fichier details.php du module.

Chaque module doit contenir un fichier detail.php qui contient le nom du module, la description, version, si c'est disponible pour la backend et/ou frontend, les menus admin etc... Si vous concevez un module avec le backend => false alors il n'y aura pas de menu dans le panneau de configuration du site. De la même manière, frontend=>false n'affichera rien dans la navigation pour les internautes

Lorsque le CP > Extensions est chargé ou lorsque PyroCMS s'installe, il indexe tout les fichiers details.php et charge les données depuis la méthode info() de la table default_modules. Si vous faites des changements dans ce fichier, il ne seront pas pris en compte tant que vous n'avez pas réinstallé le module. Une exception : Les sections et raccourcis de menu dans le panneau d'administration. Il sont chargés en permanence.

Vous devez utiliser $ this-> db-> dbprefix ('table_name') lors de l'exécution des requêtes manuelles. Cela permet de s'assurer que le module utilise la table de base de données correctement et que tous les noms de tables sont précédées d'un "ref site" qui, dans la plupart des installations sera simplement "default_". Cela garantit que vous pouvez facilement passer à professionnel si le besoin s'en fait sentir ou que vous pouvez distribuer le module d'installation à la fois sur la Communauté et Pro.

<div class="tip"><strong>Note:</strong> Ceci est necessaire lorsque vous utilisez  $this->db->query() ou équivalent. En revanche l'Active Record comme $this->db->where() and $this->db->get() ajoute le préfixe automatiquement. Vous pouvez également gerer vos tables avec  dbforge pour éviter cette étape.</div>

Si vous souhaitez creer un module disponible pour tous les sites dans le cas d'une installation multisite, alors vous devez specifier votre propre préfixe avant de faire une requete. 
If you wish to create a module that is available for use across all sites on a Multi-Site install then you can specify your own prefix before running queries to that table.

Voici la structure d'un fichier details.php classique: 

	<?php defined('BASEPATH') or exit('No direct script access allowed');
	
	class Module_Sample extends Module {
	
		public $version = '2.0';
		
		public function info()
		{
			return array(
				'name' => array(
					'en' => 'Sample'
				),
				'description' => array(
					'en' => 'This is a PyroCMS module sample.'
				),
				'frontend' => TRUE,
				'backend' => TRUE,
				'menu' => 'content', // You can also place modules in their top level menu. For example try: 'menu' => 'Sample',
				'sections' => array(
					'items' => array(
						'name' 	=> 'sample.items', // These are translated from your language file
						'uri' 	=> 'admin/sample',
							'shortcuts' => array(
								'create' => array(
									'name' 	=> 'sample.create',
									'uri' 	=> 'admin/sample/create',
									'class' => 'add'
									)
								)
							)
					)
			);
		}
		
		public function install()
		{
			$this->dbforge->drop_table('sample');
			$this->db->delete('settings', array('module' => 'sample'));
		
			$sample = array(
		        'id' => array(
				'type' => 'INT',
					'constraint' => '11',
					'auto_increment' => TRUE
				),
				'name' => array(
					'type' => 'VARCHAR',
					'constraint' => '100'
				),
				'slug' => array(
					'type' => 'VARCHAR',
					'constraint' => '100'
				),
			);
		
			$sample_setting = array(
				'slug' => 'sample_setting',
				'title' => 'Sample Setting',
				'description' => 'A Yes or No option for the Sample module',
				'`default`' => '1',
				'`value`' => '1',
				'type' => 'select',
				'`options`' => '1=Yes|0=No',
				'is_required' => 1,
				'is_gui' => 1,
				'module' => 'sample'
			);
		
			$this->dbforge->add_field($sample);
			$this->dbforge->add_key('id', TRUE);
		
			// Let's try running our DB Forge Table and inserting some settings
			if ( ! $this->dbforge->create_table('sample') OR ! $this->db->insert('settings', $sample_setting))
			{
				return FALSE;
			}
		
			// No upload path for our module? If we can't make it then fail
			if ( ! is_dir($this->upload_path.'sample') AND ! @mkdir($this->upload_path.'sample',0777,TRUE))
			{
				return FALSE;
			}
		
			// We made it!
			return TRUE;
		}
		
		public function uninstall()
		{
			$this->dbforge->drop_table('sample');
		
			$this->db->delete('settings', array('module' => 'sample'));
		
			// Put a check in to see if something failed, otherwise it worked
			return TRUE;
		}
		
		
		public function upgrade($old_version)
		{
			// Your Upgrade Logic
			return TRUE;
		}
		
		public function help()
		{
			// Return a string containing help info
			return "Here you can enter HTML with paragrpah tags or whatever you like";
		
			// You could include a file and return it here.
			return $this->load->view('help', NULL, TRUE); // loads modules/sample/views/help.php
		}
	}

	Le tableau contient des détails qui seront lues et enregistrées dans la base de données lors de l'installation. Vous pouvez fournir autant de langues supplémentaires que vous le souhaitez, par défaut la version english du nom et la description sera utilisée. 
	
	Ce tableau sera disponible dans votre Public\_Controller's and Admin\_Controller's via $this-&gt;module\_details['name']. Notez que le nom et la description retourné seront ceux de la langue active. 
	

## Detail File Resources


Même s'il est probable que votre module tierce partie sera installé via la section Add-ons du panneau de commande, notez qu'il peuvent également être installé pendant l'installation de PyroCMS s'ils se trouvent dans le dossier Shared Addons.

Nous recommandons que votre fichier details.php soit indépendant des configs et autres helper, ou d'autres ressources CodeIgniter.


## Public Controllers

Dans codeIgniter il y a une seule classe controleur. Dans PyroCMS il y en à 4 : Controller, MY\_Controller, Admin\_Controller and Public\_Controller. Pour les utiliser, vous devez les étendre comme ça :

	class News extends Public_Controller {
		
		function index()
		{
			$data['message'] = "Hello World!";
	
			// Loads from addons/<site-ref>/modules/blog/views/view_name.php
			$this->template->build('view_name', $data);
		 }
	}

	Cette page sera disponible pour quiconque est loggé ou pas, et utilisera le design du frontend.
	Cela signifie que que ça utilisera le thème courant et sera visible par "http://example.com/modulename".

## Admin Controllers

Contrôleurs d'administration ont quelques propriétés différentes à eux. Il vérifie automatiquement que l'utilisateur a la permission d'être là, et les rediriger vers une page de connexion si elle n'est pas. Cela signifie qu'ils doivent soit avoir un rôle d'utilisateur de "admin" ou bien être autorisés pour accéder au module.

<def>addons/</def>&lt;site-ref&gt;<def>/modules/&lt;module-name&gt;/controllers/admin.php</def>

	class Admin extends Admin_Controller {
	
		function index()
		{
			$data['message'] = "Hello logged in admin guy!";
	
			// Loads from addons/modules/blog/views/admin/view_name.php
			$this->template->build('admin/view_name', $data);
		 }
	}

This page can be accessed via "http://example.com/admin/&lt;module-name&gt;".

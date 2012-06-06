# Contrôleurs de Base

PyroCMS est fournit avec de nombreux contrôleurs de base pour étendre des fonctionnalités existantes. Vous pouvez éntendre vos propres classes avec les contrôleurs de base de PyroCMS&nbsp;:

	class Blog extends Public_Controller
	{
		public function __construct()
		{


## MY\_Controller

MY\_Controller permet d'obtenir les fonctionnalités suivantes. Si vous utilisez les contrôleurs Public\_Controller ou Admin_Controller, les fonctionnalités de MY\_Controller seront déjà incluses. MY\_Controller permet d'obtenir les fonctionnalités suivantes&nbsp;:

* Vérifie la constante SITE_REF pour vérifier que le site est bien configuré
* Défini le dbprefix pour SITE_REF
* Vérifie que les migrations sont en cours à la version actuelle
* Défini la constant CURRENT_LANGUAGE
* Charge le système d'authentification utilisateur
* Collectes des données sur l'utilisateur courant. Ces données sont accessibles via $this->current_user
* Gère les persmissions en se basant sur le module et sur l'utilisateur courant
* Défini le profileur de sortie (output profiler) en se basant sur les préférences

## Public\_Controller

Ce contrôleur est utilisé pour les contrôleurs du front-end, la classe Public\_Controller exécutera les processus suivant avant d'exécuter votre Contrôleur&nbsp;:

* Exécute les redirections à partir du module Redirection
* Appelle l'événement public_controller
* Vérifie si le site est désactivé et met le site hors ligne le cas échéant
* Charge le Thème du site et défini les variables en rapport avec celui-ci
* Défini les variables Javascript suivantes : APPPATH_URI et BASE_URI
* Défini une URL Canonique qui apparait dans le header metadata
* Défini le fil RSS dans le header metadata si le module blog existe et est activé
* Charge les variables du module Variables
* Charge les options du Thème

## Admin\_Controller

Ce contrôleur est utilisé pour les contrôleurs du back-end. Il exécute les processus suivants&nbsp;:

* Vérifie si l'utilisateur a accès au panneau d'administration
* Défini les requêtes en https: si configuré
* Défini le thème d'administration et charge les différents répértoires nécessaires
* Défini l'option enable_parser à FALSE. Paramétrez cette option à TRUE si vous souhaitez utiliser les tags PyroCMS dans vos vues admin.
# Translating Language Files

PyroCMS est construit pour avoir une interface entièrement multilingue, ce qui signifie que vous pouvez switcher entre différentes langues, et si votre langue n'est pas supportée, vous pouvez facilement la traduire à partir d'une des langues existantes.

## Currently Supported

Si votre langue est répertoriée ci-dessous, alors vous n'avez pas besoin de traduire quoi que ce soit, mais gardez à l'esprit que la seule langue officielle est l'anglais soutenu. Chaque autre langue est fourni et entretenu par la communauté. Ils pourraient être périmées ou contenir du traduction incorrecte.

* anglais
* arabe
* brésilienne
* Chinois (Traditionnel)
* tchèque
* Néerlandais
* finlandaise
* français
* Allemand
* grec
* hébreu
* italienne
* lituanienne
* polonaise
* Russie
* slovène
* Espagnol

### Step #1: Traduire ou Télécharger un pack de langue CodeIgniter

CodeIgniter possède une large communauté de développeurs dans de nombreuses langues, donc un contrôle rapide de la [CodeIgniter Translations Wiki] (http://codeigniter.com/wiki/Language_Translation/) ou Google peut vous fournir un pack de langue. Gardez à l'esprit que PyroCMS fonctionne avec le moteur v2.0.x CodeIgniter si vous installez v1.7.x ou plus, vous trouverez très probablement que des lignes de traduction sont manquantes ou incorrectes.

De toute façon, l'installation de votre pack de langue to system/codeigniter/languages/*&lt;language-name&gt;*

### Step #2: Traduire le pack de langue PyroCMS

Les fichiers de langue PyroCMS existent à la fois dans le dossier principal de l'application et à l'intérieur de chaque module. Ceci est une liste de tous les dossiers qui contiennent des fichiers de langue:

1. system/pyrocms/language/*&lt;language-name&gt;*/
2. system/pyrocms/modules/*&lt;module-name&gt;*/language/*&lt;language-name&gt;*/
3. addons/modules/*&lt;module-name&gt;*/language/*&lt;language-name&gt;*/

Pour obtenir ces nouveaux dossiers, il suffit de copier le dossier **english** , le renommer et de traduire tout le texte en anglais dans votre langue.

### Step #3: Ajouter la langue de chacun des modules details.php

Chaque module dispose d'un fichier details.php de détails sur le module comme des versions, des informations sur l'installation, les noms et les descriptions. Chaque nom et la description doit être traduit dans votre langue actuelle basée sur la [ISO_3166-2](http://en.wikipedia.org/wiki/ISO_3166-2) code 2 lettres. Par exemple, anglais : "en" et français : "fr".

### Step #4: Ajouter la langue dans la configuration

Ouvrez system/pyrocms/config/languages.php et d'ajouter votre langue au tableau avec le même code à deux chiffres utilisé à l'étape 3. Une fois ceci fait, vous verrez votre langue disponible dans le menu déroulant dans le Panneau de configuration.

Cela devrait être elle! Si vous obtenez des erreurs relatives à la langue lorsque vous passez à votre nouvelle langue et que vous voulez revenir à l'anglais , il suffit d'ajouter ?lang=en dans l'URL.

Lorsque vous avez confirmé que tout semble correct, vous pouvez envisager de contribuer aux changements de pack de langues de retour au cœur de PyroCMS via <a href="/docs/manuals/developers/contributing-changes-to-pyrocms ">forking avec GIT</a>. De cette façon, il peut être contribué à la prochaine version majeure et d'autres n'auront pas à passer du temps pour traduire PyroCMS .
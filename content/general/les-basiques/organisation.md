# Organisation 

Une des fonctions les plus importantes d'un CMS est de fournir une structure organisationnelle pour les concepteurs, développeurs et constructeurs de sites de créer leurs sites de manière modulaire et flexible. Dans cette section, nous allons parler de la façon dont vous pouvez structurer votre site en utilisant PyroCMS.

Pour un exemple, prenons un site simple pour un salon de coiffure. Cela va être un site très basique, nous allons donc jeter un oeil sur les pages dont nous avons besoin:

* Une page d'accueil
* Une page "Qui sommes nous"
* Une page avec les heures d'ouverture et une carte de localisation

Ça y est, assez simple pour continuer.

Nous pouvons commencer par regarder les modèles de page. Ils sont assez horrible, mais nous avons une idée de base de ce que nous avons besoin de monter sur le site.

{{ asset:img file="docs/barbershop-pages.jpeg" alt="Example Pages" class="doc_image" }}

Avant d'entrer dans la façon dont nous allons organiser ce site, nous allons jeter un coup d'oeil aux différents outils qui s'offrent à vous. Il ya quatre principaux:

1. Le thème général
2. Les thèmes partiels
3. Mises en page
4. pages

Ci-dessous nous allons entrer dans ce que chacune des parties fait, et puis tout rassembler pour notre site de salon de coiffure.

## Outils pour les thèmes

Votre conception commence avec votre thème. Un thème est l'endroit où vos mises en page de base se font (CSS, JS). (Pour plus de détials sur les thèmes et leur structure, voir le {{ link title="guide des themes" uri="/general/faire-des-themes-pyrocms/personnaliser-vos-themes" }}). Les deux outils d'organisation disponibles à votre thème sont **Theme Layouts** et **Theme Partials**.

### Theme Layouts

Les fichiers de mise en page sont les "Coquilles" du code HTML de votre site. Ils sont des fichiers dans le dossier ** views / layouts  ** de votre thème, et contiennent des choses comme l'ouverture et de fermeture HTML, l'en-tête, pied de page, et d'autres choses qui, invariablement, se présentent sur ​​votre site. Vous pouvez avoir autant de mises en page que vous le souhaitez.

### Theme Partials

Les partiels sont des morceaux de code que vous utilisez encore et encore que vous souhaitez séparer en petits morceaux. Les exemples sont des choses comme l'en-tête, pied de page, et les métadonnées. Ils sont conservés dans votre thème dans le dossier ** views/partials **  et mises en page sont insérés dans l'aide de balises PyroCMS:

	{{ noparse }}{{ theme:partial name="header" }}{{ /noparse }}

Vous pouvez avoir autant partiels thème que vous souhaitez, même si elles ne sont pas nécessaires. Ils sont à portée de main pour séparer les parties de code de votre site.

## Outils Page

Après, nous avons utilisé nos éléments de thème pour la mise en page générale, nous passons à nos pages spécifiques, qui sont traitées à l'intérieur du panneau de commande. Il existe deux outils qui sont disponibles ici: **Page Layouts** and **Pages**.

### Page Layouts

Les mises en page peuvent être trouvés dans la section mises en page du module Pages, et sont gérés par l'intermédiaire du panneau de contrôle PyroCMS.

Autrement dit, les mises en page sont des moyens pour séparer les différentes structures organisationnelles de vos pages qui font pas partie de la plus grande mise en page (en-tête, pied de page, etc.) Lorsque vous créez une nouvelle mise en page, vous lui assignez une mise en page du thème et le contenu de mise en page est intégrée dans la mise en page thème avec la balise suivante

	{{ noparse }}{{ template:body }}{{ /noparse }}

Si cela vous semble confus, ne vous inquiétez pas. Nous allons revenir à l'exemple salon de coiffure sous peu pour expliquer comment la mise en page se fait dans la pratique. Pour l'instant, rappelez-vous juste qu'ils traitent de la structure des pages individuelles.

### Pages

La dernière partie de la structure organisationnelle de PyroCMS est la page. Les pages sont ce que vous allez réellement voir via l'URL, et ils contiennent tout le contenu que vous souhaitez ajouter layouts / partials / page .

On peut assigné un layout à chaque page (qui à leur tour pourront être assigné)

## Notre exemple : le salon de coiffure de Bill

Maintenant que nous avons passé en revue les différentes parties d'une page PyroCMS, nous pouvons facilement imaginer la façon dont nous allons construire notre page de salon de coiffure. Encore une fois, voici les trois pages dont nous avons besoin pour mettre en œuvre notre site:

Tout d'abord, nous pouvons prendre la tête et pied de page et le mettre dans un **theme layout**. Nous savons que ces éléments ne changera pas de page en page, afin que nous puissions les garder tous en un seul endroit. Voici les domaines qui seront inclus dans notre **theme layout**:

{{ asset:img file="docs/barbershop-theme-layouts.jpeg" alt="Theme" class="doc_image" }}

<div class="tip"><strong>Note:</strong> Si nous voulons, nous pouvons garder la tête et pied de page de code dans leur propre <strong>partials</strong> et les charger dans la mise en page principale. Ce n'est pas nécessaire, cependant.</div>  

Maintenant que nous avons ces zones réprésenté, nous pouvons nous tourner vers nos pages. Nous en avons trois, et nous savons que chaque page a une structure HTML différente entre le header et footer. La page d'accueil est plus complexe (avec la photo et le coupon), la page "Qui sommes nous" est simple, et horaires et la carte ont juste besoin de deux colonnes. Voici la zone qui sera traitée par la mise en page:

{{ asset:img file="docs/barbershop-page-layouts.jpeg" alt="Page Layout Areas" class="doc_image" }}

Donc pour cet exemple nous allons créer trois mises en page ** **:

1. home
2. défaut
3. Horaire et carte

Deux d'entre eux sont très spécifiques (accueil et horaire), mais par défaut (ce que nous allons utiliser pour la page "Qui sommes nous") est suffisamment générique pour être réutilisé pour de nouvelles pages sur la route - c'est seulement un titre et le corps du texte, après tous.

Prenons Horaires d'ouverture et de la carte pour notre mise en page ** ** par exemple. Il faudra deux colonnes - le contenu de la page en un seul, et une carte Google (using the Google Maps {{ link uri='/general/les-basiques/widgets-plugins-and-modules' title="widget" }}) dans les autres: 

{{ asset:img file="docs/barbershop-single.jpeg" alt="Single page" class="doc_image" }}

Donc, nous allons aller à ** Contenu → Pages ** dans le panneau de commande et sélectionnez le ** ** Layouts section. Cliquez sur Mise en page ** ** Ajouter une page pour créer un nouveau.

Voici un exemple de ce que notre code de disposition pourrait ressembler pour les horaires et la carte:

     <h1>{{ noparse }}{{ page:title }}{{ /noparse }}</h1>
     
     <div class="one_third">{{ noparse }}{{ page:body }}{{ /noparse }}</div>

     <div class="two_thirds">{{ noparse }}{{ widgets:instance id="1"}}{{ /noparse }}</div>

* {{ noparse }} {{ page:title }}  et {{ page:body }} sont les tags spéciales pour une utilisation dans la mises en page PyroCMS. {{ /noparse }}*

Notez que la mise en page n'a pas besoin de se référer à sa mise en page thème parent. Le contenu de mise en page va aller là où nous avons mis **{{ noparse }}{{ template:body }}{{ /noparse }}** dans notre theme layout.

Si nous disposons de nos mises en page prête, nous pouvons aller dans l'arborescence des pages sous ** Contenu → Pages ** et créer une page pour chaque page de notre exemple, l'attribution de la disposition correspondante dans l'onglet ** Design **.

## Roundup

PyroCMS fournit quelques jolis outils organisationnels:

1. Un endroit pour mettre la coque du site (header, footer, etc.) - **theme layouts**.
2. Une façon de créer des mises en page ** ** sans avoir à toucher à la mise en page "maître".

Une fois que vous vous êtes habitué à la création de pages, mise en page et des mises en thème, vous pouvez vraiment expérimenter de nouvelles façons d'organiser votre site. Par exemple, vous pouvez utiliser des balises PyroCMS dans des boîtes contenu de la page. Vous pouvez également créer la page "morceaux" pour séparer le contenu de votre page en plusieurs morceaux différents.

PyroCMS vise à être souple, afin d'utiliser cette flexibilité pour que votre site soit exactement comme vous l'imaginez.
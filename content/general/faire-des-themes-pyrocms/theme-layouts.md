# Thème : Les Layouts

L'idée de base est que la plupart de vos pages vont avoir le même header, le même footer, la même navigation etc... et seul le contenu de la page changera.
Partant de cette idée, vous pouvez éviter de vous répéter et la duplication de code en utilisant des fichiers que vous allez inclure (les layouts).
En utilisants plusieurs layouts, vous pouvez faire un contenu personnalisé pour chacun de vos modules ou chacune de vos pages.

Tous les layouts sont dans <dfn>addons/&lt;site-ref&gt;/themes/&lt;theme-name&gt;/views/layouts/</dfn> où <dfn>shared_addons/themes/&lt;theme-name&gt;/views/layouts/</dfn>.

Chaque thème doit avoir au moins un layout que s'appeleriot &quot;default&quot; dans <dfn>addons/themes/views/layouts/.</dfn>


## Exemple de Layout

En utilisant les tags template, vous pouvez écrire les balises Titles, métadata (qui comprennent CSS et javascript) et le body pour creer le layout le plus simple possible : 


<pre class="prettyprint">{{ noparse }}
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
	&lt;title&gt;{{ template:title }}&lt;/title&gt;
	{{ template:metadata }}
&lt;/head&gt;
&lt;body&gt;
	&lt;h1&gt;{{ template:title }}&lt;/h1&gt;
	{{ template:body }}
&lt;/body&gt;

&lt;/html&gt;{{ /noparse }}</pre>

## Multiple Layouts


Pour plus de flexibilité, vous pouvez utiliser autant de layout que vous le souhaitez. Lorsque vous modifiez ou créez un layout de Pages dans CP &gt; Page &gt; Pages Layout et sélectionnez votre fichier désiré dans la liste déroulante, tout vos layouts de thèmes seront disponibles. 


## Mobile Layouts

Une fonctionnalité intéressante de PyroCMS est la capacité de distinguer les layouts pour l'affichage sur mobile.


Pour profiter de cette fonctionnalité, déplacez vos mises en page dans un dossier appelé "Web" dans votre dossier vues, de sorte que votre layout défault se trouve:

     your-theme/views/web/layouts/default.html
	 
Quand un utilisateur accède à votre navigateur depuis un navigateur Web, ces layouts seront utilisés. Si l'utilisateur est sur un appareil mobile, cependant, vous pouvez fournir différentes mises en page dans un dossier appelé *mobile*, de sorte que votre layout défault se trouve:

     your-theme/views/mobile/layouts/default.html



<strong>Note:</strong> PyroCMS ne considère pas un iPad comme étant un mobile. Donc vos layouts *mobile* ne seront pas chargés.  Notez aussi que le nouveau thème PyroCMS par défaut utilise le [responsive design](http://en.wikipedia.org/wiki/Responsive_Web_Design)


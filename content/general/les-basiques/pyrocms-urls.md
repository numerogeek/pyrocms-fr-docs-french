# URLs PyroCMS 

PyroCMS va au dela d'une arborescence classique. Sous **Content &rarr; Pages**, Vous trouverez une liste de vos pages. Chaque page a une URL sur laquelle l'utilisateur peut y accéder  (bien que PyroCMS ne viennent sur la page que sous certaines conditions).

{{ asset:img file="docs/pages.png" alt="Page Tree" class="doc_image" }}

Toutefois, PyroCMS est également un système CMS modulaire , et une de ses caractéristiques uniques est de permettre aux modules d'avoir leur propre URL "publique". Par exemple, le module **Blog**  dispose d'une interface dans le panneau de contrôle, mais il contient aussi toute la logique pour afficher les messages du blog et même un flux RSS, accessible via l'URL.

Ces modules URL utilisent les thèmes que vous avez choisis pour votre site , de sorte qu'ils seront stylisé de la même manière. Toutefois, si vous voulez affiner le contrôle  sur ces modules URL , vous pouvez le faire avec {{ link title="la surcharge des vues de module dans les thèmes" uri="/general/faire-des-themes-pyrocms/surcharge-vues-module" }}.

<div class="tip">
<strong>Astuce! Personnaliser les urls:</strong><br /> Bien que n'étant pas pris en charge via le Panneau de configuration, de temps en temps vous voudrez peut-être un routage personnalisé pour permettre à PyroCMS d'ignorer certains segments. Ceci peut être réalisé avec le logiciel gratuit<a href="http://www.pyrocms.com/store/details/pyroroutes">PyroRoutes</a> .
</div>

# Tag Reference

Les tags sont un moyen de mettre des contenus dynamiques dans vos thèmes ou dans vos pages.
Il peuvent aussi être un raccourci pour inserer une image, lien, JS, etc...
Ils peuvent etre embarqués duans une Page, un post de blog, ou directement dans le thème.

Par exemple, ce simple tag va retourner l'url du site : 

	{{ noparse }}{{ url:site }}{{ /noparse }}

Les tags peuvent être de simples variables, mais aussi des fonctionnalités plus avancés comme afficher un post de blog. 

Il est important de noter que certains tags acceptent des attributs qui affectent leur affichage. Par exemple, la liste des plugins que vous voyez en haut de cette page est générée par un plug-in dans le core de PyroCMS  - le plugin {{ link uri="/modules-and-tags/tag-reference/pages" title="Pages" }}, by embedding the page_tree tag:

	{{ noparse }}{{ pages:page_tree start-id=&quot;foo&quot; }}{{ /noparse }}

Pour plus d'infos sur la syntaxe des tags de PyroCMS, voir la page {{ link title="Syntaxe Tag" uri="/general/les-basiques/pyrocms-tags" }}.

<!--## Under the hood

If you are developer wanting to know more about how plugin tags work and how you can make your own, check out the {{ link title="developer docs" uri="/general/basics/pyrocms-tags" }}.
-->
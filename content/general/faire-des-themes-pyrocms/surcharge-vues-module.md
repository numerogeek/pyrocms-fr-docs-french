# Surcharge des vues de modules.

PyroCMS is written intended to be styled mainly by CSS, but as designers you want full control over how your site looks. We understand that, so PyroCMS will let you replace any module view with a view inside your theme. Let&#39;s say you want to replace the main blog listing page. Simply copy:

PyroCMS est écrit pour être customisé principalement avec du CSS, mais en tant que concepteurs vous voulez un contrôle total sur la façon dont votre site s'affiche. On le sait, donc PyroCMS vous permettra de remplacer n'importe quelle vue d'un module avec une vue à l'intérieur de votre thème. Disons que vous voulez remplacer la page principale du blog. Il suffit de copier:

	system/cms/modules/blog/views/posts.php

vers:

	addons/<site-ref>/themes/<theme-name>/views/modules/blog/posts.php

Now you can edit that view however you like and upgrade PyroCMS knowing your customized views are safe.
Maintenant, vous pouvez modifier votre vue comme bon vous semble et mettre à jour PyroCMS en sachant que vos vues personnalisées sont dans un endroit qui ne sera jamais écrasé.

## Syntaxe dans les vues surchargées.

You can still use PHP in these overloaded views. This means you can just copy whatever is there exactly and change it. In later versions we may be removing this as there is always the possibility that themes can contain malicious PHP if downloaded from a third-party site, but we will likely make this a setting.

Either way, you can use {{ link uri="/general/les-basiques/pyrocms-tags" title="Tag syntax" }} and this is most likely the safest, but can be more complicated for converting.


Vous pouvez toujours utiliser PHP dans ces vues surchargés. Cela signifie que vous pouvez simplement copier ce qui est là, tel-quel, et le changer. Dans les versions ultérieures, nous pourront peut-être supprimer cette fonctionnalité, car il ya toujours la possibilité que les thèmes contiennent du code PHP malicieux s'ils sont téléchargés à partir d'un site tiers, mais nous allons probablement laisser l'option via un réglage.
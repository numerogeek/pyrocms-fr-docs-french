# Add-ons

Les Add-ons sont des choses que vous pouvez télécharger et installer dans PyroCMS pour ajouter des fonctionnalités. Ils sont de trois types: **Widgets**, **Plugins**, et **Modules** ({{ link title="Voir le guide." uri="/general/les-basiques/widgets-plugins-and-modules" }}).

## Installer des Modules

Pour installer un module aller sur **Add-ons** dans le panneau de commande et cliquez sur Envoyer. Sélectionnez l'archive zip et télécharger. Si votre module ne se présente pas ou ne fonctionne pas correctement, assurez-vous que la structure du dossier est correct lorsque l'archive est extraite.

Alternativement, vous pouvez simplement télécharger le dossier module dans votre dossier _addons/shared\_addons/modules_ ou _addons/[site-ref]/modules_ . Une fois que vous actualisez la page add-ons du panneau de commande, vous devriez le voir dans la liste des modules. Click sur **Install** pour l'installer. 

### Desactiver ou Désinstaller un module

Si vous souhaitez supprimer un module du back-office et à partir des menus d'administration, vous pouvez désactiver le module. Pour supprimer les données et supprimer le module lui-même utiliser la fonction Supprimer.


<div class="tip"><strong>Attention :</strong> La suppression de tous les fichiers source d'un module, fichiers téléchargés, et les éléments de bases de données associées avec le module.</div>

## Installer des widgets

Pour installer un widget, vous devez le télécharger sur _addons/shared\_addons/widgets_ ou _addons/[site-ref]/widgets_. Ensuite, accédez é **Content &rarr; Widgets**. Votre widget devrait maintenant apparètre dans la liste. Pour l'utiliser il suffit de le glisser dans la zone appropriée Widget comme n'importe quel autre widget.

## Installer des plugins

Les Plugins n'ont pas de procédure d'installation. Il suffit de les télécharger sur _addons/shared\_addons/plugins_ ou _addons/[site-ref]/plugins_ et d'utiliser le tag dans vos layouts!

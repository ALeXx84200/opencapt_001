Développement custom
Si, pour les besoins de votre projet, vous avez besoin de customiser certaines parties du code, nous avons rendu cette opération la plus simple possible. Pour arriver à cela nous avons rendu possible le code custom. Cela vous permettra de développer du code spécifique sans tout perdre à chaque mise à jour.
Seuls les fichiers au niveau du backend sont modifiable. En effet, depuis la version 2.0 la partie frontend est gérée par Angular. Ce dernier nécessitant une compilation après chaque modification, la personnalisation n'est donc pas gérable.
Ajout d'un nouveau custom
Pour l'ajout d'un nouveau custom, rien de bien compliqué. Ouvrez le fichier custom/custom.ini à l'aide de la commande suivante : 
nano custom/custom.ini
Sur ce fichier, deux custom sont présents par défaut, tous deux désactivés. Afin d'en activer un, il vous suffit de passer le champ enabled à True. Si vous souhaitez créer votre propre custom suivant une convention de nommage particulière, vous le pouvez en dupliquant un bloc tel que le bloc [votre_custom] : 
[oc_invoices_1]
path = custom/oc_invoices_1
selected = True
​
[oc_invoices_2]
path = custom/oc_invoices_2
selected = False
​
[votre_custom]
path = custom/votre_custom
selected = True
Création de l'arborescence
Après avoir activé le custom voulu, comme montré précédemment, il ne vous reste plus qu'à choisir les fichiers à modifier et à recréer leur arborescence. Pour la suite nous allons nous baser sur l'exemple du custom [votre_custom]. Si jamais vous souhaitez modifier, par exemple, le fichier gérant les webservices liés aux utilisateurs, vous devrez recréer l'arborescence dans le dossier custom, comme suit : 
├── bin
├── custom
   └── votre_custom
        └── src
           └── backend
               └── rest
                  └── user.py
├── dist
├── instance
└── src
    ├── assets
    ├── backend
       ├── classes
       ├── controllers
       ├── invoice_classification
       ├── models
       ├── process
       └── rest
    └── frontend
Après avoir rajouté vos fichiers customs il est nécessaire de redémarrer différents services :
systemctl restart OCVerifier-worker_CUSTOMID
systemctl restart OCSplitter-worker_CUSTOMID
systemctl restart apache2
À noter que tout développement custom peut éventuellement être intégré au code source d'Open-Capture, si celui-ci répond à une problématique générique et peut répondre à une demande de la communauté. 

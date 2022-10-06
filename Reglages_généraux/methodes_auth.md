# Méthodes d'authentification
OpenCapture permet d'exploiter un annuaire de type AdLDAP ou OpenLDAP afin de centraliser la gestion des utilisateurs.
Deux niveaux d'exploitation possibles:
Authentification LDAP, la vérification des mots de passe des utilisateurs se fait dans l'annuaire dans ce cas.
Synchronisation des données de l'annuaire dans la base Opencapture.
Le menu des méthodes authentification rassemble les différents types d'authentification disponibles. Cette page permet de voir directement toutes les méthodes qu'un administrateur peut activer ou désactiver.

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2FAd1z4fAsFUNtHKTYLVgn%2Fcapture_doc1.png?alt=media&token=d1d0fd66-29d6-4627-ac43-71510b167fd1)

La méthode d’authentification "défaut" est celle qui est activée par défaut. Elle permet la connexion simple depuis la base de données d'Open-Capture For Invoices.
Activation de la méthode d'authentification LDAP
Une fois que le bouton d'activation est sélectionné, il faut remplir les paramètres de connexion et tester la connexion au serveur LDAP. La partie "Synchronisation" contient tous les paramètres nécessaires pour la synchronisation des utilisateurs.

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2FGmDFoYByksow1QK2od2o%2Fcapture_doc7.png?alt=media&token=09324423-f8b6-475b-a89c-8a3f0be6aeff)

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2F6WPZcLmYRGq7LXalp9Cv%2Fcapture_doc3.png?alt=media&token=4f5e82a3-a844-49c9-94ef-e2847cebebcb)

Il existe un script python dont le chemin depuis le répertoire d'installation OpenCapture  est le suivant  /bin/ldap/connectionLdapTest/connection_ldap.py . Le script permet de récupérer les paramètres de synchronisation.
Pour lancer le script : python3 connection_ldap.py 

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2FrBR5wAIfjgFPEoBSMWUC%2Fcapture.png?alt=media&token=bfa96e80-0c89-41e5-9d5a-04266620a369)

Exemple : 
givenName : Attribut prénom utilisateur
sn : Attribut nom utilisateur 
uid : Attribut source utilisateur
objectClass : Classe objet
inetOrgPerson : Classe utilisateur
Lorsque tous les champs obligatoires sont remplis, l'administrateur peut  lancer l'opération de synchronisation via le bouton "Lancer" dans la partie "Lancement".

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2FTAc3UPVX1Txu8nNK2oxw%2Fcapture_doc4.png?alt=media&token=57f5f112-cd00-4f95-b512-e142be31d067)

Le bouton "Enregistrer" sera cliquable seulement si le test de connexion et l'opération de synchronisation sont valides.
En cliquant sur ce dernier, toutes les informations (celles de connexion et aussi celles de synchronisation) seront enregistrées dans la base de données Opencapture dans la table login_methods. (Au chargement de la page, tous les champs seront remplis avec les données déjà enregistrées)
Si la méthode d'authentification LDAP est activé,  un message "LDAP activé"  va apparaître en dessous du formulaire de connexion.

![](https://2236962982-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Mi5WgnLF5b40vkqQsRV%2Fuploads%2FbVrdXx4T1VYHJVPpjwQ4%2Fcapture_doc5.png?alt=media&token=e10358be-4d91-4246-ae43-7cd6aa1dc07d)

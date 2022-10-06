nhbbygbukyhniuhjuAjout d'une nouvelle langue
La gestion du multilingue est gérée par . Son intégration à Open-Capture est facilitée grâce au module . Passons maintenant à la procédure pour rajouter une nouvelle langue, en plus du français et de l'anglais, présent par défaut.
Modification côté Python
Le premier fichier à modifier est instance/lang.json que vous trouverez à l'aide de la commande suivante : 
nano /var/www/html/opencapture/instance/lang.json
Il faudra rajouter la déclaration de la langue qui sera affichée dans la liste de choix situé dans le menu à droite. 
{
    "fr": {
        "label" : "Francais",
        "lang_code": "fra",
        "moment_lang_code": "fr-FR"
    },
    "en": {
        "label" : "English",
        "lang_code": "eng",
        "moment_lang_code": "en-GB"
    }
}
En vous basant sur l'existant vous pouvez rajouter une langue en sachant que :
La clé du tableau ('en', 'fr') est utile seulement pour la compréhension
L'index label est utile seulement pour la compréhension
L'index lang_code représente le code de langue qui sera renseigné automatiquement dans le fichier de configuration afin de récupérer les REGEspa_SPAX, l'OCR Tesseract ainsi que les variables de langues
L'index moment_lang_code indique le code spécifique pour gérer l'affichage des dates dans l'interface
Par exemple si nous voulions rajouter la langue espagnol (qui sera utilisée pour le reste de ce tutoriel) notre JSON ressemblerait donc à ça : 
{
    "fr": {
        "label" : "Francais",
        "lang_code": "fra",
        "moment_lang_code": "fr-FR"
    },
    "en": {
        "label" : "English",
        "lang_code": "eng",
        "moment_lang_code": "en-GB"
    },
    "spa": {
        "label" : "Español",
        "lang_code": "spa",
        "moment_lang_code": "spa_SPA"
    }
}
Ajout d'un paquet de langue Tesseract 
Si vous souhaitez que Tesseract puisse lire et comprendre également la nouvelle langue, il faut installer le paquet spécifique. Pour cela, le lien suivant recense les codes de langue Tesseract : . Dans notre exemple, pour rajouter la langue espagnole la commande à taper serait : 
sudo apt install tesseract-ocr-spa
Création des fichiers Babel
Il est désormais temps de créer le dossier Babel contenant toutes les traductions. Il suffira d'une seule ligne pour tout créer, le plus long sera de traduire ensuite tous les champs. Encore une fois, nous utilisons notre exemple avec la langue espagnole. 
cd /var/www/html/opencapture/src/assets/i18n/
pybabel init -i backend/messages.pot -d backend/translations -l spa
Ce qui vous donnera une arborescence comme ceci : 
backend
├── messages.pot
└── translations
    ├── en
    │   └── LC_MESSAGES
    │       ├── messages.mo
    │       └── messages.po
    ├── fr
    │   └── LC_MESSAGES
    │       ├── messages.mo
    │       └── messages.po
    └── spa
        └── LC_MESSAGES
            ├── messages.mo
            └── messages.po
Ouvrez maintenant le fichier spa/LC_MESSAGES/message.po. Vous aurez X traductions, présentées comme ci-dessous. Il ne vous reste plus qu'à tout traduire dans le champ msgstr.
#: src/backend/models/user.py:40
msgid "USER"
msgstr ""
Modification fichier JSON
Le dernier élément à créer pour finaliser l'ajout de langue est le fichier JSON contenant les REGEX. En effet les REGEX sont liés à une langue. Situé dans src/assets/locale, ce fichier JSON est essentiel pour une bonne reconnaissance des différentes métadonnées. Vous aurez à refaire le tableau des mois, qui recense toutes les écritures possible d'un mois, afin de pouvoir détecter tout type de date. Ensuite il faudra retravailler les REGEX une par une afin qu'elle puisse détecter du texte d'une autre langue. 
Dans notre exemple, il faudra créer un fichier nommé  src/assets/locale/spa.json

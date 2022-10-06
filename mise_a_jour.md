Mise à jour
Un script de mise à jour est disponible afin de faciliter ce processus. Ce dernier est situé dans le meme dossier que le script d'installation : /var/www/html/opencapture/bin/install/update.sh.
Ce script récupérera le dernier tag d'Open-Capture et mettra à jour les paquets APT ainsi que les paquets PIP si nécessaire. Tout le paramétrages spécifique fait en base de données ou dans les fichier .ini seront conservés. Un backup sera également effectué, sous la forme suivante : /var/www/html/opencapture.$currentDate. Pour lancer le script, rien de plus simple :
cd /var/www/html/opencapture/bin/install
sudo ./update.sh
Après la mise à jour, il est probable qu'une mise à jour de certains champs/tables de la base de données soit nécessaire. Si tel est le cas, un message apparaitra à la fin du script de mise à jour, tel que : 
########################################################
                 Version : 2.3.0
    A script containing database changes is present
      If necessary, do not hesitate to execute it
 in order to take advantage of the latest modifications
########################################################
Afin de mettre à jour la BDD les commandes à taper sont les suivantes (pour l'exemple de la version 2.3.0) : 
sudo su postgres -c psql
\c opencapture_angular
\i /var/www/html/opencapture/bin/install/migration_sql/2.3.0.sql
quit

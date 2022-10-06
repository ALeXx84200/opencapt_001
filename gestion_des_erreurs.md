Gestion des erreurs
Si vous rencontrez des erreurs, il y a plusieurs endroits où aller regarder afin de déterminer la cause du problème. Le premier endroit est le fichier de log principal. Il recense tout ce qu'il se passe dans le traitement d'Open-Capture, même lorsqu'il n'y a pas d'erreurs. Ci-dessous des exemples de logs en fonction de l'installation (via systemd ou via supervisor). Pour les mails, les fichiers de logs sont situés dans /var/www/html/opencapture/bin/data/MailCollect/*BATCH_NAME*. Les logs sont ensuite séparés par jours.
[Open-Capture  ] 06-04-2021 14:26:51 INFO Start following batch : BATCH_20210406_142651576284_daycputd
[Open-Capture  ] 06-04-2021 14:26:51 INFO Action after processing e-mail is : none
[Open-Capture  ] 06-04-2021 14:26:51 INFO Number of e-mail to process : 8
[Open-Capture  ] 06-04-2021 14:26:51 INFO Start to process only attachments
[Open-Capture  ] 06-04-2021 14:26:51 INFO Process e-mail n°1/2
[Open-Capture  ] 06-04-2021 14:26:51 INFO Found 1 attachments
[Open-Capture  ] 06-04-2021 14:26:51 INFO Process attachment n°1/1
[Open-Capture  ] 06-04-2021 14:26:52 INFO Processing file : /home/nathan/PycharmProjects/oc_invoices_flask/bin/data/MailCollect//MAIL_1/20210406/BATCH_20210406_142651576284_daycputd/mail_9/attachments/Plans_Bailleur_ST_NAZAIRE_IMMACULÉE_V2_220321.pdf
[Open-Capture  ] 06-24-2021 14:27:47 INFO Supplier found : Edissyum using VAT Number : FR71510268261
[Open-Capture  ] 06-04-2021 14:28:11 INFO Invoice date found : 16/03/2021
[Open-Capture  ] 06-04-2021 14:28:35 INFO Invoice inserted in database
[Open-Capture  ] 06-04-2021 14:28:35 INFO Process end after 00:01:44.23
[Open-Capture  ] 06-04-2021 14:28:35 INFO Process e-mail n°2/2
[Open-Capture  ] 06-04-2021 14:28:35 INFO No attachments found
[Open-Capture  ] 06-04-2021 14:28:35 INFO Start to process only attachments
Si jamais une erreur apparait dans l'interface web, vous empêche toute action et que rien n'est présent dans les fichiers de logs, il faudra aller regarder du côté les logs d'erreurs du service `apache2`. Vous pourrez voir l'erreur en utilisant la commande suivante. Avec cette erreur, vous pouvez ouvrir une  afin que nous puissions l'investiguer.
sudo tail -f /var/log/apache2/error.log
Si jamais le problème intervient lors du traitement de la facture (cette dernière ne remonte pas dans l'interface par exemple), ce sera le service gérant Open-Capture-Splitter ou Open-Capture-Vérifier qu'il faudra vérifier. Comme pour la partie web, avec les informations sur l'erreur, vous pouvez ouvrir une .
sudo systemctl status OCVerifier-worker_CUSTOMID
Si vous êtes capable de corriger le problème vous-même, il faudra bien penser à redémarrer le service en question afin que les modifications soient prises en compte. Si vous utilisez supervisor, il faudra redémarrer le service web de la même manière que présenté ci-dessous. Cependant pour les deux autres services, une seule commande sera nécessaire.
sudo supervisorctl restart all
Dans le cas où le (ou les) worker est totalement down il sera possible de redémarrer totalement le service rabbitMQ, la librairie gérant les piles de documents et permettant de les traiter un par un. 
rabbitmqctl stop_app
rabbitmqctl start_app


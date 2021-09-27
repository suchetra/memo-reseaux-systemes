# memo-reseaux-systemes

SSH

* pour redémarrer la ligne de commande et prendre en compte les modifications
  * service ssh restart 


ssh allow password login ?


* créer un fichier
  * touche nomFichier.txt

* pour accéder et éditer un fichier
  * nano nomFichier.txt
  * pour quitter une fois édité
    * ctrl s puis ctrl x 

* accéder au dossier
  * cd nomDossier

* lister les fichiers
  * ls
  * ll (en plus précis)

* voir un fichier
  * cat nomFichier.txt

* supprimer un fichier
  * rm nomFichier.txt

___

* créer un nouvel user
  * adduser nico2 

* donner des privilèges au user actuel ?
  * sudo 

* créer un user et donner des privilèges
  * sudo adduser

* donner des privilèges à nico2
  * usermod -aG sudo nico2

* pour s'auto connecter
  * ssh nico2@localhost	

* pour savoir dans quel groupe je suis	
  * groups

apt install nano ?

* Configurer et autoriser le password (à faire depuis le root)
  * nano /etc/ssh/sshd_config

password asked : yes
chercher ctrl w
ctrl ^x pour quitter) 

___

scp root@monip: chemindufichier identifiantDestinataire@sonip ?

* envoyer un fichier depuis mon serveur au serveur de quelqu'un d'autre (via son mot de passe), puis saisir son identifiant et mot de passe
  * scp nomFichier identifiantDestinataire@adresseIPDestinataire:

* envoyer un fichier depuis mon serveur au serveur de quelqu'un d'autre (via la clé)
  * créer un fichier .txt "key"
  * coller la clé à l'intérieur
  * restreindre les droit d'accès (“rw rw r” devenu “rw”) (voir sur Google "permission fichier linux") de key est un fichier .txt
    * chmod 600 key 
  * le deuxième nomFichierAEnvoyer.txt peut être modifier pour qu'il ait un nouveau nom dans le serveur destinataire
    * scp -i key nomFichierAEnvoyer.txt root@adresseIPDestinataire:nomFichierAEnvoyer.txt 
  * vérifier depuis le serveur et depuis le user destinataire que le fichier est reçu :
    * sudo ls /root
  * vérifier depuis le serveur et depuis le root destinataire que le fichier est reçu :
    * ls

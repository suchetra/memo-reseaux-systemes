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
    * ctrl c pour exit ?


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

* installer des packages
  * apt install nomPackage 
 
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
___

chat en ligne avec commande netcat 

* Version - rejoindre quelqu’un qui héberge le port
  * Je suis connecté avec mon user et le destinataire est en root 
  * 0102 étant le port, choix du port entre 1024 - 65000 (en dehors pour les usages internes, exemple ssh port par défaut 22, 443 pour HTTP, etc.)
    * nc  adresseIPDestination 0102 


* Version - hébergement et quelqu’un nous rejoint
  * Je suis connecté en root, 64000 étant le port
    * nc -l -p  64000
___
___

Docker

(cf : https://www.wanadev.fr/24-tuto-docker-demarrer-docker-partie-2/)

* démarrer Docker
  * docker run -d -p 80:80 docker/getting-started

* affiche la liste des containers qui tournent sur la machine
  * docker ps

* pour arrêter le container
  * docker rm nomIDContainer 
  * docker rm surnomCommeVigorousDog
  * ou simplement faire "exit" quand on est en mode interactif

* Voir l'historique entre l'image de base et l'image finale (on stocke en réalité tous les containers qui nous ont permis de passer de l'image de base à l'image finale) 
  * docker history
* voir la « bibliothèque » d'images
  * docker images

* chercher une image
  * docker search nomImage
* télécharger une image
  * docker pull nomImage


* Construire une image depuis un Dockerfile (spécifier le chemin du Dockerfile (d'où le point à la fin de la commande si vous lancez la commande depuis le même endroit)
  * docker build .
* Nommer une image au moment de l'utilisation de docker-commit, gra^ce à la commande docker-build et de son option --tag
  * $ docker build --tag="myImage[:myTag]"


* créer un docker file
  * vi nomFichier


* vérifier les droits
  * groups
* Add your user to the docker group (redémarrer Putty en quittant et se reconnectant)
  * sudo usermod -aG docker $USER
* voir les info docker
  * docker info

* créer une image
  * docker run -d --name container1 ubuntu:latest
  * docker run -d --name container1 ubuntu sleep3600 (pas bon car ubuntu remplace )

___

Tuto :
* lancer Docker
* créer Dockerfile
* modifier Dockerfile et mettre : 

FROM ubuntu:20.04
RUN apt-get update && apt-get install -y apt-utils && rm -rf /var/lib/apt/lists/*
# Set the locale
RUN  apt-get update && apt-get install locales && locale-gen en_US.UTF-8 && rm -rf /var/lib/apt/lists/*
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server php

remarque :
-y veut dire yes
Si demandé : Geographic area: 8


Quand l'installation est complète, ensuite :

(boutique nomImage)
argument -t https://stackoverflow.com/questions/30137135/confused-about-docker-t-option-to-allocate-a-pseudo-tty
* docker build -t boutique .

* docker images
* nano start.sh

on modifie dans le start.sh : 
-ti https://docs.docker.com/engine/reference/run/
* docker run -ti -p 80:80 --name nicolas boutique bash

remarque :
nicolas est le surnom du container

on sort
* sudo chmod +x start.sh

* ./start.sh 

puis
* service apache2 start

si on sort il faut dire qu'on supprime nicolas dans le start.sh :
* docker run -ti -p 80:80 --name nicolas --rm boutique bash

ctrl d pour sortir 
./start.sh 

___

faire un commit :
ouvrir un deuxième putty
docker commit idContainer nomImage

___

ls
cd var/www/html/
ls
service apache2 start
dans navigateur aller sur son adresse IP

rm index.html
ls
git clone https://github.com/suchetra/ClothingStore.git .
apt-get install git

nano : editeur de texte
apt-get install nano


vers index.php
git status
git branch
(inscription nom de la branche)
git checkout inscription
git pull
apt-get install phpmyadmin
apt-get install sql-server

autres commandes :
ctrl r (dans navigateur pour rafraichir le cache)

ctrl s
ctrl x
* voir quels services est en marche
  * service --status-all
mysql --version
* affiche la liste des containers cachés
  * docker ps -a 

* renommer
  * mv Dockerfile2 Dockerfile

Si container name is conflict

* docker stop nicolas
* docker rm nicolas

Question :
- est-il possible de créer une image avant un container
pas de container sans image


installer phpmyadmin
installer sql-server

___

docker run -ti -p 80:80 --name nicolas2container --rm nicolas2container bash

___

docker push reponico:tagnico

docker tag local-image:tagname new-repo:tagname
docker tag nicolas3image:latest reponico:tagnico

docker push new-repo:tagname
docker push reponico:tagnico

https://lucasvidelaine.wordpress.com/2018/01/29/utilisation-de-dockerhub/
$ docker login --username=pseudo
$ docker images

$ docker tag e7860ef846q5 pseudo/myrepo:test
$ docker tag 961e0a9a3596 suchetra/reponico2:tagnico2

$ docker push pseudo/myrepo
$ docker push suchetra/reponico2:tagnico2

$ docker run pseudo/myrepo

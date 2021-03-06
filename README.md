# memo-reseaux-systemes

NETCAT

chat en ligne avec commande netcat 

* Version - rejoindre quelqu’un qui héberge le port
  * Je suis connecté avec mon user et le destinataire est en root 
  * 0102 étant le port, choix du port entre 1024 - 65000 (en dehors pour les usages internes, exemple ssh port par défaut 22, 443 pour HTTP, etc.)
    * nc  adresseIPDestination 0102 


* Version - hébergement et quelqu’un nous rejoint
  * Je suis connecté en root, 64000 étant le port
    * nc -l -p  64000
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


* Construire une image depuis un Dockerfile (spécifier le chemin du Dockerfile (d'où le point à la fin de la commande si vous lancez la commande depuis le même endroit))
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

ou cloner une branche spécifique (à tester)
https://www.freecodecamp.org/news/git-clone-branch-how-to-clone-a-specific-branch/

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

___
___
___

Raccourcis 

revenir au répertoire précédent
cd -

retrouver une commande
ctrl r motAChercher

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

DEPLACEMENT et SUPPRESSION

autres commandes
q pour quitter

* déplacer dossierA au dossier parent
  * mv dossierA ..
  * pour forcer : 
    * sudo mv dossierA ..
* effacer dossierA et son contenu 
  * rm -rf dossierA
* déplacer file1 file2 file3 et le mettre dans DESTINATION
  * mv -t DESTINATION file1 file2 file3
  * déplacer tous les dossiers (sauf les dossiers cachés)
    * mv * DESTINATION
* supprimer un fichier
  * rm nomFichier.txt

SSH

* connexion au serveur distant
  * ssh nicolas.tan@51.15.220.20

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

___

* installer des packages
  * apt install nomPackage 
 
*  changer mot de passe
  * se loguer normalement et rentrer la commande :
    * passwd
 
* créer un nouvel user
  * adduser nico2 
* autre méthode
  * sudo adduser --force-badname jean.poma

* effacer un user
  * Passez en mode utilisateur racine :
    * sudo su -
  * puis :
    * userdel nomUser

* switch between users on one terminal
  * su - anotherUser

* To list all local users you can use:
  * cut -d: -f1 /etc/passwd

* donner des privilèges au user actuel ?
  * sudo 

* créer un user et donner des privilèges
  * sudo adduser

* donner des privilèges à nico2 pour utiliser Docker
  * usermod -aG sudo nico2
* sinon tester :
  * sudo usermod -a -G docker $USER

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

afficher les log
var/log
voir les log en temps réel
tail -f ?

___ 
Encryption asymétrique

on a la clé publique
on donne à l'autre personne (exemple serveur distant) la clé privé comme ça il peut nous envoyer le message 

___
LIEN SYMBOLIQUE 

fichier qu'on modifie et le fichier cible, qui est issue du lien symbolique, qu'on veut modifier indirectement (sans le modifier directement)

* voir le lien symbolique 
  * Simplest way: cd to where the symbolic link is located and do ls -l to list the details of the files. The part to the right of -> after the symbolic link is the destination to which it is pointing.
Source: https://ostoday.org/apple/question-how-do-i-update-a-symbolic-link-in-linux.html

https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1604
* créer le lien symbolique "le dossier choisi" vers "l'endroit où sera le lien symbolique"
  * ln -s /home/nicolas.tan/ClothingStore/ /var/www/html/

  * ls -l /var/www/html

___
BDD

scp C:\Users\kode\Documents\www\sqls\lastones\shopseb.sql iulian.baranescu@212.47.251.44:/var/www/html/shop_base.sql
scp C:\Users\Nicolas\Desktop\campus_marche_noir.sql nicolas.tan@51.15.220.20:/var/www/html/

scp C:\Users\Nicolas\Desktop\campus_marche_noir.sql 
qui a marché
___

markdown
markdown cheat sheet pdf

créer un alias, raccourci 
https://doc.ubuntu-fr.org/alias
https://qastack.fr/ubuntu/686710/why-do-i-get-a-train-when-i-run-ls

script shell programmation
https://www.tuteurs.ens.fr/unix/shell/script.html




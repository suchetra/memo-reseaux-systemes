# memo-reseaux-systemes

SSH

* pour redémarrer la ligne de commande et prendre en compte les modifications
  * service ssh restart 


ssh allow password login

id dans puty 
user nico 2
password aze

putty auth clé ssh pour connexion en root
adduser nico2 (creer une nouvel user)
sudo (donner prifilege a ton user actuel)
sudo adduser

usermod -aG sudo nico2      donne provilege a nico2

ssh nico2@localhost	pour s auto connecter

groups 	pour savoir dans quelle group je suis	

apt install nano
(nano /etc/ssh/sshd_config)
(password asked : yes
chercher ctrl w
ctrl ^x pour quitter) 

service ssh restart


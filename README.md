# -Tuto-Installation-d-un-serveur-web-sous-linux-PHP-7.4
Création et installation d'un serveur web sous linux

-----------------------------------------------------------------------------------------

Crée un hébergement web Linux server
Server Linux recommander :

Ubuntu 16.04
Ubuntu 18.04
Ubuntu 20.04
CentOS 7 / 8 / 9
Debian 8 / 9 /10
 Simple et pratique vous avez juste à taper la liste des commandes suivante dans l'ordre indiquer !

On vas commencer par le serveur apache2 / PHP

Les Dépôts

-----
Mise à jour
Ajout des dépôts
et installation :


```apt update && upgrade
apt -y install software-properties-common curl
LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
add-apt-repository -y ppa:chris-lea/redis-server
apt update
apt-add-repository universe
apt -y install php7.4 php7.4-cli php7.4-gd php7.4-mysql php7.4-pdo php7.4-mbstring php7.4-tokenizer php7.4-bcmath php7.4-xml php7.4-fpm php7.4-curl php7.4-zip mysql-server apache2 tar unzip git redis-server 

```

Voila vous avez installer les paquets pour le serveur web
Nous allons maintenant modifier le mot de passe root MYSQL Serveur

ou CREATE USER 'user1'@'%' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON *.* TO 'user1'@'%' WITH GRANT OPTION;



Arrêtez le serveur de base de données en lançant:

```sudo systemctl stop

sudo systemctl edit mysql

#Mettre le ceci : (pour quitter CTRL X / y / y

[Service]
ExecStart=
ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/run/mysqld/mysqld.pid

sudo systemctl daemon-reload
sudo systemctl start mysql
```
Changer le mot de passe root
```sudo mysql -u root
FLUSH PRIVILEGES;
UPDATE mysql.user SET authentication_string = PASSWORD('VOTREMDP') WHERE user = 'root';
UPDATE mysql.user SET plugin = 'mysql_native_password' WHERE user = 'root';
```
Rétablir les paramètres normaux de votre serveur de base de données
```sudo systemctl unset-environment MYSQLD_OPTS
sudo systemctl revert mysql
sudo systemctl daemon-reload
sudo systemctl restart mysql
```
Connexion mysql root avec votre nouveau MDP
```
mysql -u root -p
```
Installation de PHPMYADMIN

```
sudo apt install phpmyadmin
```
Installation des paquet pour phpmyadmin

```sudo apt install php libapache2-mod-php
sudo apt install php7.2-mbstring
sudo a2dismod mpm_event
sudo a2enmod mpm_prefork
service apache2 restart
```
Installation des paquet MYSQLI pour phpmyadmin

```apt install php-mysql
apt policy php-mysql
service apache2 restart
```

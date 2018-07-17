# LAMP Stack Provisions
If you want to provision a LAMP stack using the vagrant file example on the [Vagrantfiles](/vagrant/vagrantfiles.html) page, create a file called bootstrap.sh that contains the example below and place it in the same directory as the vagrant file.
```
# Update Packages
apt-get update
# Upgrade Packages
apt-get upgrade

# Git
apt-get install -y git

# Apache
apt-get install -y apache2

# Enable Apache Mods
a2enmod rewrite

#Add Onrej PPA Repo
apt-add-repository ppa:ondrej/php
apt-get update

# Install PHP
apt-get install -y php7.2

# PHP Apache Mod
apt-get install -y libapache2-mod-php7.2

# Restart Apache
service apache2 restart

# PHP Mods
apt-get install -y php7.2-common
apt-get install -y php7.2-mcrypt
apt-get install -y php7.2-zip

# Set MySQL Pass
debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'

# Install MySQL
apt-get install -y mysql-server

# PHP-MYSQL lib
apt-get install -y php7.2-mysql

# Restart Apache
sudo service apache2 restart
```

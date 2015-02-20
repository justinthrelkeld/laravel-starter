# -*- mode: ruby -*-
# vi: set ft=ruby :

# Documentation: http://vagrantup.com

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
PATH=~/.composer/vendor/bin:$PATH

composer global require "laravel/installer=~1.1"

sudo apt-get update
sudo apt-get install nginx php5-json php5-curl php5-fpm php5-cli php5-mcrypt git -y

# set up nginx stuff
sudo rm /etc/php5/fpm/php.ini
sudo ln -s /var/www/html/box_config/nginx/php.ini /etc/php5/fpm/php.ini

sudo rm /etc/nginx/sites-available/default
sudo ln -s /var/www/html/box_config/nginx/sites-available /etc/nginx/sites-available/default

# stop Apache so we can use nginx instead
apachectl -k stop
sudo rm /etc/init.d/apache2

sudo php5enmod mcrypt
sudo service php5-fpm restart

# aaaaand bring on nginx
sudo update-rc.d nginx defaults
sudo service nginx restart

echo "checking that mysql is running"
mysqlcheck
echo "mysql is running, setting up database"
mysql -u root -proot -e "create database vagrant_dev"

cd /var/www/html
chmod -R 777 /var/www/html/storage
php artisan migrate
SCRIPT



Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "avenuefactory/lamp"
  config.vm.provision :shell, inline: $script
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.usable_port_range
  config.vm.network "private_network", ip: "192.168.33.100"
  config.vm.synced_folder "", "/var/www/html"

end

# Langkah install php
sudo apt update
sudo apt install apache2
sudo apt install php8.2 php8.2-curl libapache2-mod-php8.2 php8.2-bcmath php8.2-zip php8.2-mbstring php8.2-mysql php8.2-gd php8.2-xml php8.2-tokenizer php-common php-json php-sqlite3
sudo nano /etc/apache2/mods-enabled/dir.conf
ubah menjadi= DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
sudo nano /var/www/html/phpinfo.php
isi=  <?php phpinfo(); ?>

# Langkah install php 
sudo wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
sudo mkdir /var/www/html/phpmyadmin
sudo tar xvf phpMyAdmin-latest-all-languages.tar.gz --strip-components=1 -C /var/www/html/phpmyadmin
sudo cp /var/www/html/phpmyadmin/config.sample.inc.php /var/www/html/phpmyadmin/config.inc.php
sudo nano /var/www/html/phpmyadmin/config.inc.php
$cfg['blowfish_secret'] = 'My_Secret_Passphras3!';
sudo chmod 660 /var/www/html/phpmyadmin/config.inc.php
sudo chown -R www-data:www-data /var/www/html/phpmyadmin
sudo systemctl restart apache2

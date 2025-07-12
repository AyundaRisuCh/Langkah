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

-- Membuat database sederhana
CREATE DATABASE IF NOT EXISTS sigap_db;

-- Menggunakan database
USE sigap_db;

-- Membuat tabel users sederhana
CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    no_hp VARCHAR(20) NOT NULL,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(10) DEFAULT 'user' NOT NULL
);

-- Data admin (password dalam plain text - HANYA UNTUK BELAJAR)
INSERT INTO users (nama, email, no_hp, password, role)
VALUES (
    'admin', 
    'admin@sigap.id', 
    '081122334455', 
    'admin123',  -- Password dalam plain text
    'admin'
);

-- Data user biasa (password dalam plain text - HANYA UNTUK BELAJAR)
INSERT INTO users (nama, email, no_hp, password, role)
VALUES (
    'user', 
    'user@test.com', 
    '085678901234', 
    'user123',  -- Password dalam plain text
    'user'
);

Buat di sql phpMyAdmin untuk bencana

CREATE TABLE data_bencana (
    id INT AUTO_INCREMENT PRIMARY KEY,
    jenis_bencana VARCHAR(50) NOT NULL,
    lokasi VARCHAR(100) NOT NULL,
    waktu_kejadian DATETIME DEFAULT CURRENT_TIMESTAMP
);


Membuat replica di aws

- klik dashboard RDS
- klik db instance
- centang database lalu klik action klik create read replica
- buat nama, single AZ, IPv4, publicly accessible, enable auto minor, lalu create read replica dan tunggu sampai available
- jika sudah klik replica yang dibuat tadi dan copy endpointnya, pastekan endpointnya di tampil.php

Membuat images server

- pada menu instance centang server dan klik action, pilih "images dan template" lalu "create image"
- masukkna nama image contoh "ServerDafa2"
- klik create image
- tunggu status di menu AMIs sampai available

Membuat auto scaling

- masuk kemenu auto scaling, dan create auto scaling
- buat Namanya, dan create template
- buat nama templatenya, pada "application and os" pilih "My AMIs" pilih instance yang kita buat
- masukkan keypair, dan security groupnya, klik create launch template
- balik pada tampilan create auto scaling, dan pilih template yang dibuat tadi, kemudian next
- untuk cpu dan memory yang minimum buat 1, dan maximumnya 2, kemudian select zone nya dan next
- di step 3 next aja ga ada yang diubah
- di step 4, bagian scaling max nya buat 2 lalu next
- step 5 & 6 next saja
- step terakhir klik create auto scaling group

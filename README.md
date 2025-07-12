## Langkah Install APACHE dan PHP
### Update dan upgrade version repository linux/ubuntu
```bash
sudo apt update && sudo apt upgrade
```
### Install Apache2 dan PHP beserta module php-mysqli 
```bash
sudo apt install apache2 php php-mysqli
```
## Langkah install phpMyAdmin
### Download phpMyAdmin
```bash
sudo wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
```
```bash
sudo mkdir /var/www/html/phpmyadmin
```
```bash
sudo tar xvf phpMyAdmin-latest-all-languages.tar.gz --strip-components=1 -C /var/www/html/phpmyadmin
```
``` bash
sudo cp /var/www/html/phpmyadmin/config.sample.inc.php /var/www/html/phpmyadmin/config.inc.php
```
``` bash
sudo nano /var/www/html/phpmyadmin/config.inc.php
```
``` bash
$cfg['blowfish_secret'] = 'My_Secret_Passphras3!';
```
``` bash
sudo chmod 775 /var/www/html/phpmyadmin/config.inc.php
```
``` bash
sudo chown -R ubuntu:ubuntu /var/www/html/phpmyadmin
```
``` bash
sudo systemctl restart apache2
```

``` bash
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
```
``` bash
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
```
``` bash
-- Buat di sql phpMyAdmin untuk bencana

CREATE TABLE data_bencana (
    id INT AUTO_INCREMENT PRIMARY KEY,
    jenis_bencana VARCHAR(50) NOT NULL,
    lokasi VARCHAR(100) NOT NULL,
    waktu_kejadian DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

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

sudo apt install git
sudo apt update
sudo apt install apache2
sudo apt install git
cd /var/www/html
ls
sudo rm index.html
cd ..
sudo chown ubuntu:ubuntu html
sudo chmod 775 -R html
ls -l
cd html
git clone (link GitHub) .

# Sonerezh

## Sekilas Tentang
**Sonerezh** merupakan sebuah aplikasi pemutar musik pribadi berbasis web yang unik. **Sonerezh** dapat mengunggah musik yang diinginkan dari web player dan memasukkannya ke database sehingga dapat didengarkan kapanpun, dimanapun, dan oleh siapapun yang diizinkan untuk mendengarkan koleksi kita.

## Instalasi
### Kebutuhan sistem :
- Unix, Linux, atau Windows
- Apache2
- Php
- MySQL
- Ffmpeg
## Proses Instalasi
1. Akses *Virtual Machine* dengan ssh
```
ssh <username>@localhost -p 2222
``` 
2. Pastikan sistem *Up-To-Date*, lalu install seluruh kebutuhan sistem (*Apache2, php, MySQL, dan ffmpeg*)
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apache2
sudo apt-get install php
sudo apt-get install php-gd php-mysql
sudo apt-get install ffmpeg
```
3. Aktifkan ekstensi PHP sudah diaktifkan (sudah di uncomment dan ada .so nya)
```
sudo nano /etc/php/7.2/apache2/php.ini
extension=exif.so
extension=gd.so
extension=gd2.so
extension=pdo_mysql.so
```
4. Cek apakah Apache sudah aktif atau belum
```
sudo service apache2 restart
```
5. Masuk ke Public HTML
```
cd /var/www/html
```
6. Download **Sonerezh**
```
wget https://www.sonerezh.bzh/downloads/latest.tar.gz
tar -zxf latest.tar.gz
```
7. Ubah kepemilikan ke www-data
```
sudo chown -R www-data:www-data sonerezh/
```
8. Buat database baru untuk **Sonerezh**
```
mysql -u root -p
	CREATE DATABASE sonerezh;
	GRANT ALL PRIVILEGES ON sonerezh.* TO 'sonerezh'@'localhost' IDENTIFIED BY '<new password>';
	flush privileges;
	exit;
```
9. Setting Virtual Host pada Apache
```
sudo a2enmod rewrite
sudo nano /etc/apache2/sites-available/sonerezh.conf
<VirtualHost *:443>
    ServerName      127.0.0.1
    DocumentRoot    /var/www/html/sonerezh

    <Directory /var/www/html/sonerezh>
        Options -Indexes
        AllowOverride All

        # Apache 2.2.x
        <IfModule !mod_authz_core.c>
            Order Allow,Deny
            Allow from all
        </IfModule>

        # Apache 2.4.x
        <IfModule mod_authz_core.c>
            Require all granted
        </IfModule>
    </Directory>

    CustomLog   /var/log/apache2/demo.sonerezh.bzh-access.log "Combined"
    ErrorLog    /var/log/apache2/demo.sonerezh.bzh-error.log
</VirtualHost>
```
10. Akrifkan *site* nya dan restart Apache
```
sudo a2ensite sonerezh
sudo service apache2 restart
```
11. Lanjutkan instalasi dengan mengunjungi 127.0.0.1:8888/sonerezh dengan browser

**belom diisi langkahnya soalnya blom bisa gua install**

12. Install sofware cloud commander yang dibutuhkan untuk managemen file
```
cd ~
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt install nodejs
sudo apt install build-essential
sudo npm i cloudcmd -g
```
13. Tambahkan 1 port host dan guest pada virtual Machine dengan port 3000 dan coba jalankan
```
sudo cloudcmd --port 3000
```
## Konfigurasi
## Maintenance
## Cara Pemakaian
1. Untuk menggunakan **Sonerezh** pengguna harus login terlebih dahulu
2. Setelah login, pengguna akan diarahkan ke halaman utama. Dalam halaman utama terdapat pemutar musik dan daftar lagu beserta data lagu (judul, penyanyi, album, durasi) yang sudah pengguna masukkan pada database **Sonerezh**
3. Menu **Artist** dapat digunakan untuk mengurutkan dan mengelompokkan lagu berdasarkan data penyanyi
4. Menu **Album** dapat digunakan untuk mengurutkan dan mengelompokkan lagu berdasarkan data album
5. Menu **Playlist** dapat digunakan untuk melihat daftar *playlist* yang dibuat oleh pengguna. Pengguna dapat menambahkan lagu pada *playlist* yang sudah tersedia, ataupun dapat membuat *playlist* baru
6. Menu **Database Update** dapat digunakan untuk me-*refresh* database agar membaca lagu yang baru saja dimasukkan ke dalam database
7. Menu **Settings** dapat digunakan untuk mengkonfigurasi aplikasi **Sonerezh** sesuai keinginan.
8. Menu **User** dapat digunakan untuk mengatur daftar user yang dapat mengakses lagu pengguna. Pengguna dapat menambahkan, menghapus, dan mengganti role dari para user sesuai keinginan.
9. Management Lagu
 ## Pembahasan
 ## Referensi 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczNTUxNjE4LDE1OTg1OTEwMDIsNjIzNj
QwMDQ3XX0=
-->
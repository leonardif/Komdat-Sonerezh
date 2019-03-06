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
Playlistsudo apt-get install apache2
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
sudo service apache2 restartPlaylist
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
    ErrorLog    /var/log/apache2/demo.sonerePlaylistzh.bzh-error.log
</VirtualHost>
```
10. Akrifkan *site* nya dan restart Apache
```
sudo a2ensite sonerezh
sudo service apache2 restart
```

11. Lanjutkan instalasi dengan mengunjungi `<host>:<port>/sonerezh` dengan browser. Akan muncul tampilan seperti berikut
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/sonerezh%201.PNG)

* Cek kembali semua *requirement* yang diperlukan
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/sonerezh%202.PNG)

* Isi konfigurasi database
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/sonerezh%203.PNG)

* Isi data diri
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/sonerezh%204.PNG)

Setelah mengklik next, akan muncul tampilan untuk login
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/login.PNG)

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
Pada Sonerezh dapat dilakukan beberapa konfigurasi umum:
<<<<<<< HEAD
* Mengonversi file audio
* Mengganti direktori dari database musik
* Memungkinkan notifikasi email
* Mengatur manajemen database
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/setting.PNG)

## Maintainance Lagu
1. Pada Sonerezh, kita dapat memasukan lagu menggunakan 
```
$ cloudcmd --port 3000
```
2. Akan muncul tampilan seperti berikut
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/cloudcmd.PNG)

3. Untuk memasukan lagu ke dalam database lagu, masukan lagu ke direktori yang telah di set sebelumnya
* Mengunduh lagu
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/download%20lagu.PNG)
* Sebelum dipindah
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/lala%20belom%20pindah.PNG)
* Setelah dipindah
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/lala%20udah%20pindah.PNG)

## Cara Pemakaian
1. Untuk menggunakan **Sonerezh** pengguna harus login terlebih dahulu
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/login.PNG)
2. Setelah login, pengguna akan diarahkan ke halaman utama.
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/home.PNG)
3. Menu **Artist** menampilkan lagu berdasarkan artis
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/artist.PNG)
4. Menu **Album** menampilkan lagu berdasarkan album
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/albums.PNG)
5. Menu **Playlist** menampilkan daftar *playlist* yang dibuat oleh pengguna. Pengguna dapat menambahkan lagu pada
*playlist* yang sudah ada ataupun membuat *playlist* baru
![](https://github.com/leonardif/Komdat-Sonerezh/blob/master/Dokumentasi/playlist.PNG)
6. Menu **Database Update** digunakan untuk memperbaharui database
7. Menu **Settings** digunakan untuk mengatur aplikasi **Sonerezh**.
8. Menu **User** dapat digunakan untuk mengatur daftar user yang dapat mengakses lagu pengguna.

 ## Pembahasan
 **Sonerezh** dibangun menggunakan bahasa pemrograman `PHP` dengan framework `CakePHP` dan database dari `MySql`. Aplikasi ini adalah aplikasi pemutar lagu secara online dari koleksi pribadi yang sudah dimasukan ke dalam database.
 
 **Sonerezh** punya beberapa kelebihan:
 * Ringan saat digunakan
 * Memiliki tingkat keamanan yang cukup terjamin
 * Memiliki fitur konversi format lagu
 * Memiliki fitur pencarian yang lengkap

Namun, **Sonerezh** juga punya beberapa kekurangan:
* Tidak adanya verifikasi email sehingga tidak bisa dipertanggungjawabkan
* Ada beberapa bug pada *Playlist* 

Jika dibandingkan dengan music player lain seperti **Spotify**, **Sonorezh** memiliki beberapa keunggulan dan kekurangan, diantaranya adalah : 
* Dengan **Sonorezh** pengguna dapat mendengarkan lagu yang ia punya secara online dan dapat pula diakses oleh pengguna lain yang diizinkan oleh admin. Sedangkan pada **Spotify** pengguna hanya dapat mendengarkan lagu yang tersedia pada spotify.
* **Sonorezh** gratis untuk seluruh fiturnya, sedangkan untuk mendapatkan seluruh fitur pada **Spotify** pengguna harus mengaktifkan premium member
* Demgan **Sonorezh** pengguna dapat mengkonversi file audio yang diinginkan karena memiliki plug-in ffmpeg, sedangkan pada **Spotify** tidak bisa
* Dengan **Sonerezh** pengguna dapat mengubah, menambah, dan menyunting lagu yang diinginkan dengan cloud cmd, sedangkan dengan **Spotify** tidak bisa
* Tampilan pada **Spotify** yang jauh lebih interaktif dari pada **Sonerezh**



 ## Referensi 
* [Sonerezh](https://www.sonerezh.bzh) - Sonerezh Official Website
* [Sonerezh Github](https://github.com/sonerezh/sonerezh) - Sonerezh Github Documentation

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczNTUxNjE4LDE1OTg1OTEwMDIsNjIzNj
QwMDQ3XX0=
-->

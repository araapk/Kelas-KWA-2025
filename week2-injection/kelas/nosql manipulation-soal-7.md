# **7. NoSQL Manipulation**

## **7.1 [Soal]**
Eksploitasi kerentanan NoSQL Injection pada endpoint login sehingga bisa masuk ke akun tanpa mengetahui password sebenarnya.

## **7.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/login`

## **7.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu **Account** di pojok kanan atas → **Login** sebagai Admin.
    2. Buka link resource di **Burp Suite → Proxy → Open Browser** → pastikan **Intercept On**.
    3. Masuk ke tab **Proxy → HTTP history** dan cari request `PATCH` dengan URL `/rest/products/reviews`.
    4. Klik kanan → **Send to Repeater** → lalu klik **Send**.
    5. Pada tab **Repeater**, modifikasi body JSON di parameter `id` dengan payload berikut:
       ```json
       {
         "id": { "$ne": null },
         "message": "aku anak baik kok"
       }
       ```
       → klik **Send**.  
       Keterangan: `$ne` = *not equal*, sehingga query akan dieksekusi dengan kondisi `id != null` (selalu benar).
    6. Masuk ke halaman OWASP Juice Shop pada salah satu produk, lalu ubah **reviews**.  
       Semua reviews sebelumnya akan berubah menjadi review baru yang kita buat.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-10 201215" src="https://github.com/user-attachments/assets/daa40a5b-bd1a-4e91-8976-9e723b90766b" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 201455" src="https://github.com/user-attachments/assets/8f44e328-6c41-40f9-ad9d-135cf40a4f48" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 202237" src="https://github.com/user-attachments/assets/116c9759-77ab-4aec-be3a-2c35be80e605" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 202331" src="https://github.com/user-attachments/assets/ceb0c1f5-0ac9-4a19-8c21-da6a1b6a8135" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Aplikasi tidak melakukan validasi yang tepat terhadap struktur JSON di body request. MongoDB (atau database NoSQL serupa) mengeksekusi `$ne:null` sebagai kondisi universal yang benar.
    3. **Refleksi:** Membuktikan bahwa NoSQL juga rentan terhadap injection. Sama seperti SQL, input pengguna harus difilter/di-sanitize, dan query harus memakai parameterized query atau ORM yang aman.

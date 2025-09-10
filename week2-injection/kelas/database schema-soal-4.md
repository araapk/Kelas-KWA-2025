# **4. Database Schema**

## **4.1 [Soal]**
Eksploitasi SQL Injection untuk menampilkan struktur database Juice Shop (tabel dan kolom) melalui fitur pencarian.

## **4.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/login`

## **4.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu Account di pojok kanan atas → Login.
    2. Buka link resource di Burp Suite → Proxy → Open Browser → pastikan **Intercept On**.
    3. Masuk ke tab **Proxy → HTTP history** dan cari request dengan URL `/rest/products/search?q=`.
    4. Klik kanan → **Send to Repeater** → lalu klik **Send**.
    5. Manipulasi parameter `q` untuk memastikan query benar-benar diproses oleh database.
    6. Gunakan payload awal untuk menyesuaikan jumlah kolom menjadi 9:
       ```
       test'))+UNION+SELECT+'1','2','3','4','5','6','7','8','9'--
       ```
       → klik **Send**.
    7. Gunakan payload kedua untuk menampilkan tabel dari struktur database:
       ```
       test'))+UNION+SELECT+'1','2','3','4','5','6','7','8',sql+FROM+sqlite_schema--
       ```
       → klik **Send**.  
       `sqlite_schema` digunakan untuk mengekstrak definisi seluruh tabel dan kolom dari database.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-10 151133" src="https://github.com/user-attachments/assets/14b8c468-cebf-4519-8773-39abe77d53eb" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 151210" src="https://github.com/user-attachments/assets/fbc5d6b9-d105-4117-835c-3b5559914c81" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 151444" src="https://github.com/user-attachments/assets/7ff66e72-4cee-4d44-a420-cb2329691638" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 151556" src="https://github.com/user-attachments/assets/e568e841-f105-476e-8194-ad910078e6d7" />

- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Dengan menyesuaikan jumlah kolom pada `UNION SELECT`, query SQL berhasil dieksekusi dan menampilkan struktur database.
    3. **Refleksi:** Tantangan ini menunjukkan pentingnya parameterized query dan validasi input, karena input yang tidak disanitasi dapat mengekspose struktur internal database yang bisa dimanfaatkan attacker untuk serangan lanjutan seperti dump data user.

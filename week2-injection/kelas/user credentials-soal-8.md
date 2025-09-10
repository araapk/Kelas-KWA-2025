# **8. User Credentials**

## **8.1 [Soal]**  
Eksploitasi kerentanan SQL Injection pada endpoint pencarian produk sehingga bisa mendapatkan kredensial user (email, password hash, role, dll).

## **8.2 [Link resource untuk latihan]**  
`https://juice-shop.herokuapp.com/#/login`

## **8.3 [Jawaban + Bukti]**  
- **Step-by-step yang sudah dicoba:**  
    1. Klik menu **Account** di pojok kanan atas → **Login**.  
    2. Buka link resource di **Burp Suite → Proxy → Open Browser** → pastikan **Intercept On**.  
    3. Masuk ke tab **Proxy → HTTP history** dan cari request `GET` dengan URL `/rest/products/search?q=...`.  
    4. Klik kanan → **Send to Repeater** → lalu klik **Send**.  
    5. Pada tab **Repeater**, modifikasi parameter `q` dengan payload berikut untuk mengidentifikasi schema tabel `Users`:  
       ```
       test'))+UNION+SELECT+'1','2','3','4','5','6','7','8',sql+FROM+sqlite_schema--
       ```  
       → klik **Send**.  
    6. Setelah mengetahui struktur tabel, ubah payload agar jumlah kolom sesuai, misalnya:  
       ```
       test'))+UNION+SELECT+id,email,password,role,deluxeToken,lastLoginIp,profileImage,totpSecret,isActive+FROM+Users--
       ```  
       → klik **Send**.  
    7. Jika berhasil, response JSON akan menampilkan daftar lengkap user beserta email, hash password, role, dan informasi akun lainnya.  

- **Screenshot terminal/browser:**  
  <img width="1920" height="1020" alt="Screenshot 2025-09-10 204518" src="https://github.com/user-attachments/assets/4a132159-b569-4838-a756-e5143ef83ac2" />
  <img width="1920" height="1020" alt="Screenshot 2025-09-10 204603" src="https://github.com/user-attachments/assets/76f61ff5-8e9a-458f-bb2c-ee30c17dc360" />
  <img width="1920" height="1020" alt="Screenshot 2025-09-10 211108" src="https://github.com/user-attachments/assets/59bda950-bc09-4692-bb1d-588014b9e00d" />


- **Catatan hasil percobaan:**  
    1. **Hasil:** Berhasil.
    2. **Alasan:** Query pencarian produk tidak menggunakan parameterized query, sehingga attacker bisa menyisipkan `UNION SELECT` untuk mengakses data sensitif.  
    3. **Refleksi:**  
       - SQL Injection sangat berbahaya karena bisa mengakibatkan kebocoran data kredensial.  
       - Sanitasi input dan penggunaan **prepared statements** sangat penting untuk mencegah hal ini.  

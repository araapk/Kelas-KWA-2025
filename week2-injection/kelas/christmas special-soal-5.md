# **5. Christmas Special**

## **5.1 [Soal]**
Dapatkan diskon Christmas Special dengan cara mengeksploitasi query SQL pada parameter search, sehingga sistem menampilkan kode voucher rahasia.

## **5.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/login`

## **5.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu Account di pojok kanan atas → Login.
    2. Buka link resource di Burp Suite → Proxy → Open Browser → pastikan **Intercept On**.
    3. Masuk ke tab **Proxy → HTTP history** dan cari request dengan URL `/rest/products/search?q=`.
    4. Klik kanan → **Send to Repeater** → lalu klik **Send**.
    5. Manipulasi parameter `q` untuk memastikan query benar-benar diproses oleh database.
    6. Gunakan payload awal untuk mencari christmas special-nya:
       ```
       test'))+UNION+SELECT+*+FROM+Products--
       ```
       → klik **Send**.
    7. Cari christmas specialnya, jika sudah ada masuk ke halaman product yang ada di OWASP Juice Shop dan tambahkan product ke keranjang.
    8. Cek apakah christmas specialnya udah ada di keranjang atau belum.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-10 154228" src="https://github.com/user-attachments/assets/19ace855-690c-4981-9ae7-e2b95cd7889a" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 163005" src="https://github.com/user-attachments/assets/694eb9c7-2271-4b2c-ac54-482864aeee32" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** SQLi dimanfaatkan untuk memanipulasi query produk sehingga menampilkan data khusus yang seharusnya tersembunyi.
    3. **Refleksi:** Kasus ini menunjukkan bagaimana insecure search query dapat dimanfaatkan untuk mendapatkan diskon/voucher palsu.

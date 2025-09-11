# **4. Five-Star Feedback**

## **4.1 [Soal]**
Eksploitasi Broken Access Control untuk memberikan atau memanipulasi feedback rating di Juice Shop tanpa hak yang sah, khususnya memberikan “five-star” pada produk milik user lain atau produk yang seharusnya tidak bisa diakses.

## **4.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Broken%20Access%20Control`

## **4.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Buka website Juice Shop:
        ```
        https://juice-shop.herokuapp.com
        ```
    2. Tekan F12 → Sources → buka file `main.js` untuk melihat route aplikasi.
    3. Temukan route untuk Admin Section:
        ```
        /#/administration
        ```
    4. Masukkan URL langsung di browser:
        ```
        https://juice-shop.herokuapp.com/#/administration
        ```
    5. Cari feedback/comments yang bintang 5 dan hapus commentsnya.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-11 114600" src="https://github.com/user-attachments/assets/a053165b-41d1-40a7-a2f3-43afd3cff13e" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Server tidak melakukan validasi kepemilikan produk atau hak akses user sebelum menerima feedback.
    3. **Refleksi:** Challenge ini menegaskan pentingnya validasi server-side agar user hanya dapat memberikan feedback pada produk yang sah atau diperbolehkan.

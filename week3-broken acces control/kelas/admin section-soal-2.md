# **2. Admin Section**

## **2.1 [Soal]**
Eksploitasi Broken Access Control untuk mengakses halaman Admin Section di Juice Shop.

## **2.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Broken%20Access%20Control`

## **2.3 [Jawaban + Bukti]**
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
    5. Halaman pertama kali menampilkan `403` karena belum login sebagai admin.
    6. Login dengan akun admin (jika punya) → atau jika ingin eksploitasi Broken Access Control, manipulasi cookie/JWT role menjadi `admin`.
    7. Refresh halaman → halaman Admin Section berhasil diakses.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-11 111210" src="https://github.com/user-attachments/assets/ddf6334d-9776-465f-a719-a325c5baef1a" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 111649" src="https://github.com/user-attachments/assets/0a659715-9e38-4ce4-9457-1a92797e81c9" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 111556" src="https://github.com/user-attachments/assets/5ab43315-b20b-49dd-b469-527d331f4e4d" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 111641" src="https://github.com/user-attachments/assets/7d902f34-10a6-4deb-9a9f-9d14348d6e40" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Server hanya mengandalkan URL obscurity atau role yang bisa dimanipulasi; validasi server-side tidak cukup.
    3. **Refleksi:** Challenge ini menunjukkan Broken Access Control, karena halaman sensitif bisa diakses tanpa hak yang sah.

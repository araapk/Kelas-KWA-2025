# **2. Login Jim**

## **2.1 [Soal]**
Eksploitasi SQL Injection untuk login sebagai Jim di Juice Shop.

## **2.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Injection&showDisabledChallenges=false`

## **2.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu Account di pojok kanan atas → Login.
    2. Pada field Email, masukkan payload `jim@juice-sh.op'--`. Cara mendapatkan Email-nya Jim dapat melihat reviews pada produk yang ada di home. Payload ini menutup query SQL sehingga server langsung memilih user `jim@juice-sh.op` tanpa memverifikasi password.
    3. Isi password secara bebas, contoh `12345`.
    4. Klik Log in.

- **Screenshot terminal/browser:**
<img width="1920" height="1032" alt="Screenshot 2025-09-09 232935" src="https://github.com/user-attachments/assets/d83fefa0-b020-4d65-8090-7efabb3386e7" />
<img width="1920" height="1032" alt="Screenshot 2025-09-09 235712" src="https://github.com/user-attachments/assets/042f28ca-cdc7-4d64-9f15-d0d52ec1790f" />
<img width="1920" height="1032" alt="Screenshot 2025-09-09 235728" src="https://github.com/user-attachments/assets/2facf6cf-ed42-4676-8033-0a6620219134" />

- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Payload menutup query SQL dan memilih user `jim@juice-sh.op` tanpa password.
    3. **Refleksi:** SQLi dapat digunakan untuk login ke akun tertentu hanya dengan mengetahui email.

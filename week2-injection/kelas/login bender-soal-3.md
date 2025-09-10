# **3. Login Bender**

## **3.1 [Soal]**
Eksploitasi SQL Injection untuk login sebagai Bender di Juice Shop.

## **3.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Injection&showDisabledChallenges=false`

## **3.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu Account di pojok kanan atas → Login.
    2. Pada field Email, masukkan payload `bender@juice-sh.op'--`. Cara mendapatkan Email-nya Bender dapat melihat reviews pada produk yang ada di home. Payload ini memaksa server memilih langsung user dengan email tersebut tanpa memeriksa password.
    3. Isi password secara bebas, contoh `12345`.
    4. Klik Log in.

- **Screenshot terminal/browser:**
<img width="1920" height="1032" alt="Screenshot 2025-09-09 235920" src="https://github.com/user-attachments/assets/7005bb65-9a24-4c7f-9c40-6ae492734b45" />
<img width="1920" height="1032" alt="Screenshot 2025-09-10 000022" src="https://github.com/user-attachments/assets/1eb763bb-c653-4329-a43f-685da63dc3b5" />
<img width="1920" height="1032" alt="Screenshot 2025-09-10 000035" src="https://github.com/user-attachments/assets/7fdd895f-c3ab-4182-94b8-c9b5b47e00c9" />

- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Query SQL dimanipulasi sehingga login bypass untuk akun `bender@juice-sh.op`.
    3. **Refleksi:** SQLi memungkinkan akses ke akun spesifik hanya dengan alamat email.

# **1. Login Admin**

## **1.1 [Soal]**
Eksploitasi SQL Injection untuk login sebagai Admin di Juice Shop.

## **1.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Injection&showDisabledChallenges=false`

## **1.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Klik menu Account di pojok kanan atas → Login.
    2. Pada field Email, masukkan payload `' OR true--`. Payload ini dimaksudkan agar query login selalu bernilai true, sehingga server tidak perlu memeriksa password.
    3. Isi password secara bebas, contoh `12345`.
    4. Klik Log in.

- **Screenshot terminal/browser:**
<img width="1920" height="1032" alt="Screenshot 2025-09-09 231923" src="https://github.com/user-attachments/assets/a3dd2e85-9b8c-48ac-a2b0-a851bf3216ff" />
<img width="1920" height="1032" alt="Screenshot 2025-09-09 232033" src="https://github.com/user-attachments/assets/801740c2-0f28-4227-b982-3b657e94b693" />

- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Payload `' OR true--` menutup query asli yang membuat query login selalu true, sehingga bypass password.
    3. **Refleksi:** SQLi dasar efektif untuk masuk ke akun admin tanpa kredensial valid.

# **5. Forged Feedback**

## **5.1 [Soal]**
Eksploitasi Broken Access Control untuk membuat atau memalsukan feedback seolah-olah berasal dari user lain (bukan akun kita sendiri), dengan cara memanipulasi parameter `UserId` pada request `POST /api/Feedbacks`.

## **5.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Broken%20Access%20Control`

## **5.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Login ke akun Juice Shop (user biasa).  
    2. Buka fitur Customer Feedback → isi form feedback.  
    3. Intercept request di **Burp Suite** untuk endpoint:
       ```
       POST /api/Feedbacks
       ```
    4. Modifikasi body request:  
       - Hapus field `captchaId` dan `captcha` (agar validasi CAPTCHA tidak terpanggil).  
       - Ganti nilai `UserId` dari milik sendiri (misalnya `3`) menjadi user lain (misalnya `1`).  
       Contoh payload:
       ```
      {
          "UserId":1,
          "captchaId":84,
          "captcha":"-10",
          "comment":"enak si tp bisa ditingkatin lagi (***der@juice-sh.op)",
          "rating":3
      }
       ```
    5. Forward request ke server.  
    6. Buka halaman **Administration** untuk memverifikasi feedback tersebut tercatat atas nama user lain.

- **Screenshot terminal/browser:**
<img width="1920" height="1032" alt="Screenshot 2025-09-16 220508" src="https://github.com/user-attachments/assets/b466e3f4-12c8-4943-9d42-8685e8c0db70" />
<img width="1920" height="1032" alt="Screenshot 2025-09-16 223055" src="https://github.com/user-attachments/assets/fcd4ca49-ddf2-46fb-b6cf-e8d6455e69ba" />
<img width="1920" height="1032" alt="Screenshot 2025-09-16 223124" src="https://github.com/user-attachments/assets/f5c5d69b-900d-4af2-a3f6-aba86678fbc9" />
<img width="1920" height="1032" alt="Screenshot 2025-09-16 223142" src="https://github.com/user-attachments/assets/e307a38a-f834-41c9-bd60-4e5f1934ee25" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil. 
    2. **Alasan:** Server tidak melakukan validasi kepemilikan `UserId` dan mempercayai input dari client.  
    3. **Refleksi:** Celah ini menunjukkan lemahnya kontrol akses di sisi server. Input sensitif seperti `UserId` tidak boleh diambil dari client, melainkan harus divalidasi berdasarkan session/token yang sah.

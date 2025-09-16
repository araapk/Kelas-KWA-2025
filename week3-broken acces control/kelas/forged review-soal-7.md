# **7. Forged Review**

## **7.1 [Soal]**
Eksploitasi Broken Access Control untuk membuat atau memodifikasi review produk seolah-olah berasal dari user lain, dengan cara memanipulasi parameter `author` (atau `UserId`) pada request `POST /rest/products/:id/reviews` maupun `PUT /rest/products/:id/reviews`.

## **7.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Broken%20Access%20Control`

## **7.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Login ke akun Juice Shop (user biasa).  
    2. Buka halaman produk → buat review sederhana (contoh: "good one"). 
    3. Intercept request menggunakan Burp Suite pada endpoint:
       ```
       PUT /rest/products/1/reviews
       ```
    4. Analisis body request. Terlihat ada parameter:
       ```
      {
        "message": "good one",
        "author": "Anonymous"
      }
       ```
    5. Modifikasi parameter author dengan username lain, misalnya "admin" atau "bendergokil".
       Contoh payload hasil modifikasi:
       ```
       {
          "message": "good one",
          "author": "admin"
        }
       ```
    7. Kirim ulang request (Send via Burp Repeater).
    8. Reload halaman produk → review baru muncul dengan nama author sesuai manipulasi (bukan akun kita sendiri).

- **Screenshot terminal/browser:**
<img width="1920" height="1032" alt="Screenshot 2025-09-16 220508" src="https://github.com/user-attachments/assets/68585474-e0d0-4f60-b3bb-ec78514753ef" />
<img width="1920" height="1032" alt="Screenshot 2025-09-16 232509" src="https://github.com/user-attachments/assets/4f32e189-b6ee-4f8c-9570-f721f280b6bf" />
<img width="1920" height="1032" alt="Screenshot 2025-09-16 232614" src="https://github.com/user-attachments/assets/0c158bfc-84c0-464d-8aa8-08a536e8147a" />
<img width="1920" height="1020" alt="Screenshot 2025-09-16 232701" src="https://github.com/user-attachments/assets/215e5c5a-a5fa-416f-bae2-5a5e820e0981" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil. 
    2. **Alasan:** Server tidak memvalidasi kecocokan antara user yang sedang login dengan field `author`. Input dari client langsung dipakai untuk menentukan siapa penulis review.
    3. **Refleksi:** Celah ini mengindikasikan Insecure Direct Object Reference (IDOR) dan lemahnya kontrol akses di server. Review bisa dipalsukan atau diubah atas nama user lain tanpa otorisasi.

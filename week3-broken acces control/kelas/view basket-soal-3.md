# **3. View Basket**

## **3.1 [Soal]**
Eksploitasi Broken Access Control untuk melihat isi shopping basket milik user lain di Juice Shop.

## **3.2 [Link resource untuk latihan]**
`https://juice-shop.herokuapp.com/#/score-board?categories=Broken%20Access%20Control`

## **3.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Buka website Juice Shop:
        ```
        https://juice-shop.herokuapp.com
        ```
    2. Buka Burp Suite → aktifkan intercept → buka halaman View Basket.
    3. Tangkap HTTP request untuk mendapatkan basket sendiri. Contoh URL request:
        ```
        http://juice-shop.herokuapp.com/rest/basket/1
        ```
        Keterangan: (1 = basket ID milik user saat ini).

    4. Modifikasi parameter `basket ID` dari `1` menjadi `2` atau ID lain yang dicurigai milik user lain.
    5. Forward request yang sudah dimodifikasi.
    6. Response menampilkan isi basket user lain → menandakan Broken Access Control.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-11 113226" src="https://github.com/user-attachments/assets/a67a8c9c-cecd-45e3-85b3-9ebe492461d8" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 113236" src="https://github.com/user-attachments/assets/c3f9bf2b-b124-4ec4-9e13-a5d33581603b" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 113432" src="https://github.com/user-attachments/assets/dee63953-10b8-4c6a-b65a-467b6c4c4e22" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Server tidak melakukan validasi ownership basket secara benar, sehingga request dengan ID lain tetap diterima.
    3. **Refleksi:** Challenge ini menegaskan pentingnya validasi server-side untuk setiap data sensitif, agar user hanya bisa mengakses data miliknya sendiri.

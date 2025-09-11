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


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.
    2. **Alasan:** Server tidak melakukan validasi ownership basket secara benar, sehingga request dengan ID lain tetap diterima.
    3. **Refleksi:** Challenge ini menegaskan pentingnya validasi server-side untuk setiap data sensitif, agar user hanya bisa mengakses data miliknya sendiri.

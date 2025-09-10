# **2. OS Command Injection, Simple Case**

## **2.1 [Soal]**
Eksploitasi OS Command Injection untuk mendapatkan informasi sistem pada aplikasi PortSwigger Web Security Academy.

## **2.2 [Link resource untuk latihan]**
`https://portswigger.net/web-security/os-command-injection/lab-simple`

## **2.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Buka lab PortSwigger di browser melalui link di atas.  
    2. Klik **View details** pada salah satu produk, kemudian lakukan **Check stock**.  
    3. Buka **Developer Console** di browser (F12 → Console) dan masukkan payload berikut:  
       ```javascript
       fetch('/product/stock', {
         method: 'POST',
         headers: {'Content-Type': 'application/x-www-form-urlencoded'},
         body: 'productId=1&storeId=London;whoami'
       })
       .then(r => r.text())
       .then(t => console.log(t));
       ```
    4. Lihat hasil di console. Jika muncul username sistem (contoh: `peter-4yDI9k`), maka exploit berhasil dijalankan.  

- **Screenshot terminal/browser:**  
<img width="1920" height="1020" alt="Screenshot 2025-09-10 222509" src="https://github.com/user-attachments/assets/975b57d5-bd00-48cd-920b-c24e49240181" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 222621" src="https://github.com/user-attachments/assets/b386d473-8474-41ab-856e-606c386091cc" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil.  
    2. **Alasan:** Payload `;whoami` memaksa aplikasi mengeksekusi perintah sistem tambahan di server setelah parameter normal.  
    3. **Refleksi:** OS Command Injection sederhana dapat digunakan untuk membaca informasi sistem, membuktikan adanya celah kritis pada aplikasi.  

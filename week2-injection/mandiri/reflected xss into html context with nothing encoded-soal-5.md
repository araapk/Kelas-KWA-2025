# **5. Reflected XSS into HTML Context with Nothing Encoded**

## **5.1 [Soal]**
Eksploitasi Reflected XSS pada parameter URL atau input form untuk menjalankan JavaScript di halaman PortSwigger Web Security Academy. Parameter ini berada di HTML context dan nothing encoded, sehingga payload langsung dieksekusi.

## **5.2 [Link resource untuk latihan]**
`https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded`

## **5.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
  1. Buka lab PortSwigger di browser melalui link di atas.  
  2. Periksa parameter URL atau form input yang rentan, misalnya `search`.  
  3. Siapkan payload XSS sederhana:  
     ```
    "><script>alert(1)</script>
     ```
     
  4. Kirim payload menggunakan console browser dengan manipulasi URL:  
    ```
    const url = new URL("https://0a8e001f0472f29d807dc19e0074005d.web-security-academy.net/");
    url.searchParams.set('search', '"><script>alert(1)</script>');
    window.location.href = url.toString();
    ```
     Hasilnya **alert box muncul di browser**, membuktikan parameter rentan terhadap Reflected XSS.

- **Screenshot terminal/browser:**  
<img width="1920" height="1080" alt="Screenshot 2025-09-11 001230" src="https://github.com/user-attachments/assets/8e7889ac-c63d-4212-93e2-abc46beba37b" />
<img width="1920" height="1020" alt="Screenshot 2025-09-11 001249" src="https://github.com/user-attachments/assets/403ca931-01e7-4d81-a314-381ce4560a49" />


- **Catatan hasil percobaan:**
  1. **Hasil:** Berhasil mengeksekusi JavaScript.  
  2. **Alasan:** Input tidak disanitasi atau di-encode → JavaScript dieksekusi secara langsung di HTML context.  
  3. **Refleksi:** Reflected XSS berbahaya karena memungkinkan eksekusi kode di browser korban, berpotensi mencuri cookie, session, atau melakukan aksi lain atas nama user.


# **1. Unprotected Admin Functionality**

## **1.1 [Soal]**
Eksploitasi Broken Access Control dengan cara mengakses panel admin yang seharusnya terbatas, tetapi ternyata bisa diakses publik tanpa autentikasi. Tujuan akhirnya adalah menghapus user `carlos` melalui panel admin.

## **1.2 [Link resource untuk latihan]**
`https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality`

## **1.3 [Jawaban + Bukti]**
- **Step-by-step yang sudah dicoba:**
    1. Buka halaman utama lab.
    2. Coba akses direktori tersembunyi menggunakan endpoint `/robots.txt`:
       ```
       https://0a9b0038041731ce808badda0c000eb.web-security-academy.net/robots.txt
       ```
    4. Respon menunjukkan ada direktori yang tidak boleh di-crawl, misalnya:
       ```
       User-agent: *
       Disallow: /administrator-panel
       ```
    5. Setelah tahu path asli (contoh `/administrator-panel`), langsung buka URL tersebut:
       ```
       https://0a9b0038041731ce808badda0c000eb.web-security-academy.net/administrator-panel
       ```
    5. Di dalamnya terdapat tombol **Delete user `carlos`**.
    7. Klik tombol tersebut → user `carlos` berhasil dihapus.
    8. Status lab berubah menjadi Solved.

- **Screenshot terminal/browser:**
<img width="1920" height="1020" alt="Screenshot 2025-09-16 235405" src="https://github.com/user-attachments/assets/005f8948-69cf-4ecb-aec4-5593c1e075d8" />
<img width="1920" height="1020" alt="Screenshot 2025-09-16 235538" src="https://github.com/user-attachments/assets/b383a9ab-066a-491b-bb6f-fb3880f3b08d" />
<img width="1920" height="1020" alt="Screenshot 2025-09-16 235604" src="https://github.com/user-attachments/assets/0d3fb2bc-1ccd-427e-8a8c-4d4a27686e95" />
<img width="1920" height="1020" alt="Screenshot 2025-09-16 235613" src="https://github.com/user-attachments/assets/0ff704aa-ffa0-4550-abe6-88a42d3b4c1a" />


- **Catatan hasil percobaan:**
    1. **Hasil:** Berhasil. 
    2. **Alasan:** Server tidak melindungi endpoint admin dengan autentikasi. Siapa pun yang mengetahui URL dapat langsung mengakses fungsi sensitif.
    3. **Refleksi:** Ini adalah bentuk Broken Access Control karena tidak ada verifikasi role sebelum membuka halaman admin. Seharusnya server menerapkan proteksi berbasis session/role, bukan hanya menyembunyikan URL.

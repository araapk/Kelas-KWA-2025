# Write-up: Unprotected Admin Functionality with Unpredictable URL

## Deskripsi Kerentanan
Lab ini menguji pemahaman tentang kerentanan di mana fungsionalitas admin yang seharusnya tersembunyi dapat diakses oleh pengguna biasa. Meskipun URL ke panel admin dirancang secara acak dan sulit ditebak, pengembang secara tidak sengaja "membocorkan" URL tersebut melalui file yang dapat diakses publik, seperti file JavaScript.

## Tujuan Lab
Tujuan dari lab ini adalah untuk menemukan panel admin yang tersembunyi, mengaksesnya, dan menghapus pengguna **carlos** untuk menyelesaikan tantangan.

---

## Langkah-langkah Penyelesaian

### 1. Memeriksa Kode Sumber Halaman
Langkah pertama adalah mencari petunjuk yang mengarah ke lokasi panel admin. Meskipun URL-nya dirancang secara acak, petunjuknya sering kali tersembunyi di dalam kode sumber halaman. Kita dapat menggunakan fitur **Developer Tools** di browser (biasanya dengan menekan `F12`) atau melihat kode sumber halaman secara langsung (`view-source`).

Dengan memeriksa kode sumber, kita akan menemukan blok `<script>` JavaScript yang berisi URL yang kita cari:

```javascript
<script>
    var isAdmin = false;
    if (isAdmin) {
        var topLinksTag = document.getElementsByClassName('top-links')[0];
        var adminPanelTag = document.createElement('a');
        adminPanelTag.setAttribute('href', '/admin-p65jj2');
        adminPanelTag.innerText = 'Admin panel';
        topLinksTag.appendChild(adminPanelTag);
        var pTag = document.createElement('p');
        pTag.innerText = ' ';
        topLinksTag.appendChild(pTag);
    }
</script>
```

Pada kode di atas, kita melihat bahwa atribut `href` untuk tautan panel admin diatur ke `/admin-p65jj2`. Perlu diingat bahwa bagian acak (`p65jj2`) akan berbeda untuk setiap sesi lab.

### 2. Mengakses Panel Admin

Setelah mendapatkan URL yang valid, kita dapat mengakses panel admin secara langsung. Cukup tambahkan path yang ditemukan (`/admin-p65jj2`) ke URL dasar lab di bilah alamat browser.

Misalnya, jika URL lab Anda adalah `https://0a5c006503b1f6d2381c22f4e008d00b.web-security-academy.net`, maka URL panel adminnya adalah `https://0a5c006503b1f6d2381c22f4e008d00b.web-security-academy.net/admin-p65jj2`.

### 3. Menghapus Pengguna "carlos"

Setelah berhasil mengakses panel admin, kita akan melihat daftar pengguna. Sesuai dengan tujuan lab, kita harus mencari pengguna bernama **carlos** dan menghapusnya. Klik tombol **Delete** yang ada di sebelah nama pengguna **carlos**.

Setelah berhasil, lab akan selesai dan muncul pesan "Congratulations, you solved the lab!".

---

## Mitigasi Kerentanan

Untuk mencegah kerentanan seperti ini, berikut adalah beberapa langkah mitigasi yang harus diterapkan:

1.  **Jangan Bocorkan URL Sensitif di Kode Klien:** Jangan pernah menyertakan URL atau path sensitif di kode sisi klien (seperti JavaScript, HTML, atau CSS) yang dapat diakses oleh siapa pun. Meskipun URL dibuat acak, seorang penyerang dapat dengan mudah menemukannya dengan memeriksa kode sumber.

2.  **Implementasikan Kontrol Akses Berbasis Peran (Role-Based Access Control):** Ini adalah mitigasi terpenting. Akses ke fungsionalitas admin harus **selalu** dikontrol di sisi server. Saat pengguna mencoba mengakses `/admin-p65jj2`, server harus terlebih dahulu memverifikasi bahwa pengguna tersebut **sudah terotentikasi dan memiliki peran sebagai administrator**. Jika tidak, server harus menolak permintaan tersebut, misalnya dengan mengembalikan kode status **403 Forbidden**.

3.  **Gunakan Otentikasi dan Otorisasi yang Kuat:** Pastikan semua endpoint yang sensitif memerlukan otentikasi yang valid. Setiap permintaan untuk tindakan admin harus menyertakan token otorisasi yang benar untuk memverifikasi identitas dan peran pengguna.

4.  **Minimalkan Paparan Kode:** Jika memungkinkan, letakkan fungsionalitas admin di subdomain yang terpisah atau di jaringan internal. Ini akan mengurangi kemungkinan URL-nya ditemukan oleh pihak eksternal. Namun, tetap terapkan kontrol akses yang ketat sebagai pertahanan utama.

Dengan menerapkan mitigasi ini, bahkan jika URL admin ditemukan, penyerang tidak akan dapat mengakses fungsionalitasnya karena mereka tidak memiliki izin yang diperlukan.
---

## Bukti 
<img width="1920" height="1020" alt="Screenshot 2025-09-17 200422" src="https://github.com/user-attachments/assets/123b7fad-ecdc-40ee-8b4e-426928b61a51" />

<img width="1920" height="1020" alt="Screenshot 2025-09-17 200915" src="https://github.com/user-attachments/assets/fd7d27fb-06b1-4c79-83bc-e7e28f2cc815" />

<img width="1920" height="1080" alt="Screenshot 2025-09-17 200948" src="https://github.com/user-attachments/assets/9382420e-0cd3-448e-a2da-b81ba257e68d" />

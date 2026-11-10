# My Wedding — Awang & Rahma

## Yang sudah disiapkan
- Video penutup tampil sederhana dalam format landscape 16:9 dengan kontrol video langsung.
- `index.html`: undangan utama, desain dan interaksi asli dipertahankan.
- `assets/`: foto, video, audio, poster, QRIS, dan logo dipisahkan dari HTML.
- `admin/index.html`: panel login admin untuk membuat tautan undangan personal.
- `firebase-config.js`: tempat konfigurasi Firebase Web.
- `firestore.rules`: aturan akses database.

## Kualitas media
Seluruh media diekstrak langsung dari HTML sumber sebagai byte asli. Tidak ada proses resize, recompress, transcode, atau perubahan bitrate. Periksa `MEDIA-MANIFEST.json` untuk ukuran, dimensi, dan checksum SHA-256 masing-masing file.

## Mengaktifkan fitur nama tamu (perlu satu kali setup Firebase)
1. Buat project di https://console.firebase.google.com/.
2. Tambahkan aplikasi Web dan salin konfigurasi Firebase ke `firebase-config.js` (ganti semua nilai `ISI_...`). Konfigurasi Web boleh berada di repository publik; jangan pernah memasukkan service-account key atau password ke file ini.
3. Di Firebase Authentication, aktifkan metode **Email/Password** lalu buat akun admin menggunakan email istri Anda.
4. Di `firestore.rules`, ganti `GANTI_DENGAN_EMAIL_ADMIN_ISTRI` dengan email admin tersebut, lalu terbitkan rules di Firestore Database > Rules.
5. Buat database Cloud Firestore dalam mode production.
6. Upload seluruh isi folder proyek ke repository GitHub. Pastikan `index.html` berada di root repository.
7. Aktifkan GitHub Pages: Settings > Pages > Deploy from a branch > `main` > `/ (root)` > Save.
8. Setelah situs aktif, buka `https://NAMA-USER.github.io/NAMA-REPO/admin/` dari HP, lalu login.
9. Ketik nama tamu dan tekan **Buat tautan undangan**. Bagikan tautan yang dihasilkan melalui WhatsApp.

## Catatan keamanan dan privasi
- Tautan personal menggunakan ID dokumen acak sebagai kode undangan. Siapa pun yang memiliki tautan dapat melihat nama penerima pada sampul.
- Hanya email admin yang dicantumkan di Firestore Rules yang boleh membuat dan membaca daftar tamu.
- Jangan mengaktifkan pendaftaran publik pada Authentication. Buat akun admin sendiri melalui Firebase Console.
- Firestore `allow get: if true` diperlukan agar halaman undangan dapat mengambil satu dokumen berdasarkan kode tautan; akses daftar (`list`) tetap khusus admin.

## Catatan penting
Fitur database belum dapat aktif sampai Anda mengisi konfigurasi Firebase dan menerbitkan Firestore Rules. Website statis dan seluruh media sudah dipisahkan serta siap diunggah ke GitHub Pages. Tidak ada konfigurasi akun atau kredensial yang dibuat-buat di dalam proyek ini.

# PANDUAN INSTALASI - Apk Sekolah Mantap v4.2
Backend = Google Apps Script (REST API). Frontend = GitHub Pages (HTTPS, sehingga kamera scan QR & presensi wajah bisa dipakai).
Nama aplikasi berubah dari "Administrasi GTK SDN 047 Tarakan" menjadi **Apk Sekolah Mantap**. Nama folder `sdn047-tarakan`, nama database Sheets, dan folder Drive **sengaja tidak diubah** agar data lama tetap terpakai.

## A. UPGRADE DARI v3.5 (data lama tetap aman)
1. Buka proyek Apps Script lama -> ganti seluruh isi `Kode.gs` dengan `Kode.gs` v4.2 (file ini).
2. Pilih fungsi `setupAppEnvironment` -> **Run** (cukup sekali; aman diulang). Proses membuat +/- 50 sheet baru dan menambah kolom baru (mis. Status & tanggal lahir pada Siswa), bisa 1-2 menit. Pastikan log bertuliskan "Setup selesai". Nama aplikasi di Pengaturan otomatis menjadi "Apk Sekolah Mantap".
3. **Deploy -> Manage deployments -> pensil -> New version -> Deploy** (URL /exec tetap sama).
4. Frontend: ekstrak ZIP, salin `js/config.js` lama Anda (berisi URL /exec) menimpa `js/config.js` di folder baru, lalu:
```
git add .
git commit -m "v4.2 Apk Sekolah Mantap"
git push
```
5. Buka situs, tekan Ctrl+Shift+R. Kartu login harus menampilkan **Versi 4.2**.

## B. INSTALASI BARU
1. https://script.google.com -> Proyek baru -> isi `Code.gs` dengan `Kode.gs` (ganti nama file menjadi **Kode**).
2. Jalankan `setupAppEnvironment` (izinkan Drive, Sheets, Gmail, Docs).
3. Deploy -> New deployment -> Web app: Execute as **Me**, Who has access **Anyone** -> salin URL /exec.
4. Isi `js/config.js` (ganti `PASTE_URL_EXEC_DI_SINI`), push ke repository GitHub **Public**, aktifkan Pages (Settings -> Pages -> branch main / root, Enforce HTTPS). Langkah git sama seperti panduan v3.5 (`git init`, `git add .`, `git commit`, `git remote add origin ...`, `git push -u origin main`, password = Personal Access Token).
5. Akun admin awal: username `ujangilham`. **Segera ganti password** di menu Pengaturan.

Setiap mengubah `Kode.gs`: Deploy -> Manage deployments -> New version.

## C. MENU DAN FITUR BARU (dikelompokkan di sidebar, ada kotak cari menu)
| Kelompok | Isi |
|---|---|
| Profil Sekolah | Visi & Misi (Admin dapat mengubah), Struktur Organisasi (bagan pohon otomatis dari kolom Atasan) |
| Data Master | Guru, Kelas, Siswa (kini ada Status Aktif/Mutasi/Lulus/Keluar), Mata Pelajaran, Tahun Ajaran |
| Akademik | Jadwal Pelajaran (tampilan grid per kelas), Kehadiran Siswa, Scan QR, Laporan Kehadiran, Presensi Wajah, Daftar Wajah, Kartu QR Massal, **Nilai Siswa (Kurikulum Merdeka)**, Kaldik (kalender bulanan), Jurnal, Perkembangan, Hafalan |
| Eskul & Kokurikuler | Ekstrakurikuler, Kehadiran Ekstrakurikuler, Kokurikuler (8 Dimensi Profil Lulusan), Kehadiran Kokurikuler (ada **Isi Massal**) |
| Guru Pintar | Generator RPP/Modul Ajar, Modul Ajar Tersimpan, Bank Soal (+ cetak lembar soal), Kuis Interaktif, Ice Breaking, Kartu Guru (QR), Arsip Dokumen |
| Kesiswaan | Pendaftaran Siswa Baru (tombol "Jadikan siswa"), Perizinan Siswa, Bimbingan Konseling, Tata Tertib, Catatan Pelanggaran, Buku Mutasi, Buku Kelulusan, Buku Prestasi, Kartu Pelajar (QR presensi) |
| Sarana & Prasarana | Inventaris Barang, Peminjaman Sarpras, Denah Sekolah & Ruang |
| Perpustakaan | Dashboard, Manajemen Buku, Anggota, Peminjaman & Pengembalian |
| Keuangan | Pembayaran Siswa (kuitansi), Tabungan, Pendapatan, Pengeluaran, Neraca, Honorarium GTK (slip), PIP |
| Unit Kesehatan Sekolah | Rekam Medis, Riwayat Kunjungan (obat otomatis mengurangi stok), Stok Obat |
| Koperasi Sekolah | Manajemen Stok, Penjualan (stok & saldo E-Money otomatis), E-Money, Laporan Keuangan |
| Jadwal Piket | Piket Guru, Piket Siswa |
| Manajemen Rapat | Jadwal, Notulen, Presensi (isi massal dari Data Guru), Follow Up |
| Organisasi Kelas | OSIS, Organisasi Kelas |
| Game Edukatif | Matematika Cepat, Teka-Teki Sains, Kuis Sejarah, Rantai Kata, Tebak Kata, Ular Tangga Edukatif, Susunan Balok Pintar, Teka-Teki Cari Kata, Kuis Al-Quran |
| Alat Pembelajaran | Spin Wheel, Pengacak Siswa, Pasangan Random, Alat Peraga 3D, Kalkulator Konversi, Papan Tulis, Mind Mapping, Peta Interaktif, Virtual Lab |
| Administrasi & Sistem | Surat Menyurat, Pengumuman, Backup & Hapus Data, Arsip Rekap & Sertifikat, Pengguna, Pengaturan |

### Persentase kehadiran
Persentase **Hadir, Sakit, Izin, Alpa** tampil di: Dashboard (hari ini + akumulasi tahun ajaran), halaman Kehadiran Siswa (tanggal terpilih + akumulasi), dan Laporan Kehadiran (per filter, plus kolom % per siswa di tabel/Excel/Word/PDF).

### Nilai Kurikulum Merdeka
Input per siswa & mata pelajaran: sampai 4 Sumatif Lingkup Materi, Sumatif Akhir Semester/Tahun, serta Tujuan Pembelajaran tercapai / perlu penguatan. Nilai formatif tidak masuk nilai rapor. **Nilai Akhir** = rata-rata (rerata sumatif lingkup materi, sumatif akhir); **deskripsi capaian** disusun otomatis. KKTP per mapel diisi di Data Mata Pelajaran (bawaan di Pengaturan, 75). Tombol **Cetak Rapor** tersedia.
Rumus ini adalah pilihan bawaan; bila sekolah memakai bobot lain, ubah fungsi `hitungNilai` di Kode.gs.

## D. HAK AKSES (revisi v4.1) — ON/OFF per fitur per pengguna
**Prinsip:** semua staf dapat **melihat** semua fitur. **Menambah, mengubah, dan menghapus** data hanya jika Admin menyalakan **ON** hak akses fitur itu untuk pengguna tersebut. **OFF = hanya melihat.** Game Edukatif dan Alat Pembelajaran bebas untuk semua pengguna.

**Cara mengatur (Admin):** menu **Pengguna & Hak Akses** -> tombol **Hak Akses** pada baris pengguna -> nyalakan/matikan saklar per fitur (dikelompokkan seperti sidebar) -> Simpan. Perubahan berlaku dalam beberapa menit tanpa pengguna harus login ulang.
- Fitur khusus yang juga bisa di-ON/OFF: Kehadiran Siswa (input/ubah), Scan QR Presensi, Presensi Wajah, Daftar Wajah Siswa.
- **Admin** selalu memiliki semua hak. Menu Pengguna, Pengaturan, dan Backup & Hapus Data tetap khusus Admin.
- **Guru Kelas tetap dibatasi pada kelasnya sendiri**, walaupun hak akses fitur ON (siswa, nilai, perizinan, tabungan, infaq, dll. hanya kelasnya).
- Guru non-wali kelas hanya melihat data yang mereka buat sendiri pada fitur berbasis kelas (nilai, jurnal, modul ajar).
- **Orang Tua / Murid** hanya melihat data anaknya dan fitur yang memang untuk mereka. Orang tua dapat mengajukan izin bila hak fitur Perizinan ON.
- Untuk pengguna lama, saat `setupAppEnvironment` dijalankan sekali, hak ON diisi setara hak lama agar tidak ada yang tiba-tiba terkunci; setelah itu Admin bebas menyesuaikan.
- **Data konfidensial tidak ikut "semua boleh melihat"**: Bimbingan Konseling, Honorarium GTK, Rekam Medis, dan Riwayat Kunjungan UKS hanya terlihat oleh peran yang memang berhak atau yang diberi hak ON oleh Admin. Daftarnya ada pada konstanta `SENSITIF` di Kode.gs (kosongkan array bila ingin dibuka untuk semua staf).

### Akun demo (hanya melihat)
Dibuat otomatis saat `setupAppEnvironment` dijalankan: username **demo**, password **demo1234**, peran **Demo**.
- Dapat membuka dan melihat hampir semua fitur, termasuk game dan alat pembelajaran.
- **Tidak dapat** menambah/mengubah/menghapus data, impor, unggah berkas, mengunduh Word/PDF lewat server, scan QR, presensi/daftar wajah, mengubah profil/password, serta membuka Pengguna, Backup, dan Arsip. Hal ini dipaksa di server, bukan hanya disembunyikan di tampilan.
- **Data pribadi disamarkan** (nama siswa menjadi mis. "An•••", NISN/NIP tersisa 3 digit terakhir, telepon/email/alamat/tanggal lahir tersembunyi, foto dan kode QR disembunyikan) agar data asli siswa tidak terbuka bagi siapa pun yang tahu password demo. Untuk menampilkan data asli, ubah `DEMO_MASK=true` menjadi `false` di Kode.gs. Menu Bimbingan Konseling, Honorarium, Rekam Medis, Kunjungan UKS, dan Kartu QR tidak muncul pada akun demo.
- **Saran:** password demo tertulis di panduan ini. Bila aplikasi berisi data siswa sungguhan, nonaktifkan akun demo (menu Pengguna, Aktif = Tidak) saat tidak diperlukan, atau ganti passwordnya.

## D2. FITUR BARU v4.1
**Keuangan**
- **Infaq Siswa — Pendapatan** (tanggal, kelas, jumlah, jenis infaq, penyetor, bukti) dan **Infaq Siswa — Pengeluaran** (uraian, jumlah, peruntukan, penerima, no. bukti), plus **Laporan Infaq** (saldo, rekap per bulan/kelas/jenis/peruntukan). Infaq dibukukan terpisah dan **tidak masuk Neraca Keuangan**. Wali kelas hanya melihat/menginput infaq kelasnya.
- **Dana BOS**: *Saldo Awal & Penyaluran* (saldo awal, penyaluran Tahap 1 dan Tahap 2, no. SP2D/dokumen, rekening), *Pengambilan Bertahap* (diambil dari dana apa, pengambilan ke-, jumlah, diambil oleh, no. cek/bukti), *Pengeluaran* (per komponen pembiayaan, sumber dana, no. bukti), dan **Rekap Dana BOS** per tahun anggaran (dana diterima, sudah diambil, belum diambil, kas tangan, belanja, sisa anggaran, persentase serapan). Pengambilan dibatasi agar tidak melebihi dana tahap terkait. Dana BOS **tidak ikut Neraca Keuangan**; jangan mengisi ulang BOS di menu Pendapatan Sekolah agar tidak ganda. Daftar komponen pembiayaan ada pada konstanta `KOMP_BOS` di Kode.gs; sesuaikan bila juknis terbaru berbeda.

**Sarana & Prasarana**
- **Kondisi Barang**: pemeriksaan per barang (jumlah baik / rusak ringan / rusak berat, pemeriksa, tindak lanjut) dengan ringkasan kondisi.
- **Barang Hibah & Berita Acara**: catat hibah (pemberi, daftar barang satu per baris: `Nama | Jumlah | Satuan | Kondisi | Harga satuan`, penerima, saksi, lokasi, peruntukan). Nomor BAST otomatis (`BAST/HIBAH/001/2026`). Tombol pada baris membuka **Berita Acara Serah Terima Barang Hibah** yang dapat dicetak atau diunduh Word. Tombol **Masukkan ke Inventaris** memindahkan barang hibah ke Inventaris Barang (sumber: Hibah), hanya sekali.

## D3. REVISI v4.2
**Kehadiran Siswa**
- Daftar siswa kini tampil walaupun penulisan kelas di Data Siswa berbeda dengan kelas pada akun guru (mis. `4-A`, `4 A`, `4–A`). Status siswa hanya menyaring yang benar-benar keluar (Mutasi/Lulus/Keluar); status kosong atau ditulis `aktif` tetap dianggap aktif.
- Bila suatu kelas memang belum punya siswa aktif, halaman menampilkan penjelasan dan daftar kelas yang ada di Data Siswa agar mudah dicek.
- Presensi mandiri **Guru PAI** dan **Guru PJOK**: tab sesi muncul otomatis dan daftar siswa tampil; guru PAI/PJOK langsung membuka sesinya dan dapat menyimpan. Wali kelas dapat melihat hasilnya (lihat saja).
- Pengguna yang **belum pernah diatur** hak aksesnya otomatis memakai templat peran (mis. Guru PAI boleh presensi PAI). Bila Admin mematikan semua hak, tersimpan sebagai "semua OFF".

**Perpindahan menu tanpa jeda**: data semua menu dimuat di latar belakang setelah login dan disimpan di peramban, sehingga membuka menu menampilkan data seketika. Animasi muat hanya muncul bila data belum siap lebih dari 0,18 detik.

**Jadwal Pelajaran**: setiap **wali kelas mengisi jadwal kelasnya sendiri** (kolom Kelas otomatis terkunci ke kelasnya; tidak dapat mengubah/menghapus jadwal kelas lain, tetapi dapat melihat semuanya). Admin dapat mematikannya per guru lewat Hak Akses.

**Laporan bulanan dengan kop surat dan tanda tangan** (Word atau PDF lewat Cetak):
- *Laporan Kehadiran* (tombol **Laporan Bulanan** di menu Kehadiran Siswa dan Laporan Kehadiran): pilih bulan, kelas, sesi. Isi: kop surat, rekap harian per siswa (H/S/I/A), jumlah, % hadir, persentase hadir/sakit/izin/alpa, tanda tangan **Wali Kelas** (sesi PAI/PJOK: guru PAI/PJOK) dan **Mengetahui Kepala Sekolah**.
- *Laporan Jurnal Mengajar* (tombol di menu Jurnal Mengajar): setiap guru mengunduh jurnalnya sendiri; Admin/Kepala Sekolah dapat memilih guru. Ditandatangani guru (atau wali kelas) dan Kepala Sekolah.
- Nama wali kelas diambil dari Data Kelas (kolom Wali Kelas); bila kosong, dari akun Guru Kelas untuk kelas itu. NIP diambil dari Data Guru (cocokkan nama). Isi **NIP Kepala Sekolah** dan **kota penandatanganan** di menu Visi & Misi (tombol Ubah).

**Visi & Misi**: ditambah **NSS** (Nomor Statistik Sekolah) dan NPSN di tampilan dan formulir, serta nama/NIP Kepala Sekolah dan kota. NPSN dan NSS ikut tercetak pada kop surat semua laporan.

## E. CATATAN PENTING
1. **Setelah mengganti Kode.gs wajib** menjalankan ulang `setupAppEnvironment` dan Deploy New version. Jika muncul pesan "Sheet ... belum ada", itu tandanya langkah ini terlewat.
2. **Hapus Data** selalu membuat salinan backup otomatis dulu (folder `Backup` di Drive). Untuk memulihkan, buka salinan dan salin sheet yang dibutuhkan.
3. **Generator Modul Ajar** menyusun draf berbasis templat (bukan AI). Guru perlu membaca dan menyesuaikannya.
4. Game, papan tulis, mind map, dan alat bantu lain berjalan di peramban. Alat Peraga 3D dan Peta Interaktif memerlukan internet (memuat pustaka three.js dan Leaflet/OpenStreetMap).
5. Data kesehatan, keuangan, dan bimbingan konseling bersifat sensitif: batasi akun Admin, dan gunakan password kuat.
6. Rantai Kata menerima kata apa pun yang diketik pemain (tidak ada pemeriksaan kamus lengkap); guru berperan sebagai juri.
7. Batas aman Google Sheets: bila data sangat besar (puluhan ribu baris per sheet), pertimbangkan arsip per tahun ajaran memakai Backup + Hapus Data.

## F. MASALAH UMUM
| Gejala | Solusi |
|---|---|
| "GAS_URL belum diisi" | Isi `js/config.js`, commit, push |
| "Sheet ... belum ada" | Jalankan ulang `setupAppEnvironment`, lalu Deploy New version |
| Menu baru tidak muncul | Deploy **New version**, lalu Ctrl+Shift+R |
| Perubahan frontend tidak terlihat | Ctrl+Shift+R (atau tunggu 1-2 menit setelah push) |
| Kamera ditolak | Ikon gembok di address bar -> Izinkan kamera -> muat ulang |
| 404 di GitHub Pages | `index.html` harus di root repo; push dari folder `sdn047-tarakan` |

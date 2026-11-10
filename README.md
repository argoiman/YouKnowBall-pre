# YouKnowBall

**Game Simulasi Biliar 2D Berbasis C++ dan SFML**

![Status](https://img.shields.io/badge/status-in%20development-blue)
![Language](https://img.shields.io/badge/language-C%2B%2B-00599C)
![Library](https://img.shields.io/badge/SFML-2.4.2-8CC445)
![Platform](https://img.shields.io/badge/platform-desktop-lightgrey)

YouKnowBall adalah game simulasi biliar 2D dengan perspektif top-down yang dikembangkan sebagai proyek mata kuliah **Desain dan Pemrograman Berorientasi Objek (DPBO)**. Game menyediakan mode **8-Ball** dan **9-Ball**, dengan pilihan dua pemain lokal pada satu perangkat atau satu pemain melawan **Bot Easy**.

Dokumen ini merupakan **README acuan proyek**: ruang lingkup produk, keputusan permainan, kontrol, arsitektur, kontrak method, struct, alur interaksi, rencana pengembangan, dan pengujian disatukan di satu tempat. Dokumen ini menggantikan rangkuman-rangkuman rancangan sebelumnya sebagai acuan kerja terpadu; revisi berikutnya harus memperbarui bagian terkait, bukan menambahkan keputusan yang bertentangan di bagian terpisah.

> **Status dokumen:** baseline pengembangan yang telah diselaraskan dengan keputusan proyek sampai 11 November 2026. Detail teknis yang memang belum diputuskan ditandai secara eksplisit sebagai *belum dikunci* dan tidak boleh dianggap sebagai keputusan final.

---

## Daftar Isi

- [1. Identitas Proyek](#1-identitas-proyek)
- [2. Tujuan dan Prinsip Desain](#2-tujuan-dan-prinsip-desain)
- [3. Ruang Lingkup](#3-ruang-lingkup)
- [4. Teknologi dan Lingkungan](#4-teknologi-dan-lingkungan)
- [5. Fitur dan Halaman Aplikasi](#5-fitur-dan-halaman-aplikasi)
- [6. Kontrol Permainan](#6-kontrol-permainan)
- [7. Aturan dan Mekanisme Permainan](#7-aturan-dan-mekanisme-permainan)
- [8. Fisika dan Prediksi Lintasan](#8-fisika-dan-prediksi-lintasan)
- [9. Penyimpanan Data](#9-penyimpanan-data)
- [10. Use Case Scenario](#10-use-case-scenario)
- [11. Responsibility-Driven Design](#11-responsibility-driven-design)
- [12. Arsitektur: 14 Class Utama](#12-arsitektur-14-class-utama)
- [13. Kontrak Method Setiap Class](#13-kontrak-method-setiap-class)
- [14. Delapan Struct Pendukung](#14-delapan-struct-pendukung)
- [15. Enumerasi](#15-enumerasi)
- [16. Relasi Antarobjek](#16-relasi-antarobjek)
- [17. Alur Kolaborasi Satu Pukulan](#17-alur-kolaborasi-satu-pukulan)
- [18. State dan Kontrak Siklus Pertandingan](#18-state-dan-kontrak-siklus-pertandingan)
- [19. WBS, Jadwal, dan Penanggung Jawab](#19-wbs-jadwal-dan-penanggung-jawab)
- [20. Kriteria Keberhasilan dan Pengujian](#20-kriteria-keberhasilan-dan-pengujian)
- [21. Risiko dan Penanganan](#21-risiko-dan-penanganan)
- [22. Hal yang Belum Dikunci](#22-hal-yang-belum-dikunci)
- [23. Referensi](#23-referensi)

---

## 1. Identitas Proyek

| Informasi | Keterangan |
|---|---|
| Nama produk | **YouKnowBall** |
| Nama proyek akademik | SimulasiBilliard |
| Kelompok | 9 |
| Mata kuliah | Desain dan Pemrograman Berorientasi Objek (DPBO) |
| Program studi | S1 Ilmu Komputer |
| Institusi | Universitas Negeri Jakarta |
| Anggota | Rapid Akbar Sinatria, Muhammad Argo Iman, Satya Firma Ashari |
| Platform | PC/Desktop |
| Jenis aplikasi | Game biliar 2D top-down |
| Bahasa | C++ |
| Library utama | SFML 2.4.2 |
| Batas penyelesaian proyek dan laporan akhir | **13 Desember 2026** |

---

## 2. Tujuan dan Prinsip Desain

### 2.1 Tujuan

1. Menerapkan konsep OOP: enkapsulasi, abstraksi, pewarisan, dan polimorfisme.
2. Menggunakan Responsibility-Driven Design (RDD) untuk menentukan tanggung jawab setiap objek.
3. Menghasilkan simulasi biliar yang dapat dimainkan dari menu awal hingga hasil pertandingan.
4. Memisahkan perhitungan fisika dari evaluasi aturan agar perubahan pada satu bagian tidak merusak bagian lain.
5. Menyediakan struktur kode yang cukup jelas untuk dikembangkan, diuji, dan dipresentasikan.

### 2.2 Prinsip desain

- Satu class memiliki tanggung jawab utama yang jelas.
- Data dan perilaku ditempatkan pada objek yang paling mengetahui atau paling tepat melakukannya.
- `PhysicsEngine` mencatat fakta fisik; `GameRules` menilai akibatnya menurut aturan.
- `Player` menyimpan identitas dan statistik; controller menentukan tindakan pemain.
- Pemain manusia dan Bot menghasilkan `ShotCommand` dan memakai jalur simulasi pertandingan yang sama.
- Tidak menambah class utama atau struct di luar baseline 14 class dan 8 struct tanpa alasan arsitektural yang kuat serta persetujuan tim.
- Halaman aplikasi dikelola melalui `ScreenManager`; tidak dibuat satu class untuk setiap halaman.
- Method baru hanya ditambahkan jika kebutuhan nyata tidak dapat dipenuhi oleh kontrak yang telah ditetapkan. Penambahan harus dicatat beserta alasan, tanggung jawab, dan dampaknya pada collaborator.

---

## 3. Ruang Lingkup

### 3.1 Fitur yang termasuk

- Mode permainan 8-Ball dan 9-Ball.
- Dua pemain lokal pada satu perangkat.
- Satu pemain melawan Bot Easy.
- Pengisian nama pemain.
- Pilihan timer: tanpa batas, 15 detik, 30 detik, atau 60 detik.
- Kontrol arah dan kekuatan pukulan yang terpisah.
- Meja, bola putih, bola objek, cue stick, bantalan, dan enam pocket.
- Gerak bola, gesekan/perlambatan, tumbukan antarb bola, pantulan bantalan, dan deteksi pocket.
- Prediksi lintasan bola putih menuju titik tumbukan pertama serta perkiraan arah bola sasaran setelah tumbukan pertama.
- Pergantian giliran, break, foul, scratch, ball-in-hand, dan kondisi kemenangan.
- Pause, lanjutkan, pengaturan dari Pause, mulai ulang, dan kembali ke menu utama.
- Halaman hasil, rematch, riwayat pertandingan, pengaturan aplikasi, cara bermain, dan keluar aplikasi.
- Penyimpanan pengaturan dan hasil pertandingan selesai secara lokal menggunakan file TXT.
- Pengaturan tampilan: mode **Fullscreen** atau **Windowed**. Mode Windowed mempertahankan rasio aspek tetap agar jendela tidak gepeng; ukuran jendela boleh diubah selama rasio aspek tetap terjaga.

### 3.2 Tidak termasuk ruang lingkup

- Multiplayer online atau jaringan.
- Akun pengguna, login, server, dan database eksternal.
- Replay pertandingan.
- Spin dan jump shot.
- Simulasi bola keluar meja.
- Bot Normal atau Hard.
- Pocket Challenge.
- Melanjutkan pertandingan yang belum selesai setelah aplikasi ditutup.

### 3.3 Prinsip batasan

Daftar di atas menetapkan fitur produk, bukan membatasi kualitas pengerjaan. Fitur yang sudah menjadi bagian ruang lingkup tidak diturunkan ke kategori tambahan hanya karena dianggap sulit. Jika waktu masih tersedia setelah kriteria kelayakan utama terpenuhi, tim melakukan penyempurnaan kualitas, kestabilan, dan pengalaman bermain.

---

## 4. Teknologi dan Lingkungan

| Teknologi | Penggunaan |
|---|---|
| C++ | Bahasa utama untuk model objek, aturan, fisika, dan alur aplikasi. |
| SFML **2.4.2** | Window, grafis 2D, input, audio, dan pengukuran waktu. |
| Figma | Wireframe dan rancangan antarmuka. |
| Git dan GitHub | Version control, kolaborasi, dan penyimpanan repository. |
| TXT | Penyimpanan lokal pengaturan dan riwayat pertandingan. |

**Catatan kompatibilitas:** gunakan SFML 2.4.2 sesuai keputusan proyek. Konfigurasi compiler, linker, dan sistem operasi harus diverifikasi bersama sebelum implementasi terintegrasi.

---

## 5. Fitur dan Halaman Aplikasi

### 5.1 Main Menu

Menampilkan akses ke:
- Mulai Pertandingan.
- Riwayat Pertandingan.
- Pengaturan Aplikasi.
- Cara Bermain.
- Keluar.

### 5.2 Match Setup

Pemain memilih:
- Jenis permainan: 8-Ball atau 9-Ball.
- Jenis lawan: pemain lokal atau Bot Easy.
- Nama pemain.
- Batas waktu setiap kesempatan: tanpa batas, 15, 30, atau 60 detik.

Setelah konfigurasi dikonfirmasi, sistem menginisialisasi pertandingan, menentukan pemain pembuka, menyiapkan rack, dan membuka halaman permainan.

### 5.3 Game Screen

Menampilkan:
- Meja dan bola.
- Cue stick pada area meja untuk mengatur arah.
- Indikator power terpisah untuk menentukan kekuatan.
- Informasi pemain dan pemain yang sedang mendapat giliran.
- Timer jika timer diaktifkan.
- Status permainan dan informasi foul/ball-in-hand jika berlaku.
- Prediksi lintasan.
- Akses Pause.

### 5.4 Pause Menu

Pilihan yang tersedia:
1. **Lanjutkan** — kembali ke pertandingan dengan state dan sisa waktu sebelumnya.
2. **Pengaturan** — membuka pengaturan aplikasi; tombol kembali mengembalikan pemain ke Pause.
3. **Mulai Ulang** — meminta konfirmasi, lalu menginisialisasi ulang pertandingan. Hasil pertandingan yang dibatalkan tidak disimpan.
4. **Menu Utama** — meminta konfirmasi sebelum meninggalkan pertandingan aktif. Hasil yang belum selesai tidak disimpan.

### 5.5 Result Screen

Menampilkan setidaknya:
- Nama pemain.
- Nama pemenang.
- Mode 8-Ball/9-Ball.
- Jumlah bola yang berhasil dimasukkan per pemain.
- Jumlah foul per pemain.
- Jumlah pukulan per pemain.
- Durasi aktif pertandingan.

Pilihan:
- **Rematch** — memulai pertandingan baru dengan konfigurasi sebelumnya; pemain pembuka ditentukan ulang.
- **Menu Utama** — kembali ke halaman utama.

Perubahan konfigurasi mode, lawan, nama, atau timer dilakukan dari Match Setup melalui Main Menu, bukan dari Rematch.

### 5.6 History Screen

Menampilkan daftar pertandingan yang selesai dan memungkinkan pemain membuka detail catatan. Pertandingan yang dibatalkan melalui restart atau kembali ke menu sebelum selesai tidak dimasukkan ke riwayat.

### 5.7 Settings Screen

Pengaturan yang disediakan:
- **Display:** Fullscreen atau Windowed.
- **Audio:** volume musik dan volume efek suara (SFX).
- **Controls:** sensitivitas kontrol mouse.

Tombol tindakan:
- **Terapkan/Simpan** untuk menerapkan dan menyimpan perubahan.
- **Kembali** untuk kembali ke halaman sebelumnya. Jika pengaturan dibuka dari Pause, halaman sebelumnya adalah Pause.

Pengaturan disimpan secara lokal dan dimuat kembali ketika aplikasi dijalankan.

### 5.8 How to Play

Memuat panduan:
- Kontrol arah dan power.
- Aturan dasar 8-Ball dan 9-Ball.
- Break.
- Foul dan scratch.
- Ball-in-hand.
- Cara menggunakan Pause dan Rematch.

---

## 6. Kontrol Permainan

Kontrol pukulan menggunakan dua bagian yang berbeda. Keduanya tidak boleh disatukan sebagai satu mekanisme drag yang sama.

### 6.1 Mengatur arah

Pemain klik dan tahan cue stick yang berada pada area meja, kemudian menggerakkannya untuk menentukan arah pukulan. Cue stick di meja berfungsi sebagai **pengarah bidikan**.

### 6.2 Mengatur kekuatan

Setelah arah ditetapkan, pemain menggunakan **indikator power yang terpisah dari area kontrol arah**. Indikator dapat memiliki bentuk visual cue stick atau bentuk lain yang ditentukan ketika implementasi UI dilakukan. Posisi dan bentuk final indikator belum ditetapkan dalam dokumen ini.

Indikator tersebut hanya menentukan **kekuatan pukulan**, bukan arah pukulan. Pemain menarik indikator untuk menentukan power, lalu melepaskannya untuk mengeksekusi tembakan.

### 6.3 Membatalkan pengaturan power

- Saat pemain sedang menarik indikator power, tombol **Space** membatalkan proses pengaturan power.
- Setelah pembatalan, pemain dapat mengarahkan cue kembali.
- Pembatalan sebelum pelepasan indikator tidak menghasilkan pukulan dan tidak membuat snapshot pukulan baru.
- Tombol Space yang dimaksud berlaku pada tahap pengaturan power, bukan sebagai pengganti kontrol arah.

### 6.4 Timeout ketika sedang mengatur power

Jika waktu habis ketika pemain sedang menarik indikator power, sistem langsung melepaskan/mengeksekusi pukulan menggunakan kekuatan yang telah tercapai saat itu. Tidak ada tambahan waktu untuk menyelesaikan tarikan.

### 6.5 Timeout ketika tidak sedang menarik power

Jika waktu habis ketika pemain tidak sedang menarik indikator power, kesempatan pemain berakhir dan giliran langsung berpindah kepada lawan. Kondisi ini **bukan foul**.

---

## 7. Aturan dan Mekanisme Permainan

Aturan permainan mengadaptasi aturan 8-Ball dan 9-Ball dari World Pool-Billiard Association (WPA), dengan penyederhanaan yang ditetapkan untuk kebutuhan proyek. Jika ada perbedaan antara aturan resmi dan penyederhanaan proyek, implementasi mengikuti keputusan proyek yang ditulis pada bagian ini.

### 7.1 Aturan umum

- Satu pertandingan terdiri dari satu rack.
- Sistem menentukan pemain pembuka ketika pertandingan baru dimulai.
- Pukulan biasa dinilai setelah seluruh bola berhenti.
- Foul biasa memberikan hak ball-in-hand kepada lawan.
- Ball-in-hand memungkinkan cue ball ditempatkan bebas pada area meja yang valid.
- Pukulan sah yang tidak memenuhi syarat mempertahankan giliran akan mengalihkan giliran kepada lawan.
- Timer berlaku pada kesempatan pemain sesuai konfigurasi pertandingan.
- Timer tanpa batas tidak menjalankan hitung mundur.

### 7.2 Break

Aturan break proyek menggunakan ketentuan sederhana dan konsisten:
- Pukulan break harus mengenai bola target legal.
- Break dinilai sah jika terdapat bola yang masuk pocket atau sekurang-kurangnya empat bola bernomor menyentuh bantalan.
- Break tidak sah memberikan lawan ball-in-hand.
- Susunan bola setelah break tidak otomatis di-rack ulang.
- Bola 8 yang masuk saat break dikembalikan ke titik penempatan yang sah; masuknya bola 8 saat break tidak langsung menentukan kemenangan.
- Pada 9-Ball, bola 9 yang masuk secara sah saat break menghasilkan kemenangan sesuai aturan mode.

### 7.3 Mode 8-Ball

- Kelompok bola terdiri dari Solid (1–7) dan Stripe (9–15).
- Meja tetap terbuka setelah break sampai kelompok ditentukan melalui bola kelompok yang pertama kali masuk secara sah setelah break.
- Setelah kelompok ditetapkan, pemain harus mengenai kelompoknya terlebih dahulu.
- Pemain harus menyelesaikan seluruh bola dalam kelompoknya sebelum memasukkan bola 8.
- Bola 8 harus dimasukkan ke pocket yang telah dipilih.
- Bola 8 masuk sebelum waktunya, ke pocket yang tidak dipilih, atau bersamaan dengan foul mengakibatkan kekalahan.
- Jika foul terjadi, lawan memperoleh ball-in-hand.

**Dua kelompok masuk pada satu pukulan:** keputusan proyek adalah kelompok ditentukan oleh bola kelompok yang pertama kali tercatat masuk secara sah. Jika kejadian benar-benar bersamaan pada resolusi simulasi, implementasi harus memakai aturan tie-break yang deterministik dan konsisten; jangan memilih kelompok secara acak. Detail tie-break teknis perlu dicatat pada pengujian integrasi.

### 7.4 Mode 9-Ball

- Bola bernomor terendah yang masih berada di meja harus menjadi kontak pertama.
- Bola dapat dimasukkan secara berurutan maupun melalui kombinasi, selama kontak pertama tetap mengenai bola bernomor terendah.
- Memasukkan bola 9 secara sah menghasilkan kemenangan.
- Jika bola 9 masuk bersamaan dengan foul, bola 9 dikembalikan ke titik penempatan yang sah dan permainan berlanjut sesuai konsekuensi foul.
- Foul memberikan lawan ball-in-hand.
- Tidak menerapkan push-out atau kekalahan karena tiga foul berturut-turut pada baseline proyek.

### 7.5 Foul dan scratch

Jenis foul dasar:
- Tidak mengenai bola target legal terlebih dahulu.
- Tidak terjadi kontak bola ketika pukulan dilakukan.
- Tidak ada bola yang masuk dan tidak ada bola yang menyentuh bantalan setelah kontak pertama.
- Cue ball masuk pocket (*scratch*).
- Pelanggaran khusus terhadap bola penentu sesuai mode.

Timeout saat pemain tidak sedang menarik power bukan foul; giliran langsung berpindah. Timeout saat indikator power sedang ditarik mengeksekusi pukulan pada power yang telah tercapai, kemudian hasilnya dinilai melalui aturan normal.

### 7.6 Ball-in-hand

- Diberikan kepada lawan ketika terjadi foul.
- Cue ball dapat ditempatkan bebas pada area meja yang valid.
- Posisi tidak boleh berada di luar area permainan, di dalam pocket, atau bertumpuk/overlap dengan bola lain.
- Timer kesempatan tetap berjalan selama proses penempatan dan menunggu pukulan berikutnya.
- Jika timer habis sebelum penempatan selesai, hak kesempatan berpindah sesuai kebijakan timeout; hal ini harus ditangani konsisten pada implementasi.

### 7.7 Pergantian giliran

Setelah semua bola berhenti:
1. `GameRules` mengevaluasi `ShotStartState` dan `ShotResult`.
2. Jika foul, lawan mendapat ball-in-hand.
3. Jika tidak foul dan syarat mempertahankan giliran terpenuhi, pemain yang sama melanjutkan.
4. Selain kondisi tersebut, giliran berpindah kepada lawan.
5. Jika kondisi menang terpenuhi, pertandingan diakhiri dan hasil disimpan.

---

## 8. Fisika dan Prediksi Lintasan

### 8.1 Fisika dasar

Simulasi mencakup:
- Pergerakan bola berdasarkan kecepatan.
- Perlambatan akibat gesekan.
- Tumbukan antarb bola.
- Pantulan pada bantalan meja.
- Deteksi bola yang masuk pocket.
- Deteksi seluruh bola telah berhenti.

Parameter numerik seperti koefisien gesekan, restitution, stop threshold, ukuran bola, dan substep simulasi ditentukan melalui tuning dan pengujian. Nilai tersebut tidak ditetapkan secara spekulatif dalam README.

### 8.2 Prediksi lintasan

Prediksi merupakan bagian dari pengalaman bidik dan termasuk target kualitas inti:
- Menampilkan arah/lintasan cue ball menuju titik tumbukan pertama.
- Menampilkan perkiraan arah gerak bola sasaran setelah tumbukan pertama.
- Prediksi harus mengikuti arah bidikan yang sedang dipilih.
- Prediksi merupakan estimasi visual, bukan jaminan hasil akhir simulasi; pantulan lanjutan dan tumbukan berantai dapat membuat lintasan aktual berbeda.

---

## 9. Penyimpanan Data

Penyimpanan lokal menggunakan file TXT dan dikelola oleh `StorageManager`.

### 9.1 Pengaturan aplikasi

Menyimpan:
- Mode tampilan (Fullscreen/Windowed).
- Lebar/tinggi jendela atau ukuran window yang dipilih, dengan rasio aspek tetap untuk Windowed.
- Volume musik.
- Volume SFX.
- Sensitivitas kontrol mouse.

### 9.2 Riwayat pertandingan

Menyimpan setidaknya:
- Waktu/tanggal pertandingan.
- Jenis permainan.
- Jenis lawan.
- Nama pemain.
- Pemenang dan alasan kemenangan.
- Jumlah bola masuk per pemain.
- Jumlah foul per pemain.
- Jumlah pukulan per pemain.
- Durasi aktif pertandingan.
- Konfigurasi timer.

### 9.3 Aturan penyimpanan

- Hanya pertandingan yang selesai secara normal yang masuk riwayat.
- Restart atau keluar dari pertandingan aktif tidak membuat catatan hasil.
- Satu pertandingan hanya boleh dicatat satu kali.
- Penanda `isResultSaved` baru berubah setelah penyimpanan berhasil.
- Format, delimiter, dan strategi pemulihan file rusak ditentukan saat implementasi penyimpanan dan harus diuji.

---

## 10. Use Case Scenario

### 10.1 Identitas use case

| Elemen | Deskripsi |
|---|---|
| Nama | Menggunakan YouKnowBall dan memainkan pertandingan hingga selesai |
| Goal | Pemain dapat mengatur dan memainkan 8-Ball/9-Ball, melihat hasil dan riwayat, mengubah pengaturan, membaca panduan, serta mengakhiri aplikasi. |
| Level | User-Goal |
| Primary Actor | Pemain |
| Supporting Actor | Tidak ada |
| Precondition | Aplikasi telah terpasang dan dapat dijalankan. |
| Trigger | Pemain menjalankan YouKnowBall. |

### 10.2 Skenario narasi

Pemain menjalankan YouKnowBall dan sistem menampilkan halaman utama yang menyediakan pilihan untuk memulai pertandingan, melihat riwayat, membuka pengaturan aplikasi, membaca cara bermain, dan keluar dari aplikasi. Untuk memulai pertandingan, pemain memilih 8-Ball atau 9-Ball. Sistem menampilkan halaman pengaturan pertandingan agar pemain dapat memilih lawan, yaitu pemain lokal atau Bot Easy, memasukkan nama pemain, serta menentukan batas waktu setiap kesempatan berupa tanpa batas, 15, 30, atau 60 detik.

Setelah pemain menekan Mulai Pertandingan, sistem menyiapkan meja, bola, pemain, dan giliran awal sesuai konfigurasi. Sistem menampilkan halaman permainan yang memuat informasi pemain, giliran, timer, cue stick, indikator power terpisah, dan prediksi lintasan. Pemain mengatur arah menggunakan cue stick pada meja, lalu menentukan kekuatan melalui indikator power yang terpisah. Pemain dapat menekan Space ketika sedang menarik indikator power untuk membatalkan pengaturan kekuatan dan mengarahkan cue kembali. Jika lawan yang dipilih adalah Bot Easy, sistem menentukan dan melakukan pukulan secara otomatis ketika giliran Bot tiba.

Setelah pukulan dilakukan, sistem menghitung gerak bola, gesekan, tumbukan, pantulan bantalan, dan bola yang masuk pocket. Setelah seluruh bola berhenti, sistem menilai hasil pukulan berdasarkan mode permainan untuk menentukan foul, scratch, pergantian atau kelanjutan giliran, ball-in-hand, dan kondisi kemenangan. Jika waktu habis ketika pemain sedang menarik indikator power, sistem langsung mengeksekusi pukulan dengan kekuatan yang telah tercapai tanpa tambahan waktu. Jika waktu habis ketika pemain tidak sedang menarik indikator power, giliran langsung berpindah dan kondisi tersebut bukan foul.

Selama pertandingan, pemain dapat menekan Esc untuk membuka Pause. Pemain dapat melanjutkan pertandingan, membuka pengaturan aplikasi, memulai ulang pertandingan, atau kembali ke menu utama setelah konfirmasi. Ketika pengaturan dibuka dari Pause, tombol Kembali mengembalikan pemain ke Pause. Pertandingan yang dimulai ulang atau ditinggalkan sebelum selesai tidak disimpan ke riwayat.

Pertandingan berlangsung sampai salah satu pemain menang sesuai aturan 8-Ball atau 9-Ball. Sistem menampilkan hasil yang memuat nama pemain, pemenang, jenis permainan, jumlah bola masuk, jumlah foul, jumlah pukulan, dan durasi aktif. Hasil pertandingan selesai disimpan ke riwayat. Pemain dapat memilih Rematch untuk memainkan pertandingan baru dengan konfigurasi sebelumnya dan pemain pembuka yang ditentukan ulang, atau memilih Menu Utama.

Dari halaman utama, pemain dapat melihat daftar dan detail riwayat pertandingan, mengubah pengaturan display, volume musik, volume SFX, dan sensitivitas mouse, serta membaca panduan kontrol dan aturan. Perubahan pengaturan diterapkan dan disimpan melalui tombol Terapkan/Simpan. Untuk mengakhiri penggunaan aplikasi, pemain memilih Keluar dan mengonfirmasi tindakan tersebut.

### 10.3 Skenario step-by-step

**Main Flow**

1. Pemain menjalankan YouKnowBall.
2. Sistem menampilkan halaman utama.
3. Pemain memilih Mulai Pertandingan.
4. Sistem menampilkan pilihan 8-Ball dan 9-Ball.
5. Pemain memilih mode permainan.
6. Sistem menampilkan pengaturan pertandingan.
7. Pemain memilih pemain lokal atau Bot Easy.
8. Pemain memasukkan nama pemain.
9. Pemain memilih timer tanpa batas, 15, 30, atau 60 detik.
10. Pemain menekan Mulai Pertandingan.
11. Sistem menyiapkan rack, pemain, giliran awal, dan konfigurasi pertandingan.
12. Sistem menampilkan meja, informasi pemain, timer, cue stick, indikator power, dan prediksi lintasan.
13. Pemain mengatur arah menggunakan cue stick pada meja.
14. Pemain menarik indikator power terpisah untuk menentukan kekuatan.
15. Pemain melepaskan indikator untuk melakukan pukulan.
16. Sistem menjalankan simulasi gerak, gesekan, tumbukan, pantulan, dan deteksi pocket.
17. Setelah seluruh bola berhenti, sistem mengevaluasi hasil pukulan sesuai aturan.
18. Sistem memperbarui statistik, status foul/scratch, ball-in-hand, dan giliran.
19. Jika belum ada pemenang, sistem melanjutkan ke kesempatan berikutnya; jika giliran Bot, Bot menentukan dan mengirim pukulan melalui jalur yang sama.
20. Pemain dapat menekan Esc untuk membuka Pause.
21. Pemain dapat memilih Lanjutkan, Pengaturan, Mulai Ulang, atau Menu Utama.
22. Sistem mengulangi siklus pukulan sampai kondisi kemenangan terpenuhi.
23. Sistem menampilkan hasil pertandingan dan menyimpan catatan ke riwayat.
24. Pemain memilih Rematch atau Menu Utama.
25. Dari Main Menu, pemain dapat membuka Riwayat, Pengaturan, atau Cara Bermain.
26. Pemain memilih Keluar.
27. Sistem meminta konfirmasi dan menutup aplikasi jika disetujui.

**Alternative Flow**

| Kode | Kondisi | Respons sistem |
|---|---|---|
| A1 | Pemain memilih lokal | Sistem menyiapkan dua controller manusia. |
| A2 | Pemain memilih Bot Easy | Sistem menyiapkan satu controller manusia dan satu BotController. |
| A3 | Pemain menekan Space saat menarik power | Pengaturan power dibatalkan; tidak ada pukulan; pemain dapat mengarahkan cue kembali. |
| A4 | Timer habis saat indikator power sedang ditarik | Sistem langsung mengeksekusi pukulan dengan power saat itu, tanpa tambahan waktu. |
| A5 | Timer habis saat pemain tidak menarik power | Kesempatan berakhir dan giliran langsung berpindah; bukan foul. |
| A6 | Pukulan menghasilkan foul | Lawan memperoleh ball-in-hand sesuai aturan mode. |
| A7 | Pemain memilih Lanjutkan dari Pause | Sistem memulihkan state dan sisa waktu; tidak membuat rack, snapshot, atau impuls baru. |
| A8 | Pemain memilih Pengaturan dari Pause | Sistem membuka Settings; tombol Kembali mengembalikan ke Pause. |
| A9 | Pemain memilih Mulai Ulang | Sistem meminta konfirmasi; jika disetujui, pertandingan diinisialisasi ulang tanpa menyimpan hasil yang dibatalkan. |
| A10 | Pemain memilih Menu Utama dari pertandingan aktif | Sistem meminta konfirmasi; jika disetujui, sesi dibatalkan tanpa catatan riwayat. |
| A11 | Pemain memilih Rematch | Sistem memulai pertandingan baru dengan konfigurasi sebelumnya dan mengundi pemain pembuka kembali. |
| A12 | Pemain memilih Terapkan/Simpan | Sistem menerapkan pengaturan dan menyimpannya secara lokal. |
| A13 | Pemain membatalkan konfirmasi Keluar | Sistem kembali ke halaman sebelumnya. |

### 10.4 Postcondition

- Pertandingan selesai: hasil ditampilkan dan disimpan satu kali ke riwayat.
- Pertandingan dibatalkan/restart: tidak disimpan sebagai pertandingan selesai.
- Pengaturan yang disimpan tersedia pada sesi aplikasi berikutnya.
- Pemain dapat kembali ke Main Menu, memulai pertandingan baru, melihat riwayat, membuka pengaturan, membaca panduan, atau menutup aplikasi.

---

## 11. Responsibility-Driven Design

RDD menentukan objek berdasarkan kebutuhan: objek mana yang mengetahui informasi (*knowing*) dan objek mana yang melakukan tindakan (*doing*). Objek yang dimintai bantuan menjadi *collaborator*.

Contoh pembagian:
- `Ball` mengetahui posisi dan kecepatan bola serta menyediakan operasi untuk memperbarui keadaan fisiknya.
- `PhysicsEngine` menghitung gerak dan tumbukan serta mencatat kejadian fisik.
- `GameRules` mengetahui aturan mode aktif dan menilai akibat pukulan.
- `MatchSession` mengetahui state, giliran, dan timer serta mengoordinasikan siklus pertandingan.
- `ScreenManager` mengetahui halaman aktif dan menangani navigasi serta tampilan.
- `StorageManager` mengetahui lokasi dan data file serta membaca/menyimpan pengaturan dan hasil.

Pemisahan ini menjaga agar aturan tidak bercampur dengan fisika, tampilan tidak mengambil alih logika pertandingan, dan penyimpanan tidak menjadi pemilik aturan permainan.

---

## 12. Arsitektur: 14 Class Utama

Jumlah class utama **tetap 14**. Tidak ada class utama tambahan dalam baseline ini.

| No. | Class | Tanggung jawab inti |
|---:|---|---|
| 1 | `GameApp` | Inisialisasi, jendela, game loop, dan shutdown aplikasi. |
| 2 | `ScreenManager` | Halaman, navigasi, event UI, dan rendering antarmuka. |
| 3 | `MatchSession` | Konfigurasi, pemain, giliran, timer, state, pukulan, pause, dan hasil pertandingan. |
| 4 | `Player` | Identitas, kelompok bola, dan statistik pemain. |
| 5 | `PlayerController` (abstract) | Kontrak umum sumber tindakan pemain. |
| 6 | `HumanController` | Mengubah input manusia menjadi perintah pukulan. |
| 7 | `BotController` | Menentukan pukulan Bot Easy. |
| 8 | `Table` | Area meja, kumpulan bola, rack, dan enam pocket. |
| 9 | `Ball` | Posisi, kecepatan, radius, dan status setiap bola. |
| 10 | `Cue` | Arah bidikan, power, impuls, dan prediksi lintasan. |
| 11 | `PhysicsEngine` | Gerak, gesekan, tumbukan, pantulan, dan deteksi pocket. |
| 12 | `GameRules` | Evaluasi aturan 8-Ball/9-Ball, foul, ball-in-hand, dan kemenangan. |
| 13 | `StorageManager` | Pengaturan dan riwayat lokal berbasis TXT. |
| 14 | `AudioManager` | Musik, efek suara, dan volume audio. |

### 12.1 Keputusan penggabungan

| Rancangan fungsi | Keputusan baseline |
|---|---|
| Game dan pengelola pertandingan | Dipisahkan menjadi `GameApp` dan `MatchSession`. |
| UIManager | Dikelola oleh `ScreenManager`. |
| GameTable dan Pocket | `Table` menyimpan enam `PocketData`; Pocket bukan class utama. |
| PhysicsSystem dan CollisionSystem | Digabung menjadi `PhysicsEngine`. |
| TurnManager dan GameTimer | Tanggung jawab siklus giliran/timer berada pada `MatchSession`. |
| EightBallRules dan NineBallRules | Ditangani `GameRules` berdasarkan `GameType`; tidak ada class turunan aturan pada baseline. |
| AIPlayer | Identitas tetap `Player`; perilaku Bot berada pada `BotController`. |
| FileStorage, SettingsManager, MatchHistory | Operasi file lokal digabung pada `StorageManager`. |
| GameResult | Direpresentasikan oleh `MatchRecord`. |
| Data proses pukulan | Ditampung oleh struct `ShotCommand`, `ShotStartState`, `ShotResult`, dan `RuleOutcome`. |

---

## 13. Kontrak Method Setiap Class

Bagian ini adalah **baseline kontrak method**, bukan hanya daftar method utama. Kontrak berikut dimaksudkan agar implementasi awal dapat dimulai tanpa menambah method secara rutin. Penambahan tetap dimungkinkan jika kebutuhan implementasi nyata tidak tertangani; setiap penambahan wajib memiliki alasan dan tidak boleh memindahkan tanggung jawab class lain.

Notasi: `+` public, `-` private, `#` protected. Parameter `const`/reference dapat disesuaikan pada deklarasi C++ final selama makna kontrak tidak berubah.

### 13.1 `GameApp`

**Atribut**
- `sf::RenderWindow window`
- `bool running`
- `sf::Clock frameClock`
- `ScreenManager screenManager`
- `StorageManager storageManager`
- `AudioManager audioManager`

**Method**
| Method | Kontrak |
|---|---|
| `bool initialize()` | Membaca pengaturan, menyiapkan window dan layanan aplikasi; mengembalikan status inisialisasi. |
| `void run()` | Menjalankan game loop selama aplikasi aktif. |
| `void processEvents()` | Mengambil event SFML dan meneruskannya ke komponen yang berwenang. |
| `void update(float deltaTime)` | Memperbarui sesi aktif, UI, dan layanan berdasarkan delta time. |
| `void render()` | Membersihkan window, meminta ScreenManager menggambar, lalu menampilkan frame. |
| `void shutdown()` | Menyimpan pengaturan terakhir bila diperlukan, menghentikan layanan, dan menutup window. |

**Tidak bertanggung jawab:** mengevaluasi foul, menghitung tumbukan, atau menentukan pemenang.

### 13.2 `ScreenManager`

**Atribut**
- `ScreenType currentScreen`
- `ScreenType previousScreen`
- `sf::Vector2i mousePosition`
- Referensi/akses ke `MatchSession`, `StorageManager`, dan `AudioManager` melalui komposisi aplikasi atau dependency yang disepakati.

**Method**
| Method | Kontrak |
|---|---|
| `void changeScreen(ScreenType type)` | Mengubah halaman aktif dan mencatat halaman asal untuk navigasi kembali. |
| `void handleEvent(const sf::Event& event)` | Menangani input UI dan meneruskan input gameplay ke controller/sesi yang tepat. |
| `void update(float deltaTime)` | Memperbarui elemen visual dan status UI. |
| `void render(sf::RenderWindow& window)` | Menggambar halaman aktif dan komponen HUD. |
| `void returnToPreviousScreen()` | Kembali ke halaman sebelumnya; Settings yang dibuka dari Pause kembali ke Pause. |

**Tidak bertanggung jawab:** memutuskan aturan pukulan atau mengubah state pertandingan secara langsung tanpa melalui `MatchSession`.

### 13.3 `MatchSession`

**Atribut**
- `MatchConfig config`
- `MatchState state`
- `MatchState previousState`
- `std::array<Player, 2> players`
- `std::array<std::unique_ptr<PlayerController>, 2> controllers`
- `int currentPlayerIndex`
- `float remainingShotTime`
- `float activeDuration`
- `bool isResultSaved`
- `Table table`
- `Cue cue`
- `PhysicsEngine physics`
- `GameRules rules`
- `ShotStartState shotStartState`

**Method**
| Method | Kontrak |
|---|---|
| `void startMatch(const MatchConfig& config)` | Menginisialisasi konfigurasi, pemain, controller, rack, breaker, timer, dan state awal. |
| `bool submitShot(const ShotCommand& command)` | Memvalidasi state, giliran, bola diam, timer, dan command; menerima atau menolak pukulan. |
| `void update(float deltaTime)` | Memperbarui timer, simulasi, Bot, dan state sesuai kondisi sesi. |
| `void onSimulationFinished(const ShotResult& result)` | Memanggil evaluasi aturan setelah semua bola berhenti dan menerapkan `RuleOutcome`. |
| `bool placeCueBall(const sf::Vector2f& position)` | Memvalidasi dan menempatkan cue ball pada kondisi ball-in-hand. |
| `void switchTurn()` | Mengalihkan giliran dan menginisialisasi kesempatan pemain berikutnya. |
| `void handleTimeout()` | Jika sedang menarik power, mengeksekusi command pada power yang tercapai; jika tidak, mengakhiri kesempatan dan langsung mengalihkan giliran tanpa foul. |
| `void pause()` | Menyimpan state sebelumnya, menghentikan timer/fisika/Bot, dan membatalkan tarikan yang belum dilepas. |
| `void resume()` | Memulihkan state dan sisa waktu tanpa membuat snapshot atau impuls baru. |
| `void restart()` | Membatalkan sesi aktif tanpa riwayat, lalu menginisialisasi ulang konfigurasi pertandingan. |
| `MatchRecord finishMatch()` | Membentuk ringkasan hasil pertandingan yang selesai. |

**Kontrak penting:** `ShotStartState` diambil tepat satu kali setelah command diterima dan sebelum impuls diberikan. Command yang ditolak tidak membuat snapshot, impuls, atau simulasi. Hasil yang sama tidak boleh disimpan lebih dari sekali.

### 13.4 `Player`

**Atribut**
- `std::string name`
- `BallGroup ballGroup`
- `int shotCount`
- `int foulCount`
- `int pocketedBallCount`

**Method**
| Method | Kontrak |
|---|---|
| `void setName(const std::string& name)` | Mengubah nama/label pemain. |
| `void setGroup(BallGroup group)` | Menetapkan kelompok Solid/Stripe pada 8-Ball. |
| `void recordShot()` | Menambah jumlah pukulan sesuai definisi statistik proyek. |
| `void recordFoul()` | Menambah jumlah foul. |
| `void recordPocketedBall()` | Menambah jumlah bola yang dikreditkan kepada pemain. |
| `void resetStatistics()` | Mengatur ulang statistik untuk pertandingan baru. |

**Tidak bertanggung jawab:** menerima input, memilih target, atau menjalankan AI.

### 13.5 `PlayerController` (abstract)

**Method**
| Method | Kontrak |
|---|---|
| `virtual ShotCommand createShot(const Table& table, const GameRules& rules, Cue& cue) = 0` | Menghasilkan perintah pukulan dari sumber kontrol terkait. |
| `virtual void cancelAction() = 0` | Membatalkan tindakan yang belum dieksekusi menjadi pukulan. |
| `virtual ~PlayerController()` | Destructor virtual agar objek turunan aman dihapus melalui pointer dasar. |

`HumanController` dan `BotController` wajib memenuhi kontrak ini. `MatchSession` tidak perlu mengetahui detail cara masing-masing controller menghasilkan command.

### 13.6 `HumanController`

**Atribut**
- `bool isAiming`
- `bool isDraggingPower`
- `sf::Vector2f currentMousePosition`
- `float powerSensitivity`
- `bool shotReady`

**Method**
| Method | Kontrak |
|---|---|
| `void handleEvent(const sf::Event& event, Cue& cue)` | Memproses input arah, tarikan indikator power, pelepasan, Space, dan pembatalan. |
| `ShotCommand createShot(const Table& table, const GameRules& rules, Cue& cue)` | Menghasilkan command valid dari arah dan power yang sudah ditentukan. |
| `void cancelAction()` | Membatalkan tahap kontrol yang belum dilepas; tidak mengirim command pukulan. |
| `ShotCommand calculateShotCommand(const Cue& cue)` | Mengemas arah dan power final ke dalam `ShotCommand`. |

**Batas tanggung jawab:** controller membaca input dan membentuk command. Ia tidak menghitung tumbukan atau menilai foul.

### 13.7 `BotController`

**Atribut**
- `int targetBallNumber`
- `int targetPocketID`
- `sf::Vector2f plannedDirection`
- `float plannedPower`
- `bool isThinking`

**Method**
| Method | Kontrak |
|---|---|
| `ShotCommand createShot(const Table& table, const GameRules& rules, Cue& cue)` | Menghasilkan command Bot Easy melalui jalur pertandingan yang sama dengan manusia. |
| `int chooseTarget(const GameRules& rules, const Table& table)` | Memilih target legal berdasarkan mode dan kondisi meja. |
| `int choosePocket(const Table& table, int targetBallNumber)` | Memilih pocket yang dinilai layak. |
| `sf::Vector2f calculateImpulse(const Table& table, int targetBallNumber)` | Menghitung arah dan besar impuls rencana. |
| `sf::Vector2f chooseCueBallPosition(const Table& table)` | Memilih posisi valid ketika Bot memperoleh ball-in-hand. |
| `void cancelAction()` | Membatalkan keputusan Bot yang belum dikirim sebagai command. |

**Batas AI:** hanya Bot Easy. Bot memilih target dan rencana pukulan; ia tidak menjalankan fisika atau menerapkan impuls sendiri. Jika jalur pot langsung tidak tersedia, Bot boleh memakai fallback menuju target legal. Hasil fallback tetap diperiksa oleh `GameRules`.

### 13.8 `Table`

**Atribut**
- `sf::FloatRect playingArea`
- `std::vector<Ball> balls`
- `std::array<PocketData, 6> pockets`

**Method**
| Method | Kontrak |
|---|---|
| `void setupRack(GameType gameType)` | Menyiapkan susunan bola untuk 8-Ball atau 9-Ball. |
| `std::vector<Ball>& getBalls()` | Memberi akses terkontrol ke kumpulan bola untuk simulasi. |
| `Ball& getCueBall()` | Mengembalikan referensi cue ball. |
| `const std::array<PocketData, 6>& getPockets() const` | Mengembalikan data enam pocket. |
| `bool isPositionValid(const sf::Vector2f& position, float radius) const` | Memvalidasi posisi terhadap batas meja dan ruang yang tersedia. |
| `int findLowestBallNumber() const` | Mengembalikan nomor bola aktif terendah untuk 9-Ball. |
| `void reset(GameType gameType)` | Mengembalikan meja ke kondisi rack awal sesuai mode. |

### 13.9 `Ball`

**Atribut**
- `int number`
- `sf::Vector2f position`
- `sf::Vector2f velocity`
- `float radius`
- `bool isPocketed`

**Method**
| Method | Kontrak |
|---|---|
| `void applyImpulse(const sf::Vector2f& impulse)` | Menambahkan impuls pada kecepatan bola sesuai model fisika. |
| `void setPosition(const sf::Vector2f& position)` | Memperbarui posisi bola. |
| `void setVelocity(const sf::Vector2f& velocity)` | Memperbarui kecepatan bola. |
| `sf::Vector2f getPosition() const` | Mengembalikan posisi bola. |
| `sf::Vector2f getVelocity() const` | Mengembalikan kecepatan bola. |
| `bool isStationary() const` | Memeriksa apakah kecepatan berada di bawah ambang diam. |
| `void markPocketed()` | Menandai bola sudah masuk pocket dan tidak lagi ikut simulasi meja. |

### 13.10 `Cue`

**Atribut**
- `float angleRadians`
- `float pullDistance`
- `float maxPullDistance`
- `float aimLineLength`
- `bool isAiming`
- `float power`

**Method**
| Method | Kontrak |
|---|---|
| `void updateAim(const sf::Vector2f& direction)` | Memperbarui arah bidikan dari kontrol arah di meja. |
| `void updatePower(float indicatorValue)` | Memperbarui kekuatan dari indikator power terpisah. |
| `void setAim(const sf::Vector2f& direction, float power)` | Memasang arah dan power yang dipilih Bot. |
| `sf::Vector2f calculateImpulse() const` | Mengubah arah dan power menjadi impuls final. |
| `std::vector<sf::Vector2f> getPredictedTrajectory(const Table& table) const` | Menghasilkan titik prediksi lintasan cue ball dan perkiraan arah bola sasaran pertama. |
| `void cancelAim()` | Menghapus proses bidikan/power yang belum dieksekusi. |
| `void render(sf::RenderWindow& window)` | Menggambar cue stick, indikator, dan bantuan bidikan sesuai tampilan aktif. |

### 13.11 `PhysicsEngine`

**Atribut**
- `float frictionCoefficient`
- `float restitution`
- `float stopSpeedThreshold`
- `float substepDuration`

**Method**
| Method | Kontrak |
|---|---|
| `void step(float deltaTime, Table& table, ShotResult& result)` | Memperbarui satu langkah simulasi dan mencatat fakta kejadian. |
| `bool areAllBallsStationary(const Table& table) const` | Memeriksa apakah seluruh bola aktif telah berhenti. |
| `void resolveBallCollision(Ball& ballA, Ball& ballB)` | Menghitung respons tumbukan dua bola. |
| `void resolveCushionCollision(Ball& ball, const sf::FloatRect& bounds)` | Menghitung pantulan bola terhadap bantalan. |
| `void detectPocketedBalls(Table& table, ShotResult& result)` | Mendeteksi bola masuk pocket dan mencatat nomor bola serta pocket terkait. |

**Tidak bertanggung jawab:** menetapkan foul, mempertahankan giliran, atau menentukan pemenang.

### 13.12 `GameRules`

**Atribut**
- `GameType gameType`
- `bool tableOpen`
- `int chosenPocketID`

**Method**
| Method | Kontrak |
|---|---|
| `void setupRack(Table& table)` | Meminta meja menyiapkan rack sesuai mode. |
| `std::vector<int> getLegalTargets(const Player& player, const Table& table) const` | Menghasilkan target legal berdasarkan mode dan kelompok pemain. |
| `RuleOutcome evaluateShot(const ShotStartState& start, const ShotResult& result, std::array<Player, 2>& players, const Table& table)` | Menilai fakta pukulan dan menghasilkan konsekuensi aturan. |
| `void assignBallGroup(Player& player, BallGroup group)` | Menetapkan kelompok pemain pada 8-Ball. |
| `bool checkWinCondition(const Table& table, const Player& player) const` | Memeriksa kondisi kemenangan mode aktif. |
| `bool validateBallInHandPosition(const Table& table, const sf::Vector2f& position) const` | Memeriksa posisi cue ball yang diajukan. |
| `void setChosenPocket(int pocketID)` | Menyimpan pocket pilihan untuk bola 8. |

`GameRules` menggunakan percabangan `GameType` untuk aturan 8-Ball dan 9-Ball. Tidak dibuat class turunan aturan pada baseline.

### 13.13 `StorageManager`

**Atribut**
- `std::string settingsFilePath`
- `std::string historyFilePath`
- `AppSettings cachedSettings`
- `std::vector<MatchRecord> historyRecords`

**Method**
| Method | Kontrak |
|---|---|
| `AppSettings loadSettings()` | Membaca pengaturan; jika file belum ada, menggunakan nilai default yang ditetapkan. |
| `bool saveSettings(const AppSettings& settings)` | Menulis pengaturan dan mengembalikan status keberhasilan. |
| `std::vector<MatchRecord> loadHistory()` | Membaca riwayat pertandingan tersimpan. |
| `bool appendMatchRecord(const MatchRecord& record)` | Menambahkan satu catatan pertandingan selesai tanpa duplikasi. |
| `const std::vector<MatchRecord>& getMatchRecords() const` | Mengembalikan data riwayat yang telah dimuat. |

### 13.14 `AudioManager`

**Atribut**
- `sf::Music backgroundMusic`
- `std::map<SoundType, sf::SoundBuffer> soundBuffers`
- `std::vector<sf::Sound> activeSounds`
- `float soundVolume`
- `float musicVolume`

**Method**
| Method | Kontrak |
|---|---|
| `bool loadMusic(const std::string& path)` | Memuat sumber musik latar. |
| `void playMusic()` | Memutar musik latar sesuai pengaturan. |
| `void stopMusic()` | Menghentikan musik latar. |
| `bool loadSound(SoundType type, const std::string& path)` | Memuat buffer efek suara. |
| `void playSound(SoundType type)` | Memutar efek suara berdasarkan peristiwa. |
| `void setMusicVolume(float volume)` | Mengatur volume musik dan membatasi nilainya pada rentang valid. |
| `void setSoundVolume(float volume)` | Mengatur volume SFX dan membatasi nilainya pada rentang valid. |

---

## 14. Delapan Struct Pendukung

Struct berikut adalah delapan wadah data pendukung. Struct tidak menambah jumlah 14 class utama. Atribut di bawah merupakan baseline data; method tidak dicantumkan karena peran utamanya adalah membawa data antarobjek.

### 14.1 `MatchConfig`

Menyimpan konfigurasi sebelum pertandingan dimulai:
- `GameType gameType`
- `OpponentType opponentType`
- `std::array<std::string, 2> playerNames`
- `float timeLimitSeconds`
- `bool unlimitedTime`

Pilihan timer yang valid: unlimited, 15, 30, atau 60 detik.

### 14.2 `AppSettings`

Menyimpan pengaturan aplikasi:
- `bool fullscreen`
- `unsigned int windowWidth`
- `unsigned int windowHeight`
- `float musicVolume`
- `float soundVolume`
- `float dragSensitivity`

Mode Windowed mempertahankan rasio aspek tetap. Ukuran jendela dapat diubah dengan menjaga rasio tersebut.

### 14.3 `MatchRecord`

Menyimpan ringkasan satu pertandingan yang telah selesai:
- `std::string matchId`
- `std::string dateTime`
- `GameType gameType`
- `OpponentType opponentType`
- `std::array<std::string, 2> playerNames`
- `std::string winnerName`
- `std::string winReason`
- `std::array<int, 2> pocketedCounts`
- `std::array<int, 2> foulCounts`
- `std::array<int, 2> shotCounts`
- `float activeDurationSeconds`
- `float timeLimitSeconds`

### 14.4 `PocketData`

Menyimpan informasi setiap pocket:
- `int pocketID`
- `sf::Vector2f centerPosition`
- `float captureRadius`

`Table` memiliki enam objek `PocketData`.

### 14.5 `ShotCommand`

Membawa perintah pukulan dari controller ke `MatchSession`:
- `sf::Vector2f direction`
- `float power`
- `bool isValid`

### 14.6 `ShotStartState`

Snapshot kondisi penting tepat sebelum impuls diberikan:
- `std::vector<int> legalTargets`
- `bool tableOpen`
- `int activePlayerIndex`
- `bool isBreakShot`

Snapshot dibuat satu kali untuk setiap pukulan yang diterima.

### 14.7 `ShotResult`

Mencatat fakta yang terjadi selama simulasi:
- `int firstHitBallNumber`
- `std::vector<int> pocketedBallNumbers`
- `std::vector<int> pocketIDs`
- `bool cueBallPocketed`
- `bool cushionAfterFirstContact`
- `int numberedBallsHitCushionOnBreak`

Struct ini diisi oleh `PhysicsEngine`; ia tidak menentukan foul atau kemenangan.

### 14.8 `RuleOutcome`

Membawa hasil evaluasi aturan kepada `MatchSession`:
- `bool isFoul`
- `FoulType foulType`
- `bool retainTurn`
- `bool ballInHand`
- `bool matchFinished`
- `int winnerIndex`
- `std::vector<int> ballsToSpot`

---

## 15. Enumerasi

Enum membatasi nilai status dan pilihan agar tidak diwakili string atau angka bebas.

| Enum | Nilai baseline | Kegunaan |
|---|---|---|
| `GameType` | `EIGHT_BALL`, `NINE_BALL` | Mode permainan. |
| `OpponentType` | `LOCAL_PLAYER`, `BOT` | Jenis lawan. |
| `ScreenType` | `MAIN_MENU`, `MATCH_SETUP`, `GAME`, `PAUSE`, `RESULT`, `HISTORY`, `SETTINGS`, `HOW_TO_PLAY`, `EXIT_CONFIRM` | Halaman aktif. |
| `MatchState` | `SETUP`, `WAITING`, `AIMING`, `POWER_SETTING`, `BALL_IN_HAND`, `SIMULATING`, `PAUSED`, `FINISHED` | State pertandingan. |
| `BallGroup` | `NONE`, `SOLID`, `STRIPE` | Kelompok 8-Ball. |
| `FoulType` | `NONE`, `SCRATCH`, `WRONG_FIRST_HIT`, `NO_BALL_CONTACT`, `NO_CUSHION_AFTER_CONTACT`, `OTHER_RULE_VIOLATION` | Kategori foul. Timeout biasa tidak dimasukkan sebagai foul. |
| `SoundType` | `BALL_COLLISION`, `CUSHION_HIT`, `BALL_POCKETED`, `CUE_HIT`, `UI_CLICK` | Kategori efek suara. |

Nilai enum dapat diperluas hanya bila kebutuhan implementasi benar-benar memerlukannya. Penambahan nilai enum bukan penambahan class atau struct.

---

## 16. Relasi Antarobjek

| Objek pertama | Relasi | Objek kedua | Makna |
|---|---|---|---|
| `GameApp` | Composition | `ScreenManager` | Aplikasi memiliki pengelola layar. |
| `GameApp` | Composition | `StorageManager` | Aplikasi memiliki layanan penyimpanan. |
| `GameApp` | Composition | `AudioManager` | Aplikasi memiliki layanan audio. |
| `GameApp` | Association | `MatchSession` | Aplikasi membuat dan mengelola sesi aktif. |
| `MatchSession` | Composition | `Table`, `Cue`, `PhysicsEngine`, `GameRules` | Sesi memiliki komponen inti pertandingan. |
| `MatchSession` | Composition | Dua `Player` | Satu sesi memiliki dua data pemain. |
| `MatchSession` | Ownership | Dua `PlayerController` | Setiap pemain memakai controller manusia atau Bot. |
| `HumanController` | Inheritance | `PlayerController` | Memenuhi kontrak pengendali manusia. |
| `BotController` | Inheritance | `PlayerController` | Memenuhi kontrak pengendali Bot. |
| `Table` | Composition | `Ball` | Meja memiliki kumpulan bola. |
| `Table` | Composition | `PocketData` | Meja menyimpan enam data pocket. |
| `PhysicsEngine` | Association | `Table`, `Ball`, `ShotResult` | Memperbarui simulasi dan mencatat fakta fisik. |
| `GameRules` | Association | `ShotStartState`, `ShotResult`, `Player`, `Table` | Mengevaluasi hasil simulasi sesuai aturan. |
| `BotController` | Association | `Table`, `GameRules`, `Cue` | Membaca kondisi meja dan target legal untuk membuat command. |
| `StorageManager` | Association | `AppSettings`, `MatchRecord` | Membaca dan menulis data lokal. |
| `AudioManager` | Association | `SoundType`, `StorageManager` | Memutar audio sesuai event dan pengaturan. |

Relasi UML final dan multiplicity harus konsisten dengan implementasi aktual. Tidak setiap collaborator harus menjadi pointer atau atribut langsung; dependency dapat diberikan melalui parameter atau referensi.

---

## 17. Alur Kolaborasi Satu Pukulan

Urutan ini menjadi dasar implementasi dan Sequence Diagram.

1. `MatchSession` memeriksa state, giliran, status bola, timer, dan hak pemain melakukan aksi.
2. `HumanController` membaca arah yang dipilih pada cue stick di meja serta power dari indikator terpisah. Untuk Bot, `BotController` menentukan target, arah, dan power.
3. Controller menghasilkan `ShotCommand`.
4. `MatchSession::submitShot()` memvalidasi command. Jika tidak valid, proses berhenti tanpa snapshot, impuls, atau simulasi.
5. Setelah command diterima, `MatchSession` mengambil `ShotStartState` tepat satu kali.
6. `Cue` mengubah arah dan power menjadi impuls final.
7. Cue ball menerima impuls melalui operasi `Ball`.
8. `PhysicsEngine` menjalankan gerak, gesekan, tumbukan, pantulan, dan deteksi pocket sambil mengisi `ShotResult`.
9. `PhysicsEngine` memeriksa sampai semua bola berhenti.
10. `MatchSession` meminta `GameRules` mengevaluasi `ShotStartState` dan `ShotResult`.
11. `GameRules` mengembalikan `RuleOutcome`.
12. `MatchSession` memperbarui statistik, giliran, ball-in-hand, atau status menang.
13. Jika pertandingan selesai, `MatchSession` membentuk `MatchRecord` dan `StorageManager` menyimpannya satu kali.
14. `ScreenManager` memperbarui HUD atau menampilkan Result Screen.

**Pemisahan mutlak:**
- Controller tidak menjalankan fisika.
- Cue tidak menentukan foul atau pemenang.
- PhysicsEngine tidak memutuskan giliran.
- GameRules tidak menghitung tumbukan.
- MatchSession mengoordinasikan proses, bukan mengambil alih perhitungan fisika atau detail rendering.

---

## 18. State dan Kontrak Siklus Pertandingan

### 18.1 State utama

| State | Makna |
|---|---|
| `SETUP` | Konfigurasi dan persiapan pertandingan. |
| `WAITING` | Menunggu aksi pemain pada giliran aktif. |
| `AIMING` | Pemain mengatur arah cue pada meja. |
| `POWER_SETTING` | Pemain menarik indikator power terpisah. |
| `BALL_IN_HAND` | Pemain menempatkan cue ball setelah foul. |
| `SIMULATING` | Bola sedang bergerak dan fisika aktif. |
| `PAUSED` | Pertandingan dihentikan sementara. |
| `FINISHED` | Kondisi kemenangan tercapai dan hasil ditampilkan. |

### 18.2 Kontrak proses

| Proses | Prakondisi | Pos kondisi |
|---|---|---|
| Menerima pukulan | Giliran valid, bola diam, timer belum habis, state mengizinkan, command valid. | Snapshot dibuat satu kali, timer kesempatan berhenti, impuls diterapkan, state menjadi `SIMULATING`. |
| Menolak pukulan | Salah satu syarat penerimaan tidak terpenuhi. | Tidak ada snapshot, impuls, atau simulasi baru. |
| Menilai pukulan | Simulasi selesai dan seluruh bola diam. | `RuleOutcome` diterapkan oleh MatchSession. |
| Timeout saat menarik power | State `POWER_SETTING` dan timer mencapai nol. | Command dieksekusi dengan power yang tercapai; tanpa tambahan waktu. |
| Timeout tanpa menarik power | Pemain sedang tidak menarik indikator power dan timer mencapai nol. | Giliran langsung berpindah; bukan foul. |
| Pause | Sesi belum selesai. | Timer/fisika/Bot berhenti; state sebelumnya disimpan; tarikan yang belum dilepas dibatalkan. |
| Resume | State `PAUSED`. | State dan sisa waktu dipulihkan; tidak membuat snapshot, rack, atau impuls baru. |
| Restart | Pemain menyetujui konfirmasi. | Sesi aktif dibatalkan tanpa riwayat; konfigurasi pertandingan digunakan kembali untuk rack baru. |
| Kembali ke Main Menu | Pemain menyetujui konfirmasi saat pertandingan aktif. | Sesi dibatalkan dan tidak disimpan sebagai hasil selesai. |
| Simpan hasil | State `FINISHED` dan hasil belum tersimpan. | Satu `MatchRecord` disimpan; penanda berubah setelah penyimpanan berhasil. |
| Rematch | Pertandingan sebelumnya selesai. | Sesi baru dibuat dengan konfigurasi sebelumnya; pemain pembuka ditentukan ulang. |

### 18.3 Timeout dan foul

Timeout bukan satu jenis perilaku untuk semua kondisi:
- Saat power sedang ditarik: eksekusi pukulan dengan power saat itu.
- Saat tidak sedang menarik power: giliran langsung berpindah, bukan foul.
- Jika pukulan hasil timeout saat power ditarik menghasilkan pelanggaran fisik menurut aturan, hasil pukulan tetap dinilai oleh GameRules seperti pukulan biasa.

---

## 19. WBS, Jadwal, dan Penanggung Jawab

**Tanggal akhir seluruh pengembangan dan laporan akhir: 13 Desember 2026.**

PIC berarti penanggung jawab utama paket pekerjaan, bukan satu-satunya anggota yang boleh mengerjakannya. Kolaborasi dan pengerjaan bersama tetap diperbolehkan. Pembagian berikut menyelaraskan kekuatan tanggung jawab: Rapid pada antarmuka, Satya pada fisika, dan Argo pada aturan/siklus pertandingan serta integrasi data. Semua anggota tetap saling membantu saat integrasi.

| Minggu | Tanggal | Paket kerja dan hasil yang dibuat | PIC | Ketergantungan / pemeriksaan |
|---:|---|---|---|---|
| 9 | 1–4 Nov 2026 | Finalisasi kebutuhan, ruang lingkup, use case, wireframe awal, 14 class, 8 struct, pembagian tanggung jawab, dan baseline desain. | Seluruh anggota | Menjadi dasar implementasi; keputusan dan dokumen diselaraskan. |
| 10 | 5–8 Nov 2026 | Finalisasi wireframe YouKnowBall, struktur halaman, alur navigasi, serta persiapan lingkungan C++ dan SFML 2.4.2. | Rapid (UI); seluruh anggota membantu | Wireframe dan setup siap menjadi acuan kerja. |
| 11 | 9–15 Nov 2026 | Implementasi `Ball` dan `Table`; geometri meja, rack, enam pocket, render bola, gerak dasar, gesekan, pantulan bantalan, tumbukan, dan deteksi pocket pada `PhysicsEngine`. | Satya (fisika); Rapid membantu tampilan; Argo membantu integrasi | Meja dan bola tampil; simulasi dapat diuji secara mandiri. |
| 12 | 16–22 Nov 2026 | Implementasi `Cue`, `HumanController`, `ShotCommand`, `ShotStartState`, `ShotResult`, dan `RuleOutcome`; kontrol arah dan power terpisah; pembatalan Space; prediksi lintasan; evaluasi awal `GameRules`. | Satya (kontrol/fisika); Argo (aturan); Rapid (visual kontrol) | Fisika minggu 11 tersedia; satu pukulan manusia menghasilkan data yang dapat dievaluasi. |
| 13 | 23–29 Nov 2026 | Implementasi `MatchSession`; siklus pertandingan, giliran, timer, timeout dua kondisi, break, foul, scratch, ball-in-hand, pause/resume, restart, dan penyelesaian hasil. | Argo (aturan/sesi); Satya membantu integrasi fisika; Rapid membantu UI | Controller dan evaluasi pukulan tersedia; satu pertandingan dapat berjalan dari awal ke hasil. |
| 14 | 30 Nov–6 Des 2026 | Implementasi `BotController` Easy; integrasi `ScreenManager` dan seluruh halaman/HUD; Pause, Result, Rematch; `AudioManager`; `StorageManager`; Settings, History, dan penyimpanan TXT; fullscreen/windowed dengan rasio tetap. | Rapid (UI); Satya (Bot/penyelarasan gameplay); Argo (storage/aturan/integrasi) | Sesi minggu 13 stabil; seluruh fitur utama terhubung. |
| 15 | 7–13 Des 2026 | Pengujian integrasi dan kasus tepi, perbaikan bug, tuning fisika/prediksi/Bot, uji penyimpanan, stabilisasi build, finalisasi laporan, dokumentasi, dan demo/presentasi akhir. | Seluruh anggota | Semua subsistem terintegrasi; laporan dan build akhir selesai paling lambat 13 Desember. |

### 19.1 Target pemeriksaan per minggu

- **Minggu 9–10:** kebutuhan, arsitektur, dan wireframe tidak saling bertentangan.
- **Minggu 11:** bola bergerak, bertumbukan, memantul, melambat, dan masuk pocket.
- **Minggu 12:** pemain dapat membidik dan mengatur power secara terpisah; satu pukulan menghasilkan catatan simulasi.
- **Minggu 13:** aturan dan siklus pertandingan berjalan; giliran, foul, timeout, ball-in-hand, pause, dan hasil terhubung.
- **Minggu 14:** Bot, UI, audio, settings, history, dan storage terintegrasi.
- **Minggu 15:** bug utama ditangani, pengujian menyeluruh dilakukan, laporan dan demo final siap.

---

## 20. Kriteria Keberhasilan dan Pengujian

### 20.1 Kriteria kelayakan utama

Proyek dinilai memenuhi standar kelayakan utama apabila:
1. Game dapat digunakan dari Main Menu sampai hasil pertandingan.
2. Mode 8-Ball dan 9-Ball dapat dimainkan dengan aturan inti yang benar.
3. Gerak bola, gesekan, tumbukan, bantalan, dan pocket berfungsi.
4. Kontrol arah dan power terpisah berjalan sesuai rancangan, termasuk pembatalan dengan Space.
5. Pergantian giliran, foul, scratch, ball-in-hand, dan dua perilaku timeout berjalan benar.
6. Mode dua pemain lokal dan Bot Easy dapat dimainkan.
7. Pause, resume, restart, rematch, dan kembali ke menu berfungsi.
8. Pengaturan tampilan, audio, dan sensitivitas dapat diterapkan serta disimpan.
9. Hasil pertandingan dan riwayat tersimpan dengan benar.
10. Build stabil dan dapat didemonstrasikan; laporan akhir selesai.

### 20.2 Kriteria kualitas lanjutan

Setelah standar kelayakan utama tercapai, penyempurnaan dilanjutkan selama waktu memungkinkan:
- Prediksi lintasan lebih akurat dan informatif.
- Bot Easy lebih konsisten dan tidak terasa acak.
- Animasi, audio, dan feedback lebih halus.
- Pengaturan aplikasi lebih matang dan konsisten.
- Detail riwayat lebih informatif.
- Pengujian kasus tepi dan kestabilan lebih menyeluruh.

Kriteria lanjutan bukan berarti fitur inti ditunda. Prediksi lintasan, Bot Easy, audio, pengaturan, riwayat, dan pengujian tetap bagian dari cakupan proyek; daftar ini membedakan tingkat penyempurnaan kualitasnya.

### 20.3 Matriks pengujian minimum

| Area | Skenario uji | Hasil yang diharapkan |
|---|---|---|
| Alur aplikasi | Menu → setup → game → result → rematch/menu | Navigasi lengkap tanpa state rusak. |
| Mode | 8-Ball dan 9-Ball | Aturan sesuai mode yang dipilih. |
| Lawan | Lokal dan Bot Easy | Kedua jenis controller dapat bermain. |
| Kontrol | Arah cue, power terpisah, Space cancel | Arah dan power tidak tercampur; cancel tidak menembak. |
| Timeout | Habis saat power ditarik | Tembakan dilepas dengan power saat itu. |
| Timeout | Habis saat tidak menarik power | Giliran berpindah langsung, bukan foul. |
| Fisika | Gesekan, tumbukan, cushion, pocket | Gerak stabil dan kejadian tercatat. |
| 8-Ball | Open table, kelompok, bola 8, break | Kelompok dan kondisi menang/kalah benar. |
| 9-Ball | Target nomor terendah, kombinasi, bola 9 | Target legal dan kemenangan benar. |
| Foul | Wrong first hit, no contact, no cushion, scratch | Ball-in-hand dan konsekuensi sesuai aturan. |
| Pause | Pause ketika aiming/power/simulasi | Tidak ada pukulan tak sengaja; resume memulihkan konteks. |
| Restart | Restart pertandingan aktif | Rack baru; pertandingan yang dibatalkan tidak masuk riwayat. |
| Rematch | Rematch dari hasil | Konfigurasi sama; breaker ditentukan ulang. |
| Settings | Fullscreen/windowed, audio, sensitivitas | Nilai diterapkan dan tersimpan. |
| Windowed | Resize jendela | Rasio aspek tetap, tidak gepeng. |
| History | Hasil selesai dan sesi batal | Hanya pertandingan selesai dicatat, tidak duplikat. |
| File | File hilang/rusak/gagal tulis | Default atau pesan penanganan yang aman; data tidak diklaim tersimpan jika gagal. |
| Prediksi | Arah cue dan lintasan objek pertama | Prediksi mengikuti arah bidik dan cukup informatif. |
| Bot | Target legal, jalur terhalang, ball-in-hand | Bot tetap memakai jalur command dan aturan yang sama. |

---

## 21. Risiko dan Penanganan

| Risiko | Dampak | Penanganan |
|---|---|---|
| Fisika tidak stabil atau bola saling menembus | Permainan sulit dinilai | Gunakan substep, validasi collision, stop threshold, dan uji berulang. |
| Tanggung jawab class tumpang tindih | Bug sulit dilacak | Kembalikan perubahan ke kontrak RDD dan satu pemilik tanggung jawab. |
| Input arah dan power tercampur | Kontrol tidak sesuai keputusan | Pisahkan state input arah dan state indikator power. |
| Timeout mengeksekusi aksi keliru | Giliran/hasil tidak konsisten | Uji dua kondisi timeout secara terpisah. |
| Resume membuat pukulan baru | Snapshot atau impuls ganda | Resume hanya memulihkan state dan sisa waktu. |
| Bot memilih target ilegal | Bot tampak curang atau macet | Ambil target dari `GameRules::getLegalTargets()`, sediakan fallback. |
| Penyimpanan ganda atau gagal | Riwayat tidak akurat | Gunakan ID pertandingan dan ubah penanda simpan hanya setelah berhasil. |
| Windowed menjadi gepeng | UI dan meja terdistorsi | Terapkan rasio aspek tetap ketika resize. |
| Integrasi terlambat | Fitur tidak sempat diuji | Integrasikan bertahap setiap minggu, bukan menunggu semua subsistem selesai. |
| Scope melebar | Target 13 Desember terancam | Tidak menambah mode/fitur di luar scope tanpa persetujuan seluruh tim. |

---

## 22. Hal yang Belum Dikunci

Bagian ini sengaja memisahkan keputusan final dari rincian yang baru dapat ditetapkan ketika implementasi berlangsung. Hal yang belum dikunci **bukan izin untuk mengubah keputusan yang sudah final**.

| Topik | Status |
|---|---|
| Bentuk visual dan posisi indikator power terpisah | Belum dikunci; fungsi indikator hanya untuk power sudah final. |
| Detail grafis cue stick pada meja dan animasi indikator | Ditetapkan saat implementasi UI; fungsi kontrol tidak boleh berubah. |
| Parameter numerik fisika (friction, restitution, stop threshold, ukuran bola) | Ditentukan melalui tuning dan pengujian. |
| Detail algoritma prediksi lintasan | Ditentukan saat implementasi; target prediksi cue ball dan bola sasaran pertama tetap wajib. |
| Heuristik dan bobot penilaian Bot Easy | Ditentukan saat implementasi; Bot tetap Easy dan memakai jalur command bersama. |
| Format delimiter dan versi file TXT | Ditentukan saat implementasi penyimpanan. |
| Tie-break teknis untuk dua kelompok 8-Ball yang tercatat benar-benar bersamaan | Harus deterministik dan konsisten; tidak boleh acak. |
| Detail posisi rack, koordinat meja, dan titik spotting | Ditetapkan berdasarkan layout serta pengujian; aturan break dan konsekuensi mode tetap berlaku. |
| Detail tampilan halaman dan animasi | Dapat disempurnakan selama tidak mengubah alur serta fungsi yang disepakati. |
| Penanganan file rusak/tidak dapat ditulis | Harus dirancang dan diuji pada tahap StorageManager. |

---

## 23. Referensi

1. **World Pool-Billiard Association (WPA).** *WPA Rules of Play*, versi dokumen 21 Oktober 2026. [PDF aturan WPA](https://wpapool.com/wp-content/uploads/2026/10/WPA-Rules-2026-10-21-211.pdf).
2. **Materi perkuliahan DPBO.** *Desain dan Pemrograman Berorientasi Objek: Studi Kasus*, materi PowerPoint, khususnya Week-1c mengenai Responsibility-Driven Design, CRC, responsibility, dan collaborator.
3. **Kelompok 9.** *Dasar Arsitektur SimulasiBilliard Merged*, 4 November 2026. Digunakan sebagai dasar penggabungan tanggung jawab dan baseline 14 class serta 8 struct, kemudian diselaraskan dengan keputusan proyek YouKnowBall yang lebih baru.

---

## Riwayat Dokumen

| Versi | Keterangan |
|---|---|
| v01–v03 | Tahapan rancangan dan penyelarasan kebutuhan, arsitektur, kontrak, serta jadwal. |
| **v04** | README terpadu yang mengonsolidasikan keputusan final dan tambahan yang telah disepakati; tidak dimaksudkan sebagai penumpukan dokumen versi lama. |

**Aturan pemeliharaan README:** jika keputusan proyek berubah melalui persetujuan tim, perbarui bagian yang relevan pada dokumen ini dan periksa seluruh bagian yang bergantung padanya (use case, class/struct, method, alur, WBS, dan pengujian). Jangan menyimpan dua ketentuan berbeda sebagai sama-sama berlaku.

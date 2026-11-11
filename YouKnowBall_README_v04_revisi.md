# YouKnowBall

> **Dokumen:** README Proyek YouKnowBall
> **Versi dokumen:** 04
> **Mata kuliah:** Desain dan Pemrograman Berorientasi Objek (DPBO)
> **Kelompok:** 9
> **Bahasa pemrograman:** C++
> **Library:** SFML 2.4.2
> **Platform:** PC/Desktop
> **Jenis aplikasi:** Game biliar 2D top-down
> **Batas akhir proyek:** 13 Desember 2026

YouKnowBall merupakan permainan biliar 2D dengan sudut pandang top-down yang dikembangkan menggunakan C++ dan SFML 2.4.2. Permainan menyediakan dua mode, yaitu 8-Ball dan 9-Ball. Pemain dapat bertanding melawan pemain lokal lain pada satu perangkat atau melawan Bot Easy.

README ini merupakan dokumen utama proyek yang menjelaskan identitas produk, ruang lingkup, rancangan antarmuka, aturan permainan, arsitektur Object-Oriented Programming (OOP), tanggung jawab class, struktur data pendukung, alur kolaborasi, pembagian pekerjaan, jadwal, pengujian, dan ketentuan integrasi.

Dokumen ini menjadi acuan bersama selama proses pengembangan. Isi dokumen menjelaskan rancangan dan perilaku yang ditargetkan, bukan dengan sendirinya menjadi bukti bahwa seluruh fitur telah selesai diimplementasikan atau diuji.

Informasi yang belum memiliki keputusan final akan ditandai sebagai **Belum dikunci** atau **Perlu ditentukan saat implementasi**. Usulan teknis tidak boleh dianggap sebagai keputusan final hanya karena dicantumkan sebagai contoh.

---

## Daftar Isi

1. [Identitas dan Gambaran Proyek](#1-identitas-dan-gambaran-proyek)
2. [Tujuan dan Prinsip Rancangan](#2-tujuan-dan-prinsip-rancangan)
3. [Ruang Lingkup Produk](#3-ruang-lingkup-produk)
4. [Halaman, Navigasi, dan Antarmuka](#4-halaman-navigasi-dan-antarmuka)
5. [Konfigurasi Pertandingan](#5-konfigurasi-pertandingan)
6. [Kontrol Permainan](#6-kontrol-permainan)
7. [Timer dan Siklus Giliran](#7-timer-dan-siklus-giliran)
8. [Aturan Permainan](#8-aturan-permainan)
9. [Prediksi Lintasan](#9-prediksi-lintasan)
10. [Bot Easy](#10-bot-easy)
11. [Hasil, Riwayat, dan Pengaturan Aplikasi](#11-hasil-riwayat-dan-pengaturan-aplikasi)
12. [Arsitektur dan Keputusan Penggabungan Class](#12-arsitektur-dan-keputusan-penggabungan-class)
13. [CRC dan Spesifikasi 14 Class](#13-crc-dan-spesifikasi-14-class)
14. [Delapan Struct Pendukung](#14-delapan-struct-pendukung)
15. [Enumerasi Pendukung](#15-enumerasi-pendukung)
16. [Hubungan Antarkelas](#16-hubungan-antarkelas)
17. [Alur Kolaborasi Satu Pukulan](#17-alur-kolaborasi-satu-pukulan)
18. [Use Case dan Skenario Penggunaan](#18-use-case-dan-skenario-penggunaan)
19. [Pembagian Peran Anggota](#19-pembagian-peran-anggota)
20. [Pembagian Kerja dan WBS Minggu 9–15](#20-pembagian-kerja-dan-wbs-minggu-915)
21. [Kontrak Perilaku dan Ketentuan Integrasi](#21-kontrak-perilaku-dan-ketentuan-integrasi)
22. [Pengujian Minimum](#22-pengujian-minimum)
23. [Risiko dan Mitigasi](#23-risiko-dan-mitigasi)
24. [Kriteria Penyelesaian](#24-kriteria-penyelesaian)
25. [Nilai Teknis yang Ditetapkan Saat Implementasi](#25-nilai-teknis-yang-ditetapkan-saat-implementasi)
26. [Hal yang Belum Dikunci](#26-hal-yang-belum-dikunci)
27. [Rujukan](#27-rujukan)
28. [Riwayat Perubahan](#28-riwayat-perubahan)

---

## 1. Identitas dan Gambaran Proyek

YouKnowBall adalah game simulasi biliar 2D dengan sudut pandang top-down yang dikembangkan menggunakan C++ dan SFML 2.4.2. Permainan menyediakan mode 8-Ball dan 9-Ball dengan dua pilihan jenis lawan, yaitu pemain lokal dan Bot Easy.

Proyek ini dikembangkan oleh Kelompok 9 untuk memenuhi tugas mata kuliah Desain dan Pemrograman Berorientasi Objek (DPBO). Perancangan sistem menerapkan konsep Object-Oriented Programming melalui pembagian tanggung jawab class, enkapsulasi, abstraksi, polimorfisme, dan kolaborasi ant objek.

### 1.1 Identitas kelompok

| Informasi | Keterangan |
|---|---|
| Kelompok | 9 |
| Anggota 1 | Rapid Akbar Sinatria |
| Anggota 2 | Muhammad Argo Iman |
| Anggota 3 | Satya Firma Ashari |
| Nama produk | YouKnowBall |
| Bahasa pemrograman | C++ |
| Library | SFML 2.4.2 |
| Platform | PC/Desktop |
| Bentuk permainan | Biliar 2D top-down |

### 1.2 Tujuan README

README ini digunakan sebagai acuan untuk:

- Menjelaskan identitas, tujuan, dan ruang lingkup YouKnowBall.
- Menjadi dokumentasi utama proyek pada repository GitHub.
- Menjadi acuan rancangan OOP dan pembagian tanggung jawab class.
- Menjelaskan atribut, method, responsibility, dan collaborator setiap class.
- Menjadi dasar penyusunan CRC Card, Class Diagram, Sequence Diagram, dan State Diagram.
- Menjaga konsistensi perilaku permainan selama implementasi.
- Menjadi pedoman pembagian pekerjaan, Work Breakdown Structure (WBS), dan pengujian.
- Menjadi referensi bagi seluruh anggota kelompok ketika melakukan integrasi.

### 1.3 Status dokumen

README v04 mengonsolidasikan kelengkapan spesifikasi dari v02, keputusan arsitektur dan kontrak method dari v03, serta keputusan proyek yang tercantum dalam dokumen kerja terbaru. Dokumen ini adalah acuan rancangan; status implementasi setiap fitur tetap harus dibuktikan melalui kode dan pengujian.

Jika terdapat perbedaan antara rancangan lama dan keputusan terbaru yang sudah dikunci, gunakan keputusan terbaru yang dijelaskan dalam README ini.

---

## 2. Tujuan dan Prinsip Rancangan

Perancangan YouKnowBall menggunakan pendekatan **Responsibility-Driven Design (RDD)**. Setiap class memiliki tanggung jawab yang jelas, mengelola informasi yang menjadi bagiannya, melakukan tindakan sesuai kewenangannya, dan berkolaborasi dengan class lain apabila suatu proses membutuhkan tanggung jawab tambahan.

### 2.1 Prinsip rancangan

Prinsip desain yang digunakan:

1. Arsitektur utama mempertahankan tepat **14 class utama dan 8 struct pendukung**.
2. Class tidak dibuat hanya untuk mewakili setiap halaman, tombol, atau elemen visual.
3. Fungsi yang memiliki tanggung jawab sejenis digabung apabila masih dapat dikelola secara wajar dalam satu class.
4. Setiap class harus memiliki batas tanggung jawab yang jelas dan tidak saling mengambil alih pekerjaan class lain.
5. `PhysicsEngine` bertanggung jawab mencatat fakta fisika, sedangkan `GameRules` mengevaluasi fakta tersebut berdasarkan aturan permainan.
6. `MatchSession` bertanggung jawab mengatur alur pertandingan dan menerapkan hasil evaluasi aturan.
7. `Player` menyimpan identitas dan statistik pemain, sedangkan controller menentukan tindakan pemain.
8. Pemain manusia dan Bot menggunakan jalur eksekusi pukulan yang sama.
9. Pengelolaan halaman dilakukan oleh `ScreenManager`, bukan dengan membuat class terpisah untuk setiap halaman.
10. Data pendukung yang tidak membutuhkan perilaku kompleks menggunakan struct.
11. Detail teknis yang belum disepakati harus ditandai sebagai hal yang perlu ditentukan, bukan dianggap sebagai keputusan final.
12. Perubahan terhadap arsitektur baseline harus memiliki alasan teknis yang jelas dan disepakati kelompok.

### 2.2 Responsibility-Driven Design

Dalam dokumentasi CRC, tanggung jawab class dibagi menjadi tiga bagian:

- **Knowing Responsibility:** informasi atau data yang diketahui dan dikelola oleh suatu class.
- **Doing Responsibility:** tindakan atau proses yang menjadi tanggung jawab suatu class.
- **Collaborator:** class lain yang bekerja sama untuk menyelesaikan suatu tanggung jawab.

Ketiga bagian tersebut digunakan untuk memastikan bahwa setiap class memiliki fungsi yang jelas dan tidak terjadi tumpang tindih tanggung jawab.

### 2.3 Prinsip pemisahan tanggung jawab

Beberapa batas tanggung jawab utama yang harus dipertahankan:

| Komponen | Tanggung jawab |
|---|---|
| `GameApp` | Mengelola siklus hidup dan jalannya aplikasi. |
| `ScreenManager` | Mengelola halaman, navigasi, dan tampilan antarmuka. |
| `MatchSession` | Mengelola jalannya pertandingan, giliran, timer, dan state pertandingan. |
| `Player` | Menyimpan identitas dan statistik pemain. |
| `PlayerController` | Menjadi kontrak dasar pengendali tindakan pemain. |
| `HumanController` | Mengolah input pemain manusia menjadi perintah pukulan. |
| `BotController` | Menentukan tindakan Bot Easy. |
| `Table` | Mengelola meja, bola, pocket, dan validasi posisi. |
| `Ball` | Menyimpan kondisi fisik satu bola. |
| `Cue` | Mengelola arah, power, impulse, dan prediksi lintasan. |
| `PhysicsEngine` | Menghitung pergerakan, tumbukan, pantulan, dan deteksi pocket. |
| `GameRules` | Mengevaluasi hasil pukulan berdasarkan aturan permainan. |
| `StorageManager` | Mengelola penyimpanan pengaturan dan riwayat lokal. |
| `AudioManager` | Mengelola musik dan efek suara. |

---

## 3. Ruang Lingkup Produk

### 3.1 Fitur yang termasuk dalam ruang lingkup

Fitur yang menjadi bagian dari YouKnowBall:

- Mode permainan 8-Ball.
- Mode permainan 9-Ball.
- Mode lawan pemain lokal, yaitu dua pemain yang bermain bergantian pada satu perangkat.
- Mode lawan Bot Easy.
- Bot Easy tersedia untuk mode 8-Ball dan 9-Ball.
- Pengaturan nama pemain sebelum pertandingan.
- Pilihan timer per giliran: tanpa batas, 15 detik, 30 detik, atau 60 detik.
- Kontrol arah dan kekuatan pukulan yang terpisah.
- Meja biliar, cue ball, object ball, cue stick, dan enam pocket.
- Simulasi pergerakan bola, gesekan, perlambatan, tumbukan antarb bola, pantulan cushion, dan deteksi pocket.
- Evaluasi aturan permainan 8-Ball dan 9-Ball.
- Pengelolaan giliran, foul, scratch, ball-in-hand, dan kondisi kemenangan.
- Prediksi lintasan sederhana.
- Pause dan resume pertandingan.
- Restart pertandingan yang sedang berlangsung.
- Rematch setelah pertandingan selesai.
- Kembali ke Main Menu.
- Halaman utama dengan akses langsung ke mode 8-Ball dan 9-Ball.
- Halaman pengaturan pertandingan.
- Halaman permainan dan HUD.
- Pause Menu.
- Results Screen.
- Match History dan detail riwayat.
- Pengaturan aplikasi, termasuk Windowed/Fullscreen dengan konten 16:9.
- Halaman How to Play.
- Konfirmasi keluar aplikasi.
- Penyimpanan pengaturan aplikasi secara lokal menggunakan file TXT.
- Penyimpanan hasil pertandingan yang telah selesai menggunakan file TXT.
- Statistik dasar pertandingan.

### 3.2 Fitur di luar ruang lingkup

Fitur berikut tidak termasuk dalam target pengembangan:

- Multiplayer online atau LAN.
- Login dan akun pengguna.
- Server atau database eksternal.
- Matchmaking online.
- Bot Normal dan Bot Hard.
- Pocket Challenge.
- Spin shot.
- Jump shot.
- Replay pertandingan.
- Turnamen.
- Melanjutkan pertandingan yang belum selesai setelah aplikasi ditutup.

### 3.3 Batasan ruang lingkup

Rincian seperti rumus fisika, nilai gesekan, strategi internal Bot Easy, format serialisasi TXT, dan nilai teknis lainnya dapat ditentukan selama implementasi.

Penentuan detail teknis tersebut tidak otomatis dianggap sebagai penambahan fitur selama masih berada dalam ruang lingkup yang telah disepakati.

---

## 4. Halaman, Navigasi, dan Antarmuka

### 4.1 Main Menu

Main Menu merupakan halaman utama yang menjadi titik awal navigasi aplikasi.

Main Menu menyediakan tombol:

1. **Main 8-Ball** — memilih mode permainan 8-Ball.
2. **Main 9-Ball** — memilih mode permainan 9-Ball.
3. **Match History** — membuka daftar pertandingan yang telah selesai.
4. **App Settings** — membuka pengaturan aplikasi.
5. **How to Play** — membuka petunjuk kontrol dan aturan permainan.
6. **Exit** — meminta konfirmasi sebelum aplikasi ditutup.

Tombol Main 8-Ball dan Main 9-Ball merupakan akses langsung untuk memilih mode permainan dari halaman utama.

Setelah pemain memilih salah satu mode, sistem membuka konfigurasi pertandingan untuk mode yang dipilih. Pemain kemudian dapat menentukan jenis lawan, nama pemain, dan batas waktu sebelum pertandingan dimulai.

**Tidak menggunakan alur satu tombol Start Match yang kemudian meminta pemain memilih 8-Ball atau 9-Ball.** Pemilihan mode sudah dilakukan melalui tombol Main 8-Ball atau Main 9-Ball pada Main Menu.

### 4.2 Match Setup

Halaman Match Setup menampilkan konfigurasi pertandingan berdasarkan mode yang dipilih dari Main Menu.

Informasi dan pilihan yang tersedia:

- Jenis permainan yang sudah dipilih dari Main Menu.
- Jenis lawan: Pemain Lokal atau Bot Easy.
- Nama pemain.
- Batas waktu per giliran.
- Tombol untuk memulai pertandingan.
- Tombol kembali ke Main Menu.

Mode 8-Ball atau 9-Ball tidak dipilih ulang pada halaman ini karena pemain sudah menentukan mode melalui tombol pada Main Menu.

### 4.3 Game Screen

Game Screen menampilkan area permainan dan informasi yang dibutuhkan selama pertandingan.

Komponen minimum:

- Meja biliar.
- Pocket.
- Cue ball dan object ball.
- Cue stick.
- Indikator arah bidikan.
- Indikator power yang terpisah dari kontrol arah.
- Prediksi lintasan.
- Nama pemain.
- Informasi pemain yang sedang mendapat giliran.
- Informasi target permainan.
- Timer apabila batas waktu digunakan.
- Akses Pause melalui tombol Esc.

### 4.4 Pause Menu

Pause Menu dapat dibuka menggunakan tombol **Esc**.

Pilihan pada Pause Menu:

1. **Lanjutkan** — melanjutkan pertandingan dari kondisi sebelumnya.
2. **Pengaturan** — membuka Settings tanpa menjalankan simulasi pertandingan.
3. **Mulai Ulang** — mengulang pertandingan aktif dengan konfigurasi yang sama, setelah konfirmasi.
4. **Menu Utama** — membatalkan pertandingan aktif dan kembali ke Main Menu, setelah konfirmasi.

### 4.5 Results Screen

Results Screen muncul setelah pertandingan selesai.

Informasi minimum:

- Nama pemain.
- Nama pemenang.
- Jenis permainan.
- Ringkasan hasil pertandingan.
- Statistik bola masuk.
- Statistik foul.
- Durasi pertandingan.

Pilihan pada Results Screen:

- **Rematch** — langsung memulai pertandingan baru menggunakan konfigurasi pertandingan sebelumnya.
- **Main Menu** — kembali ke halaman utama.

### 4.6 Match History

Match History menampilkan daftar pertandingan yang telah selesai dan berhasil disimpan.

Pemain dapat memilih salah satu catatan untuk melihat detail pertandingan.

Pertandingan yang dibatalkan, di-restart sebelum selesai, atau ditinggalkan sebelum selesai tidak dimasukkan ke Match History.

### 4.7 Settings

Settings menyediakan pengaturan:

- Music Volume.
- SFX Volume.
- Mouse Sensitivity.
- Display Mode: Windowed atau Fullscreen.

Settings dapat dibuka dari Main Menu maupun Pause Menu.

### 4.8 How to Play

How to Play menjelaskan:

- Cara mengatur arah bidikan.
- Cara mengatur power.
- Fungsi tombol Space.
- Cara melakukan pukulan.
- Cara melakukan Pause.
- Aturan dasar 8-Ball.
- Aturan dasar 9-Ball.
- Foul dan scratch.
- Ball-in-hand.

### 4.9 Pengelolaan halaman

Tidak dibuat class terpisah untuk setiap halaman. Pengelolaan halaman dan perpindahan antarhalaman dilakukan melalui `ScreenManager`.

---

## 5. Konfigurasi Pertandingan

Konfigurasi pertandingan dilakukan setelah pemain memilih Main 8-Ball atau Main 9-Ball dari Main Menu.

| Pengaturan | Pilihan |
|---|---|
| Jenis permainan | Mengikuti tombol mode yang dipilih pada Main Menu |
| Mode lawan | Pemain Lokal / Bot Easy |
| Nama pemain 1 | Diisi pengguna |
| Nama pemain 2 | Diisi pengguna pada mode Pemain Lokal |
| Identitas pemain 2 pada mode Bot | Bot Easy |
| Batas waktu per giliran | Tanpa batas / 15 / 30 / 60 detik |

### 5.1 Mode Pemain Lokal

Dua pemain menggunakan satu perangkat yang sama dan bermain secara bergantian.

Nama kedua pemain dapat diatur sebelum pertandingan dimulai.

### 5.2 Mode Bot Easy

Satu pemain manusia bertanding melawan Bot Easy.

Bot Easy mengambil keputusan pukulan secara otomatis dan menggunakan jalur pemrosesan pukulan yang sama dengan pemain manusia.

### 5.3 Pilihan timer

Pilihan waktu per giliran:

- Tanpa batas.
- 15 detik.
- 30 detik.
- 60 detik.

Nilai tanpa batas direpresentasikan sebagai `0` pada `MatchConfig`.

### 5.4 Konfigurasi Rematch

Rematch menggunakan kembali konfigurasi pertandingan yang telah selesai, termasuk:

- Jenis permainan.
- Jenis lawan.
- Nama pemain.
- Batas waktu.
- Konfigurasi pertandingan lain yang digunakan.

Untuk mengubah konfigurasi, pemain harus kembali ke Main Menu dan memilih tombol Main 8-Ball atau Main 9-Ball sesuai mode yang ingin dimainkan.

---

## 6. Kontrol Permainan

Kontrol arah dan power dipisahkan agar pemain dapat menentukan arah dan kekuatan pukulan secara terkontrol.

### 6.1 Mengatur arah bidikan

- Pemain menggunakan mouse untuk mengatur arah cue.
- Cue stick ditampilkan pada area meja billiard.
- Arah cue menunjukkan arah bidikan.
- Pemain menentukan arah terlebih dahulu sebelum mengatur power.

### 6.2 Mengatur kekuatan pukulan

- Power diatur melalui indikator cue/stik yang terpisah dari kontrol arah.
- Indikator power hanya digunakan untuk mengatur kekuatan pukulan.
- Mengubah power tidak boleh mengubah arah bidikan.
- Persentase power tidak wajib ditampilkan selama indikator visual dapat menunjukkan tingkat kekuatan.

### 6.3 Penguncian arah

Ketika pemain sedang mengatur power:

- Arah bidikan dikunci.
- Perubahan posisi indikator power hanya memengaruhi kekuatan pukulan.
- Pemain tidak dapat mengubah arah sampai proses pengaturan power dibatalkan atau selesai.

### 6.4 Membatalkan pengaturan power

Pemain dapat menekan tombol **Space** sebelum mouse dilepas.

Jika tombol Space ditekan:

- Pengaturan power dibatalkan.
- Pukulan tidak dijalankan.
- Pemain kembali ke tahap mengatur arah bidikan.

### 6.5 Menjalankan pukulan

Pukulan dijalankan ketika pemain melepaskan mouse secara normal setelah menentukan arah dan power.

Sistem menggunakan arah dan power yang sudah ditentukan untuk membentuk perintah pukulan.

### 6.6 Pause ketika input sedang berlangsung

Jika pemain membuka Pause ketika sedang melakukan drag yang belum menghasilkan pukulan:

- Input drag dibatalkan.
- Tidak ada pukulan yang dijalankan.
- Arah dan power tidak boleh tersimpan sebagai pukulan yang belum dikonfirmasi.
- Setelah pemain melanjutkan permainan, pemain kembali ke kondisi siap mengatur pukulan.

---

## 7. Timer dan Siklus Giliran

### 7.1 Pilihan waktu

Timer per giliran memiliki empat pilihan:

| Pilihan | Durasi |
|---|---:|
| Unlimited | Tanpa batas |
| 15 Seconds | 15 detik |
| 30 Seconds | 30 detik |
| 60 Seconds | 60 detik |

### 7.2 Perilaku timer

- Timer mulai berjalan ketika pemain berikutnya sudah siap bermain.
- Timer berjalan ketika pemain mengatur arah bidikan dan power.
- Timer berhenti ketika bola sedang bergerak dalam simulasi.
- Timer berhenti ketika pertandingan berada dalam kondisi Pause.
- Resume melanjutkan sisa waktu sebelumnya, bukan mengatur ulang timer.
- Setelah seluruh bola berhenti, hasil pukulan dievaluasi sebelum giliran berikutnya dimulai.

### 7.3 Timeout ketika pemain tidak sedang mengatur power

Jika timer habis ketika pemain tidak sedang melakukan drag power:

- Giliran langsung berpindah kepada lawan.
- Timeout tidak dihitung sebagai foul.
- Lawan tidak memperoleh ball-in-hand akibat timeout.
- Sistem memulai timer giliran baru ketika pemain berikutnya sudah siap.

### 7.4 Timeout ketika pemain sedang mengatur power

Jika timer habis ketika pemain sedang melakukan drag power:

- Sistem langsung mengeksekusi pukulan.
- Power yang digunakan adalah power yang telah tercapai pada saat timer habis.
- Tidak ada tambahan waktu untuk menyelesaikan drag.
- Arah bidikan tetap menggunakan arah yang telah dikunci ketika pengaturan power dimulai.

### 7.5 Timer ketika Pause dan Resume

- Timer berhenti selama Pause.
- Simulasi fisika juga berhenti selama Pause.
- Ketika pemain memilih Lanjutkan, simulasi kembali berjalan sesuai kondisi sebelumnya.
- Timer meneruskan sisa waktu yang dimiliki pemain sebelum Pause.

Timeout bukan jenis foul dan tidak memberikan ball-in-hand.

---

## 8. Aturan Permainan

Aturan permainan YouKnowBall mengadaptasi aturan dasar 8-Ball dan 9-Ball untuk kebutuhan proyek.

Dokumen WPA digunakan sebagai referensi aturan. Namun, implementasi YouKnowBall tidak diklaim sebagai penerapan penuh seluruh peraturan turnamen WPA.

### 8.1 Aturan umum

- Permainan menggunakan cue ball untuk memukul object ball.
- Pemain harus menunggu sampai seluruh bola berhenti sebelum melakukan pukulan berikutnya.
- Hasil pukulan dievaluasi setelah simulasi selesai.
- `PhysicsEngine` mencatat kejadian fisik.
- `GameRules` mengevaluasi kejadian tersebut berdasarkan aturan permainan.
- `MatchSession` menerapkan hasil evaluasi terhadap giliran dan status pertandingan.
- Scratch dihitung sebagai foul.
- Foul yang diterapkan dalam proyek memberikan giliran kepada lawan dan hak ball-in-hand.
- Timeout bukan foul dan tidak memberikan ball-in-hand.

### 8.2 Aturan 8-Ball

#### Kelompok bola

- **Solid:** bola nomor 1–7.
- **Stripe:** bola nomor 9–15.
- **Bola 8:** bola penentu kemenangan.

#### Kondisi awal meja

Pada awal permainan:

- Meja berstatus terbuka (*open table*).
- Kelompok bola pemain belum ditentukan.
- Kedua pemain belum memiliki kelompok Solid atau Stripe.

#### Penentuan kelompok

Kelompok pemain ditentukan ketika satu pukulan sah memasukkan bola dari satu kelompok saja.

Jika bola Solid dan Stripe masuk secara bersamaan ketika meja masih terbuka:

- Kelompok pemain belum ditentukan.
- Meja tetap berstatus terbuka.
- Kelompok ditentukan pada pukulan berikutnya yang secara sah memasukkan bola dari satu kelompok saja.

#### Kelanjutan giliran

Pukulan sah yang memasukkan bola dari kelompok pemain sendiri membuat pemain tetap memperoleh giliran.

#### Kondisi kalah dan menang

- Bola 8 yang masuk sebelum seluruh kelompok sendiri habis menyebabkan pemain yang memukul kalah.
- Bola 8 yang masuk secara sah setelah seluruh kelompok sendiri habis menyebabkan pemain yang memukul menang.
- Bola 8 yang masuk bersama scratch atau foul menyebabkan pemain yang memukul kalah.

#### Bola 8 pada break

Jika bola 8 masuk pada break:

- Bola 8 dikembalikan ke meja.
- Permainan dilanjutkan.
- Kondisi tersebut tidak langsung menghasilkan kemenangan atau kekalahan.

### 8.3 Aturan 9-Ball

#### Kontak pertama

Bola aktif dengan nomor terendah harus menjadi bola pertama yang terkena cue ball.

Bola lain boleh masuk selama kontak pertama tetap mengenai bola aktif bernomor terendah dan ketentuan pukulan sah terpenuhi.

#### Kondisi menang

Memasukkan bola 9 secara sah menyebabkan pemain yang melakukan pukulan menang.

#### Bola 9 masuk bersama foul

Jika bola 9 masuk dalam pukulan yang mengandung foul:

- Pukulan tidak menghasilkan kemenangan.
- Bola 9 dikembalikan ke meja.
- Foul tetap diproses.
- Giliran dan ball-in-hand ditentukan berdasarkan hasil evaluasi foul.

#### Bola 9 pada break

Jika bola 9 masuk saat break:

- Bola 9 dikembalikan ke meja.
- Permainan dilanjutkan.
- Bola 9 yang masuk pada break tidak langsung menghasilkan kemenangan.

### 8.4 Foul dan scratch

- Scratch adalah kondisi ketika cue ball masuk ke pocket.
- Scratch dihitung sebagai foul.
- Foul yang dikenali oleh implementasi proyek menyebabkan giliran berpindah kepada lawan.
- Lawan memperoleh hak ball-in-hand.
- Timeout biasa bukan foul.
- Timeout tidak memberikan ball-in-hand.
- Daftar foul selain scratch belum dikunci sebagai daftar final. Jenis foul tambahan hanya boleh dicantumkan sebagai fitur final jika telah disepakati, diimplementasikan, dan diuji.

Daftar foul selain scratch harus mengikuti kondisi yang benar-benar ditetapkan dan diimplementasikan dalam proyek. Jangan mengklaim bahwa seluruh foul dalam peraturan resmi pool telah diterapkan apabila implementasi hanya mencakup aturan dasar proyek.

### 8.5 Ball-in-hand

Ball-in-hand merupakan hak pemain untuk menempatkan cue ball sebelum melakukan pukulan berikutnya.

Posisi cue ball harus memenuhi ketentuan:

1. Berada di dalam area permainan yang diizinkan.
2. Tidak bertumpuk atau overlap dengan bola aktif lainnya.
3. Tidak berada di dalam pocket.
4. Divalidasi sebelum pemain kembali ke tahap membidik.

Pembagian tanggung jawab:

- `GameRules` menentukan apakah suatu hasil pukulan memberikan hak ball-in-hand.
- `MatchSession` mengatur perubahan state dan fase penempatan cue ball.
- `Table` memvalidasi apakah posisi yang dipilih memenuhi batas area dan geometri meja.

### 8.6 Batas adaptasi aturan

Aturan yang dijelaskan dalam bagian ini merupakan aturan yang ditetapkan untuk proyek YouKnowBall.

Kasus aturan tambahan yang belum disepakati tidak boleh ditulis sebagai fitur final hanya berdasarkan asumsi atau referensi umum.

---

## 9. Prediksi Lintasan

Prediksi lintasan merupakan fitur standar permainan yang membantu pemain memperkirakan hasil awal dari arah pukulan.

Prediksi dibatasi pada:

1. Garis prediksi cue ball sampai perkiraan titik tumbukan pertama.
2. Prediksi arah object ball setelah tumbukan pertama.

Prediksi merupakan bantuan visual dan tidak menjamin lintasan akhir seluruh bola.

Ketentuan:

- Prediksi tidak mengubah posisi bola.
- Prediksi tidak menjalankan simulasi pertandingan.
- Prediksi tidak menentukan foul atau kemenangan.
- Prediksi tidak menggantikan perhitungan `PhysicsEngine`.
- Tumbukan lanjutan, gesekan, pantulan cushion, dan interaksi dengan bola lain tetap dihitung oleh `PhysicsEngine`.

Prediksi lintasan termasuk dalam target **Standar 90**, bukan fitur yang ditunda ke Standar 100.

---

## 10. Bot Easy

Bot Easy merupakan lawan komputer yang tersedia untuk mode 8-Ball dan 9-Ball.

### 10.1 Tanggung jawab Bot Easy

Bot Easy bertugas:

- Membaca kondisi meja.
- Membaca informasi pemain dan giliran.
- Menentukan target pukulan yang sesuai dengan aturan permainan.
- Memilih arah pukulan.
- Menentukan kekuatan pukulan.
- Menghasilkan `ShotCommand` untuk dikirimkan ke `MatchSession`.

### 10.2 Batas implementasi Bot

- Bot menggunakan heuristik sederhana.
- Bot tidak memiliki mesin fisika sendiri.
- Bot tidak menjalankan simulasi terpisah.
- Bot menggunakan `PlayerController` melalui `BotController`.
- Bot menghasilkan `ShotCommand` dengan format yang sama seperti pemain manusia.
- Pukulan Bot diproses melalui `MatchSession`.
- Simulasi pukulan tetap dilakukan oleh `PhysicsEngine`.
- Evaluasi hasil pukulan tetap dilakukan oleh `GameRules`.

### 10.3 Tingkat kesulitan

Hanya **Bot Easy** yang termasuk dalam ruang lingkup proyek.

Bot Normal dan Bot Hard tidak termasuk dalam target implementasi.

Detail strategi internal, pemilihan target, dan fallback Bot Easy dapat ditentukan saat implementasi selama tetap mengikuti aturan permainan dan batas tanggung jawab class.

---

## 11. Hasil, Riwayat, dan Pengaturan Aplikasi

### 11.1 Results Screen

Setelah kondisi kemenangan terpenuhi, sistem menampilkan Results Screen.

Informasi minimum:

- Nama pemain pertama.
- Nama pemain kedua.
- Nama pemenang.
- Jenis permainan.
- Mode lawan.
- Jumlah bola yang masuk sesuai pencatatan statistik proyek.
- Jumlah foul setiap pemain.
- Durasi pertandingan.

Results Screen menyediakan dua pilihan:

- **Rematch**
- **Main Menu**

### 11.2 Keputusan final Rematch

Rematch menggunakan pendekatan **langsung memulai pertandingan baru dengan konfigurasi pertandingan sebelumnya**.

Alurnya:

1. Pertandingan selesai.
2. Results Screen ditampilkan.
3. Pemain memilih Rematch.
4. Sistem langsung membuat pertandingan baru.
5. Konfigurasi pertandingan sebelumnya digunakan kembali.
6. Pertandingan baru dimulai tanpa membuka halaman konfigurasi.
7. Hasil pertandingan sebelumnya tetap tersimpan di Match History.
8. Hasil pertandingan Rematch disimpan sebagai record baru setelah pertandingan tersebut selesai.

Konfigurasi yang digunakan kembali mencakup:

- Mode permainan 8-Ball atau 9-Ball.
- Jenis lawan.
- Nama pemain.
- Batas waktu.
- Konfigurasi pertandingan lain yang digunakan sebelumnya.

Jika pemain ingin mengganti mode permainan atau konfigurasi lainnya, pemain harus memilih Main Menu terlebih dahulu.

Dari Main Menu, pemain dapat memilih Main 8-Ball atau Main 9-Ball dan mengatur pertandingan baru.

### 11.3 Perbedaan Rematch dan Restart

| Fitur | Perilaku |
|---|---|
| Rematch | Memulai pertandingan baru setelah pertandingan selesai dengan konfigurasi pertandingan sebelumnya. |
| Restart / Mulai Ulang | Mengulang pertandingan yang sedang berlangsung dengan konfigurasi yang sama. |
| Main Menu → Main 8-Ball | Memulai konfigurasi pertandingan baru untuk mode 8-Ball. |
| Main Menu → Main 9-Ball | Memulai konfigurasi pertandingan baru untuk mode 9-Ball. |

Rematch dan Restart merupakan dua tindakan yang berbeda dan tidak boleh dipertukarkan.

### 11.4 Restart dari Pause Menu

Restart digunakan untuk mengulang pertandingan yang masih berlangsung.

Ketentuannya:

- Pemain memilih Mulai Ulang dari Pause Menu.
- Sistem menampilkan konfirmasi sebelum pertandingan aktif dibatalkan.
- Jika pemain membatalkan konfirmasi, pertandingan tetap berada dalam kondisi Pause.
- Jika pemain menyetujui, pertandingan dimulai kembali dari awal.
- Konfigurasi pertandingan tetap sama seperti konfigurasi sebelumnya.
- Pertandingan yang dibatalkan tidak disimpan sebagai hasil selesai.
- Restart tidak membuat catatan Match History untuk pertandingan yang dibatalkan.

### 11.5 Kembali ke Main Menu dari Pause

Jika pemain memilih Menu Utama ketika pertandingan masih berlangsung:

- Sistem menampilkan konfirmasi.
- Jika pemain membatalkan konfirmasi, pemain tetap berada di Pause Menu.
- Jika pemain menyetujui, pertandingan aktif dibatalkan.
- Sistem kembali ke Main Menu.
- Pertandingan yang dibatalkan tidak disimpan ke Match History.

### 11.6 Penyimpanan Match History

- Pertandingan yang telah selesai disimpan ke Match History.
- Penyimpanan dilakukan secara lokal menggunakan file TXT.
- Setiap pertandingan selesai menghasilkan satu catatan baru.
- Pertandingan yang dibatalkan sebelum selesai tidak disimpan.
- Pertandingan yang di-restart sebelum selesai tidak disimpan.
- Hasil pertandingan sebelumnya tetap tersimpan ketika pemain melakukan Rematch.
- Hasil Rematch baru disimpan setelah pertandingan Rematch selesai.
- Satu pertandingan selesai tidak boleh tersimpan lebih dari satu kali.

### 11.7 Data Match Record

`MatchRecord` digunakan untuk menyimpan ringkasan hasil pertandingan.

Data yang dicatat mencakup:

- Identitas record.
- Tanggal dan waktu pertandingan.
- Jenis permainan.
- Jenis lawan.
- Nama pemain.
- Nama pemenang.
- Statistik bola masuk.
- Statistik foul.
- Durasi pertandingan.
- Batas waktu yang digunakan.

Detail atribut dan tipe data mengikuti spesifikasi struct pada bagian arsitektur.

### 11.8 Pengaturan aplikasi

Pengaturan aplikasi mencakup:

- Music Volume.
- SFX Volume.
- Mouse Sensitivity.
- Display Mode: Windowed atau Fullscreen.

Pengaturan disimpan secara lokal menggunakan file TXT dan dimuat kembali ketika aplikasi dijalankan.

### 11.9 Pengaturan dari Main Menu

Jika Settings dibuka dari Main Menu:

- Sistem menampilkan nilai pengaturan saat ini.
- Pengguna dapat mengubah seluruh pengaturan yang tersedia.
- Tombol Terapkan/Simpan menerapkan perubahan dan menyimpannya ke file TXT.
- Tombol Kembali membuang perubahan yang belum diterapkan dan kembali ke Main Menu.

### 11.10 Pengaturan dari Pause Menu

Jika Settings dibuka dari Pause Menu:

- Music Volume dapat diubah.
- SFX Volume dapat diubah.
- Mouse Sensitivity dapat diubah.
- Display Mode dapat diubah.
- Simulasi pertandingan tetap berhenti.
- Timer pertandingan tetap berhenti.
- Tombol Terapkan/Simpan menerapkan perubahan dan menyimpannya ke file TXT.
- Tombol Kembali membuang perubahan yang belum diterapkan dan kembali ke Pause Menu.
- Pemain tidak otomatis kembali ke pertandingan setelah keluar dari Settings.

### 11.11 Display Mode

Mode tampilan yang tersedia:

- Windowed.
- Fullscreen.

Ketentuan tampilan:

- Konten menggunakan koordinat logis dengan rasio 16:9.
- Windowed dapat di-resize tanpa meregangkan konten.
- Fullscreen menggunakan area layar yang tersedia.
- Jika rasio layar tidak sesuai 16:9, sistem menggunakan letterbox atau pillarbox.
- Konten tidak boleh terdistorsi akibat perubahan ukuran window.
- Posisi mouse dikonversi ke koordinat logis agar kontrol bidikan tetap akurat setelah resize.
- Mode tampilan dan ukuran window disimpan dalam pengaturan aplikasi.

### 11.12 Penyimpanan lokal

`StorageManager` bertanggung jawab membaca dan menulis:

- Pengaturan aplikasi.
- Riwayat pertandingan.

Penyimpanan menggunakan file TXT lokal. Proyek tidak menggunakan server, akun daring, atau database eksternal.
---

## 12. Arsitektur dan Keputusan Penggabungan Class

### 12.1 Baseline arsitektur

Arsitektur YouKnowBall mempertahankan tepat **14 class utama dan 8 struct pendukung**.

Keempat belas class utama menjadi fondasi rancangan OOP. Struct digunakan sebagai wadah data untuk menghubungkan komponen tanpa menambah kompleksitas class yang tidak diperlukan.

Penambahan atau pemisahan class maupun struct tidak dilakukan hanya untuk fungsi kecil yang masih dapat digabung secara wajar. Perubahan terhadap baseline harus memiliki alasan teknis yang jelas dan disepakati kelompok.

### 12.2 Daftar 14 class utama

| No. | Kelompok | Class | Tanggung jawab utama |
|---:|---|---|---|
| 1 | Pengelolaan aplikasi | `GameApp` | Mengelola window SFML, event loop, siklus aplikasi, dan koordinasi tingkat aplikasi. |
| 2 | Pengelolaan aplikasi | `ScreenManager` | Mengelola halaman aktif, navigasi, input antarmuka, serta delegasi update dan render. |
| 3 | Pertandingan | `MatchSession` | Mengelola siklus pertandingan, pemain aktif, controller, timer, pause, pergantian giliran, dan hasil. |
| 4 | Pemain | `Player` | Menyimpan identitas, kelompok bola, dan statistik pemain. |
| 5 | Pengendali pemain | `PlayerController` | Menyediakan kontrak umum bagi sumber perintah pukulan. |
| 6 | Pengendali pemain | `HumanController` | Mengolah input pemain manusia menjadi `ShotCommand`. |
| 7 | Pengendali pemain | `BotController` | Menjalankan strategi Bot Easy dan menghasilkan `ShotCommand`. |
| 8 | Objek permainan | `Table` | Mengelola kumpulan bola, pocket, geometri meja, dan validasi posisi. |
| 9 | Objek permainan | `Ball` | Menyimpan kondisi fisik satu bola. |
| 10 | Objek permainan | `Cue` | Mengelola arah, power, impuls pukulan, dan prediksi lintasan. |
| 11 | Simulasi | `PhysicsEngine` | Menghitung gerak, gesekan, tumbukan, pantulan cushion, dan deteksi pocket. |
| 12 | Aturan permainan | `GameRules` | Mengevaluasi aturan 8-Ball dan 9-Ball, foul, ball-in-hand, serta kondisi menang/kalah. |
| 13 | Penyimpanan | `StorageManager` | Membaca dan menulis pengaturan serta riwayat pertandingan melalui file TXT. |
| 14 | Audio | `AudioManager` | Mengelola musik, efek suara, dan volume audio. |

### 12.3 Pengelompokan class

Untuk memudahkan pembagian tanggung jawab, class dikelompokkan menjadi:

**A. Pengelolaan aplikasi**
- `GameApp`
- `ScreenManager`

**B. Pengelolaan pertandingan dan pemain**
- `MatchSession`
- `Player`

**C. Pengendali pemain**
- `PlayerController`
- `HumanController`
- `BotController`

**D. Objek permainan dan simulasi**
- `Table`
- `Ball`
- `Cue`
- `PhysicsEngine`

**E. Aturan permainan**
- `GameRules`

**F. Layanan aplikasi**
- `StorageManager`
- `AudioManager`

### 12.4 Keputusan penggabungan tanggung jawab

Beberapa keputusan desain berikut digunakan untuk menjaga jumlah class tetap terkendali.

| Kebutuhan | Keputusan desain |
|---|---|
| Pengelolaan halaman | Ditangani `ScreenManager`, tanpa membuat satu class utama untuk setiap halaman. |
| Pengelolaan pertandingan | Dipusatkan pada `MatchSession`. |
| Pengelolaan identitas pemain | Ditangani `Player`, bukan controller. |
| Input pemain manusia | Ditangani `HumanController`. |
| Strategi Bot | Ditangani `BotController`. |
| Kontrak pengendali pemain | Didefinisikan oleh `PlayerController`. |
| Pengelolaan bola dan pocket | Dipusatkan pada `Table` dan `Ball`. |
| Pengaturan arah dan power | Dikelola melalui `Cue`, dengan input diolah controller. |
| Perhitungan gerak dan tumbukan | Ditangani `PhysicsEngine`. |
| Evaluasi aturan | Ditangani `GameRules`. |
| Penyimpanan lokal | Ditangani `StorageManager`. |
| Pemutaran musik dan SFX | Ditangani `AudioManager`. |

### 12.5 Polimorfisme PlayerController

`PlayerController` merupakan abstract class yang menjadi kontrak umum bagi pengendali pemain.

Dua class yang mengimplementasikannya:

- `HumanController`
- `BotController`

Keduanya memiliki cara pengambilan keputusan yang berbeda, tetapi menghasilkan format perintah pukulan yang sama, yaitu `ShotCommand`.

Dengan demikian, `MatchSession` tidak perlu memiliki jalur simulasi terpisah untuk pemain manusia dan Bot.

Alur keduanya:

1. Controller memperbarui proses pengambilan keputusan.
2. Controller menyiapkan `ShotCommand`.
3. `MatchSession` mengambil perintah yang telah siap.
4. Perintah diproses melalui jalur pukulan yang sama.
5. `PhysicsEngine` menjalankan simulasi.
6. `GameRules` mengevaluasi hasil simulasi.

### 12.6 Batas tanggung jawab yang tidak boleh dilanggar

1. `Ball` tidak mendeteksi tumbukan atau menentukan foul.
2. `Table` tidak menjalankan simulasi fisika.
3. `PhysicsEngine` tidak menentukan pemenang, foul, atau pergantian giliran.
4. `GameRules` tidak menjalankan simulasi dan tidak menyimpan file.
5. `MatchSession` tidak menghitung rumus tumbukan atau membaca input mouse mentah.
6. `Player` tidak membaca input, menjalankan timer, atau menentukan pemenang.
7. `HumanController` tidak mengubah posisi bola secara langsung.
8. `BotController` tidak menjalankan mesin fisika sendiri.
9. `ScreenManager` tidak memiliki tanggung jawab untuk menghitung aturan biliar.
10. `StorageManager` tidak mengatur UI atau menentukan aturan pertandingan.
11. `AudioManager` tidak menentukan kapan sebuah kejadian permainan terjadi; komponen pemilik kejadian meminta audio diputar.

---

## 13. CRC dan Spesifikasi 14 Class

Bagian ini menjelaskan tanggung jawab setiap class melalui deskripsi, Knowing Responsibility, Doing Responsibility, atribut penting, kontrak method, dan collaborator.

Signature method mengikuti kontrak v03. Atribut penting merupakan informasi konseptual dari rancangan CRC v02 dan dapat disesuaikan secara teknis selama implementasi tanpa mengubah tanggung jawab class.

### 13.1 Kelompok A — Pengelolaan Aplikasi

#### 13.1.1 `GameApp`

**Deskripsi:**

Mengelola inisialisasi, window SFML, game loop, dan koordinasi layanan tingkat aplikasi.

**Responsibility:**

Mengelola siklus hidup dan jalannya aplikasi YouKnowBall.

**Knowing Responsibility:**
- Status aplikasi berjalan atau berhenti.
- Objek window dan waktu antar-frame.
- Pengaturan aplikasi yang sedang digunakan.
- Layanan tingkat aplikasi yang digunakan.

**Doing Responsibility:**
- Menginisialisasi window, aset, pengaturan, dan layanan aplikasi.
- Memuat pengaturan melalui `StorageManager`.
- Menjalankan game loop.
- Membaca event window.
- Meneruskan event antarmuka ke `ScreenManager`.
- Memanggil proses update dan render.
- Menerapkan perubahan display settings.
- Menutup aplikasi dan melepaskan resource.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `window` | `sf::RenderWindow` |
| `running` | `bool` |
| `frameClock` | `sf::Clock` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| Constructor | `GameApp()` | Menyiapkan keadaan awal aplikasi. |
| `initialize` | `bool initialize()` | Memuat `AppSettings` melalui `StorageManager`, membuat window sesuai mode tampilan, dan menginisialisasi komponen. Mengembalikan status keberhasilan. |
| `run` | `void run()` | Menjalankan loop event, update, dan render selama aplikasi aktif. |
| `processEvents` | `void processEvents()` | Membaca event window SFML dan meneruskan event antarmuka ke `ScreenManager`. |
| `update` | `void update(float deltaTime)` | Meminta komponen aktif melakukan update. Tidak menghitung fisika atau aturan sendiri. |
| `render` | `void render()` | Membersihkan window, memanggil render `ScreenManager`, lalu menampilkan frame. |
| `applyDisplaySettings` | `void applyDisplaySettings(const AppSettings& settings)` | Menerapkan Windowed/Fullscreen dan ukuran window, menjaga viewport 16:9 serta pemetaan koordinat. |
| `shutdown` | `void shutdown()` | Menyimpan pengaturan terakhir bila diperlukan dan melepaskan resource aplikasi. |

**Collaborator:**
- `ScreenManager`
- `StorageManager`
- `AudioManager`
- `MatchSession`

**Batas tanggung jawab:**

`GameApp` mengelola siklus aplikasi, bukan detail tampilan setiap halaman, aturan biliar, pergantian giliran, atau perhitungan fisika.

---

#### 13.1.2 `ScreenManager`

**Deskripsi:**

Mengelola layar aktif, perpindahan halaman, penerimaan event antarmuka, dan tampilan informasi aplikasi.

**Responsibility:**

Mengelola halaman aktif, navigasi, dan interaksi antarmuka aplikasi.

**Knowing Responsibility:**
- Jenis layar yang sedang aktif.
- Layar sebelumnya untuk kebutuhan navigasi kembali.
- Posisi pointer atau event antarmuka yang sedang diproses.
- Halaman atau komponen yang sedang menerima input.

**Doing Responsibility:**
- Berpindah antarhalaman.
- Menangani event UI.
- Meneruskan event ke halaman aktif atau controller yang relevan.
- Memperbarui elemen antarmuka.
- Menggambar halaman aktif.
- Membuka pengaturan pertandingan.
- Membuka pengaturan aplikasi.
- Membuka riwayat pertandingan.
- Membuka halaman How to Play.
- Mengembalikan pengguna ke halaman asal, termasuk kembali ke Pause apabila Settings dibuka dari Pause.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `currentScreen` | `ScreenType` |
| `previousScreen` | `ScreenType` |
| `mousePosition` | `sf::Vector2i` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `setScreen` | `void setScreen(ScreenType screen)` | Mengganti halaman aktif dan menyiapkan transisi halaman. |
| `getCurrentScreen` | `ScreenType getCurrentScreen() const` | Mengembalikan halaman yang sedang aktif. |
| `handleEvent` | `void handleEvent(const sf::Event& event)` | Meneruskan event ke halaman aktif atau controller yang relevan. |
| `update` | `void update(float deltaTime)` | Memperbarui halaman aktif dan sesi apabila halaman permainan sedang aktif. |
| `render` | `void render(sf::RenderTarget& target)` | Meminta halaman aktif menggambar elemen visual ke render target. |
| `setViewport` | `void setViewport(const sf::FloatRect& viewport)` | Memperbarui area render logis setelah ukuran window berubah. |
| `openMatchSetup` | `void openMatchSetup()` | Membuka halaman konfigurasi pertandingan. |
| `openSettings` | `void openSettings()` | Membuka halaman pengaturan aplikasi. |
| `openHistory` | `void openHistory()` | Membuka halaman riwayat pertandingan. |
| `openHowToPlay` | `void openHowToPlay()` | Membuka halaman petunjuk permainan. |

**Collaborator:**
- `GameApp`
- `MatchSession`
- `StorageManager`
- `AudioManager`

**Batas tanggung jawab:**

`ScreenManager` merupakan pengelola antarmuka. Komponen halaman menampilkan tombol, panel, teks, meja, HUD, dan dekorasi.

Tidak perlu membuat satu class utama baru untuk setiap halaman jika masih dapat dikelola secara wajar dalam struktur UI yang sudah ada.

---

### 13.2 Kelompok B — Pertandingan dan Pemain

#### 13.2.1 `MatchSession`

**Deskripsi:**

Mengelola satu sesi pertandingan dari inisialisasi rack sampai pertandingan selesai, termasuk konfigurasi, pemain, controller, giliran, timer, pause, restart, dan hasil.

**Responsibility:**

Mengelola konfigurasi, alur, giliran, timer, dan status pertandingan.

**Knowing Responsibility:**
- Konfigurasi pertandingan.
- Data dua pemain dan controller masing-masing.
- Pemain aktif dan status sesi.
- Sisa timer dan durasi aktif pertandingan.
- Kondisi sebelum pukulan.
- Hasil simulasi yang sedang diproses.
- Status penyimpanan hasil pertandingan.
- Fase pertandingan sebelumnya ketika Pause.

**Doing Responsibility:**
- Memulai pertandingan dan menyiapkan rack.
- Memvalidasi serta menerima perintah pukulan.
- Mengambil snapshot kondisi awal sebelum pukulan.
- Mengelola timer dan pergantian giliran.
- Memanggil simulasi fisika.
- Meminta evaluasi aturan setelah simulasi selesai.
- Menerapkan `RuleOutcome`.
- Mengelola ball-in-hand dan penempatan cue ball.
- Mengelola pause, resume, dan restart.
- Menyelesaikan pertandingan.
- Membentuk catatan hasil dan meminta penyimpanan satu kali.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `config` | `MatchConfig` |
| `state` | `MatchState` |
| `players` | `std::array<Player, 2>` |
| `controllers` | `std::array<std::unique_ptr<PlayerController>, 2>` |
| `currentPlayerIndex` | `int` |
| `remainingShotTime` | `float` |
| `activeDuration` | `float` |
| `isResultSaved` | `bool` |
| `table` | `Table` |
| `cue` | `Cue` |
| `physics` | `PhysicsEngine` |
| `rules` | `GameRules` |
| `shotStartState` | `ShotStartState` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `startMatch` | `bool startMatch(const MatchConfig& config)` | Memvalidasi konfigurasi dan menyiapkan pemain, controller, meja, giliran, timer, serta status pertandingan. |
| `update` | `void update(float deltaTime)` | Memperbarui fase pertandingan; memanggil fisika saat simulasi, evaluasi aturan saat bola berhenti, dan timer/controller saat giliran aktif. |
| `submitShot` | `void submitShot(const ShotCommand& command)` | Menyimpan snapshot awal, mengubah status ke simulasi, dan memulai pukulan. |
| `beginBallInHand` | `void beginBallInHand()` | Mengubah fase agar pemain dapat menempatkan cue ball. |
| `placeCueBall` | `bool placeCueBall(const sf::Vector2f& position)` | Meminta `Table` memvalidasi posisi dan menerapkan posisi hanya jika valid. |
| `pauseMatch` | `void pauseMatch()` | Menghentikan timer dan membatalkan input controller yang belum dikirim. |
| `resumeMatch` | `void resumeMatch()` | Melanjutkan fase sebelumnya dan sisa timer. |
| `restartMatch` | `void restartMatch()` | Mengatur ulang pertandingan menggunakan konfigurasi yang sama dan tidak menyimpan pertandingan yang dibatalkan. |
| `switchTurn` | `void switchTurn()` | Mengganti pemain aktif dan menyiapkan controller serta timer berikutnya. |
| `handleTimeout` | `void handleTimeout()` | Jika power sedang diatur, menjalankan pukulan menggunakan power saat itu. Jika tidak, memindahkan giliran tanpa foul dan tanpa ball-in-hand. |
| `finishMatch` | `void finishMatch(int winnerIndex)` | Mengakhiri pertandingan, menghentikan timer, membentuk record, dan meminta penyimpanan hasil. |
| `getActivePlayerIndex` | `int getActivePlayerIndex() const` | Mengembalikan indeks pemain aktif. |
| `getState` | `MatchState getState() const` | Mengembalikan fase pertandingan saat ini. |
| `getActivePlayer` | `const Player& getActivePlayer() const` | Memberikan data pemain aktif untuk UI atau evaluasi. |
| `getConfig` | `const MatchConfig& getConfig() const` | Mengembalikan konfigurasi pertandingan aktif. |

**Collaborator:**
- `Player`
- `PlayerController`
- `HumanController`
- `BotController`
- `Table`
- `Cue`
- `PhysicsEngine`
- `GameRules`
- `StorageManager`

**Batas tanggung jawab:**

`MatchSession` adalah koordinator alur pertandingan. Class ini tidak menghitung gerak bola, membaca mouse mentah, atau memutuskan aturan sendiri.

`MatchSession` menerima keputusan dari `GameRules` dan menerapkannya terhadap state pertandingan.

**Ketentuan snapshot pukulan:**

Setiap pukulan yang diterima harus mengambil `ShotStartState` tepat satu kali sebelum Cue menghitung impuls akhir dan sebelum impuls diberikan kepada cue ball.

Snapshot tersebut tidak boleh dibuat ulang hanya karena proses update berjalan beberapa frame atau pertandingan dilanjutkan dari fase jeda.

---

#### 13.2.2 `Player`

**Deskripsi:**

Menyimpan identitas, kelompok bola, dan statistik pemain selama satu pertandingan.

`Player` tidak menentukan input atau strategi pukulan.

**Responsibility:**

Menyimpan identitas, kelompok bola, dan statistik setiap pemain.

**Knowing Responsibility:**
- Nama pemain.
- Kelompok bola pada 8-Ball.
- Jumlah pukulan.
- Jumlah foul.
- Jumlah bola yang masuk.

**Doing Responsibility:**
- Mengatur nama pemain.
- Menetapkan kelompok bola.
- Mencatat bola yang masuk.
- Mencatat foul.
- Mengambil statistik pemain.
- Mengatur ulang statistik ketika pertandingan baru dimulai.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `name` | `std::string` |
| `ballGroup` | `BallGroup` |
| `shotCount` | `int` |
| `foulCount` | `int` |
| `pocketedBallCount` | `int` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| Constructor | `Player(const std::string& name)` | Membuat pemain dengan nama dan statistik awal. |
| `setName` | `void setName(const std::string& name)` | Mengubah nama pemain. |
| `getName` | `const std::string& getName() const` | Mengambil nama pemain. |
| `setBallGroup` | `void setBallGroup(BallGroup group)` | Menetapkan kelompok bola pemain. |
| `getBallGroup` | `BallGroup getBallGroup() const` | Mengambil kelompok bola pemain. |
| `addPocketedBall` | `void addPocketedBall(int ballNumber)` | Memperbarui statistik bola masuk. |
| `addFoul` | `void addFoul()` | Menambah jumlah foul pemain. |
| `getPocketedCount` | `int getPocketedCount() const` | Mengambil jumlah bola yang masuk. |
| `getFoulCount` | `int getFoulCount() const` | Mengambil jumlah foul. |
| `resetStats` | `void resetStats()` | Mengatur ulang statistik pemain. |

**Collaborator:**
- `MatchSession`
- `GameRules`

**Batas tanggung jawab:**

`Player` hanya menyimpan identitas, kelompok, dan statistik. Class ini tidak membaca input, mengelola timer, atau menentukan pemenang.

---

### 13.3 Kelompok C — Pengendali Pemain

#### 13.3.1 `PlayerController` (abstract)

**Deskripsi:**

Menetapkan kontrak umum bagi sumber keputusan pemain agar sistem pertandingan menggunakan jalur penerimaan pukulan yang sama untuk manusia dan Bot.

**Responsibility:**

Menyediakan kontrak dasar bagi pengendali tindakan pemain.

**Knowing Responsibility:**
- Kontrak operasi yang harus dimiliki setiap controller.
- Status proses pengambilan keputusan.
- Status perintah pukulan yang siap dikirim.
- Status input atau perintah yang dapat dibatalkan.

**Doing Responsibility:**
- Menyediakan kontrak update controller.
- Menyediakan pemeriksaan kesiapan `ShotCommand`.
- Menyediakan mekanisme pengambilan perintah pukulan.
- Menyediakan mekanisme pembatalan input atau perintah tertunda.
- Memungkinkan polimorfisme antara `HumanController` dan `BotController`.

**Atribut penting:**

Tidak menetapkan atribut data khusus pada baseline. Detail status input dan keputusan berada pada class turunan.

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `update` | `virtual void update(float deltaTime) = 0` | Memperbarui proses pengambilan keputusan controller. |
| `hasShotCommand` | `virtual bool hasShotCommand() const = 0` | Memeriksa apakah perintah pukulan siap dikirim. |
| `consumeShotCommand` | `virtual ShotCommand consumeShotCommand() = 0` | Mengambil satu perintah pukulan dan mengosongkan status siap. |
| `cancelPendingInput` | `virtual void cancelPendingInput() = 0` | Membatalkan input atau perintah yang belum dikirim. |
| Destructor | `virtual ~PlayerController() = default` | Menyediakan destructor virtual untuk penggunaan polimorfisme. |

**Collaborator:**
- `HumanController`
- `BotController`
- `MatchSession`

**Batas tanggung jawab:**

`PlayerController` tidak mengetahui detail input manusia maupun strategi Bot. Detail tersebut ditangani oleh class turunan.

---

#### 13.3.2 `HumanController`

**Deskripsi:**

Menerjemahkan input mouse dan keyboard pemain manusia menjadi keputusan arah serta kekuatan pukulan.

**Responsibility:**

Mengolah input pemain manusia menjadi `ShotCommand`.

**Knowing Responsibility:**
- Status proses drag.
- Posisi mouse dalam koordinat logis.
- Sensitivitas kontrol.
- Arah bidikan yang sedang dipilih.
- Power yang sedang diatur.
- Status kesiapan perintah pukulan.

**Doing Responsibility:**
- Membaca input mouse dan keyboard.
- Mengatur arah bidikan melalui `Cue`.
- Mengatur power melalui indikator yang terpisah dari kontrol arah.
- Mengunci arah selama power diatur.
- Membatalkan drag dan perintah yang belum dikirim.
- Menghasilkan `ShotCommand` ketika input dilepas secara sah.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `isDragging` | `bool` |
| `dragStartPosition` | `sf::Vector2f` |
| `currentMousePosition` | `sf::Vector2f` |
| `dragSensitivity` | `float` |
| `currentDirection` | `sf::Vector2f` |
| `currentPower` | `float` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `handleEvent` | `void handleEvent(const sf::Event& event, const sf::Vector2f& logicalMousePosition)` | Membaca input mouse/keyboard dalam koordinat logis dan memperbarui arah atau power melalui `Cue`. |
| `update` | `void update(float deltaTime)` | Memperbarui status input dan kesiapan perintah pukulan. |
| `hasShotCommand` | `bool hasShotCommand() const` | Memeriksa apakah perintah pukulan siap dikirim. |
| `consumeShotCommand` | `ShotCommand consumeShotCommand()` | Mengambil satu perintah pukulan yang telah siap. |
| `cancelPendingInput` | `void cancelPendingInput()` | Membatalkan drag dan perintah yang belum dikirim. |
| `setCue` | `void setCue(Cue* cue)` | Menghubungkan controller ke Cue yang digunakan. |

**Collaborator:**
- `PlayerController`
- `MatchSession`
- `Cue`
- `Table`

**Ketentuan input:**

Konversi koordinat piksel ke koordinat logis dilakukan oleh lapisan window/aplikasi sebelum event diteruskan kepada controller.

`HumanController` tidak mengubah posisi bola dan tidak menjalankan fisika secara langsung.

---

#### 13.3.3 `BotController`

**Deskripsi:**

Menghasilkan keputusan pukulan Bot Easy menggunakan heuristik sederhana berdasarkan target sah, posisi bola, pocket, arah, dan kekuatan.

**Responsibility:**

Menentukan strategi dan menghasilkan perintah pukulan untuk Bot Easy.

**Knowing Responsibility:**
- Target bola legal.
- Posisi bola pada meja.
- Pilihan pocket.
- Kandidat arah dan power.
- Jenis permainan aktif.
- Informasi pemain Bot.
- Status proses pengambilan keputusan.

**Doing Responsibility:**
- Memeriksa giliran Bot.
- Memilih target legal.
- Memilih pocket tujuan.
- Menentukan arah dan kekuatan pukulan.
- Menghasilkan `ShotCommand`.
- Membatalkan perintah yang belum dikirim.
- Menyediakan konteks meja, pemain, dan mode permainan yang dibutuhkan Bot.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `targetBallNumber` | `int` |
| `targetPocketId` | `int` |
| `candidateDirection` | `sf::Vector2f` |
| `candidatePower` | `float` |
| `isThinking` | `bool` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `update` | `void update(float deltaTime)` | Memeriksa giliran Bot dan menyiapkan perintah jika belum tersedia. |
| `chooseShot` | `ShotCommand chooseShot(const Table& table, const Player& bot, GameType gameType) const` | Memilih target, arah, dan power sederhana berdasarkan keadaan meja. |
| `hasShotCommand` | `bool hasShotCommand() const` | Memeriksa apakah perintah pukulan siap dikirim. |
| `consumeShotCommand` | `ShotCommand consumeShotCommand()` | Mengambil satu perintah dan mengosongkan status siap. |
| `cancelPendingInput` | `void cancelPendingInput()` | Menghapus perintah yang masih tertunda. |
| `setContext` | `void setContext(const Table* table, const Player* bot, GameType gameType)` | Memberikan konteks baca yang diperlukan Bot. |

**Collaborator:**
- `PlayerController`
- `MatchSession`
- `Table`
- `Player`
- `GameRules`
- `Cue`

**Batas AI:**

Bot Easy menggunakan strategi sederhana. Bot tidak mempunyai simulasi fisika terpisah dan tidak dijamin selalu menghasilkan pot yang berhasil.

Setiap pukulan Bot tetap melewati jalur yang sama dengan pemain manusia, yaitu `ShotCommand`, `MatchSession`, `PhysicsEngine`, dan `GameRules`.

---

### 13.4 Kelompok D — Objek Permainan dan Simulasi

#### 13.4.1 `Table`

**Deskripsi:**

Menyimpan area bermain, kumpulan bola, enam data pocket, dan geometri meja serta memvalidasi posisi bola.

**Responsibility:**

Mengelola area permainan, bola, pocket, dan validasi posisi bola.

**Knowing Responsibility:**
- Batas area bermain.
- Kumpulan bola yang berada di meja.
- Data enam pocket.
- Posisi cue ball dan object ball.
- Status bola yang masih aktif atau sudah masuk pocket.

**Doing Responsibility:**
- Menyiapkan geometri dan susunan bola sesuai jenis permainan.
- Menyediakan akses ke bola dan pocket.
- Mengambil bola berdasarkan nomor.
- Memeriksa apakah posisi berada di dalam area permainan.
- Memvalidasi penempatan cue ball.
- Mengatur posisi cue ball setelah validasi.
- Mengatur ulang susunan bola.
- Mengembalikan bola ke meja melalui proses respot.
- Memeriksa apakah seluruh bola berhenti.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `playingArea` | `sf::FloatRect` |
| `balls` | `std::vector<Ball>` |
| `pockets` | `std::vector<PocketData>` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `initialize` | `void initialize(GameType gameType)` | Menyiapkan geometri, pocket, dan susunan bola awal. |
| `getBall` | `Ball* getBall(int ballNumber)` | Mengambil bola berdasarkan nomor atau mengembalikan `nullptr` jika tidak ditemukan. |
| `getBall` | `const Ball* getBall(int ballNumber) const` | Mengambil bola berdasarkan nomor dalam akses baca-saja. |
| `getBalls` | `std::vector<Ball>& getBalls()` | Memberikan akses perubahan internal untuk sistem fisika. |
| `getBalls` | `const std::vector<Ball>& getBalls() const` | Memberikan akses baca-saja terhadap kumpulan bola. |
| `getPockets` | `const std::vector<PocketData>& getPockets() const` | Mengambil data pocket. |
| `isInsidePlayableArea` | `bool isInsidePlayableArea(const sf::Vector2f& position) const` | Memeriksa apakah titik berada dalam area permainan. |
| `canPlaceCueBall` | `bool canPlaceCueBall(const sf::Vector2f& position) const` | Memeriksa batas meja, overlap dengan bola aktif, dan area pocket. |
| `setCueBallPosition` | `void setCueBallPosition(const sf::Vector2f& position)` | Mengubah posisi cue ball setelah validasi. |
| `resetBalls` | `void resetBalls(GameType gameType)` | Mengatur ulang susunan bola berdasarkan jenis permainan. |
| `respotBall` | `void respotBall(int ballNumber)` | Mengembalikan bola tertentu ke posisi spot yang ditentukan. |
| `areAllBallsStopped` | `bool areAllBallsStopped() const` | Memeriksa apakah seluruh bola telah berhenti. |

**Collaborator:**
- `Ball`
- `PhysicsEngine`
- `GameRules`
- `BotController`
- `PocketData`

**Batas tanggung jawab:**

`Table` menyimpan objek permainan dan memvalidasi geometri. Class ini tidak menjalankan simulasi fisika dan tidak menentukan aturan permainan.

---

#### 13.4.2 `Ball`

**Deskripsi:**

Menyimpan keadaan fisik satu bola dan menyediakan operasi untuk mengubah posisi, kecepatan, serta statusnya.

**Responsibility:**

Menyimpan dan mengelola kondisi fisik setiap bola selama permainan.

**Knowing Responsibility:**
- Nomor bola.
- Posisi bola.
- Kecepatan bola.
- Radius bola.
- Status bola masih berada di meja atau sudah masuk pocket.

**Doing Responsibility:**
- Mengatur posisi bola.
- Mengatur kecepatan bola.
- Menerima impuls.
- Memperbarui posisi berdasarkan waktu.
- Menghentikan bola.
- Memeriksa apakah bola sedang bergerak.
- Mengatur status pocket.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `number` | `int` |
| `position` | `sf::Vector2f` |
| `velocity` | `sf::Vector2f` |
| `radius` | `float` |
| `isPocketed` | `bool` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| Constructor | `Ball(int number, const sf::Vector2f& position, float radius)` | Membuat bola dengan nomor, posisi, dan radius. |
| `setPosition` | `void setPosition(const sf::Vector2f& position)` | Mengubah posisi bola. |
| `getPosition` | `const sf::Vector2f& getPosition() const` | Mengambil posisi bola. |
| `setVelocity` | `void setVelocity(const sf::Vector2f& velocity)` | Mengubah kecepatan bola. |
| `getVelocity` | `const sf::Vector2f& getVelocity() const` | Mengambil kecepatan bola. |
| `applyImpulse` | `void applyImpulse(const sf::Vector2f& impulse)` | Menambahkan impuls pada kecepatan sesuai parameter fisika. |
| `updatePosition` | `void updatePosition(float deltaTime)` | Memperbarui posisi; dipanggil oleh `PhysicsEngine`. |
| `stop` | `void stop()` | Mengatur kecepatan menjadi nol. |
| `isMoving` | `bool isMoving() const` | Memeriksa kecepatan terhadap ambang berhenti. |
| `setPocketed` | `void setPocketed(bool pocketed)` | Mengatur status pocket bola. |
| `isPocketed` | `bool isPocketed() const` | Mengambil status pocket bola. |
| `getNumber` | `int getNumber() const` | Mengambil nomor bola. |
| `getRadius` | `float getRadius() const` | Mengambil radius bola. |

**Collaborator:**
- `Table`
- `PhysicsEngine`
- `Cue`

**Batas tanggung jawab:**

`Ball` hanya mengelola keadaan satu bola. Class ini tidak mendeteksi tumbukan, pocket, foul, atau kemenangan.

---

#### 13.4.3 `Cue`

**Deskripsi:**

Mengelola informasi bidikan, arah, power, dan impuls pukulan. Cue juga menyediakan prediksi lintasan sederhana sebagai bantuan visual.

**Responsibility:**

Mengelola arah, kekuatan, impuls pukulan, dan prediksi lintasan bola.

**Knowing Responsibility:**
- Arah bidikan.
- Sudut bidikan.
- Nilai power.
- Batas power yang diperbolehkan.
- Parameter untuk menghitung impuls.
- Informasi meja yang diperlukan untuk prediksi lintasan.

**Doing Responsibility:**
- Menyimpan arah bidikan yang telah dinormalisasi.
- Mengatur power dalam rentang valid.
- Menghitung vektor impuls dari arah dan power.
- Menghasilkan prediksi lintasan cue ball hingga tumbukan pertama.
- Menghasilkan perkiraan arah awal object ball setelah tumbukan.
- Mengatur ulang status bidikan setelah pukulan atau pembatalan.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `angleRadians` | `float` |
| `pullDistance` | `float` |
| `maxPullDistance` | `float` |
| `power` | `float` |
| `aimDirection` | `sf::Vector2f` |
| `aimLineLength` | `float` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `setAimDirection` | `void setAimDirection(const sf::Vector2f& direction)` | Menyimpan arah bidikan yang telah dinormalisasi. |
| `getAimDirection` | `const sf::Vector2f& getAimDirection() const` | Mengambil arah bidikan. |
| `setPower` | `void setPower(float power)` | Mengatur power dalam rentang valid. |
| `getPower` | `float getPower() const` | Mengambil nilai power. |
| `calculateImpulse` | `sf::Vector2f calculateImpulse() const` | Menghitung vektor impuls dari arah dan power. |
| `predictTrajectory` | `std::vector<sf::Vector2f> predictTrajectory(const Table& table) const` | Menghasilkan garis prediksi tumbukan pertama dan arah awal object ball tanpa mengubah keadaan meja. |
| `reset` | `void reset()` | Mengatur ulang status arah dan power setelah pukulan atau pembatalan. |

**Collaborator:**
- `HumanController`
- `BotController`
- `Ball`
- `Table`
- `PhysicsEngine`

**Batas tanggung jawab:**

`Cue` tidak membaca event secara langsung dan tidak menentukan apakah pemain boleh memukul. Keputusan penerimaan pukulan berada pada controller dan `MatchSession`.

Prediksi lintasan tidak menggantikan perhitungan fisika sebenarnya.

---

#### 13.4.4 `PhysicsEngine`

**Deskripsi:**

Menghitung perubahan fisik bola dan mencatat fakta kejadian selama satu pukulan.

**Responsibility:**

Menangani simulasi pergerakan bola, tumbukan, pantulan cushion, gesekan, dan deteksi pocket.

**Knowing Responsibility:**
- Parameter gesekan.
- Parameter restitusi atau pantulan.
- Ambang kecepatan untuk menentukan bola berhenti.
- Interval pembaruan simulasi.
- Keadaan meja dan bola selama simulasi.
- Catatan kejadian fisik pada pukulan aktif.

**Doing Responsibility:**
- Memulai pencatatan kejadian pukulan baru.
- Memberikan impuls awal kepada cue ball.
- Memperbarui pergerakan bola.
- Menghitung perlambatan akibat gesekan.
- Menangani tumbukan antarb bola.
- Menangani pantulan pada cushion.
- Mendeteksi bola yang masuk pocket.
- Mencatat bola pertama yang terkena.
- Mencatat bola yang masuk pocket.
- Mencatat scratch dan kontak cushion yang relevan sebagai fakta.
- Memeriksa apakah seluruh bola sudah berhenti.
- Menghasilkan `ShotResult`.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `frictionCoefficient` | `float` |
| `restitution` | `float` |
| `stopThreshold` | `float` |
| `substepDuration` | `float` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `beginShot` | `void beginShot()` | Mengosongkan catatan kejadian untuk pukulan baru. |
| `applyCueImpulse` | `void applyCueImpulse(Ball& cueBall, const sf::Vector2f& impulse)` | Memberikan impuls awal kepada cue ball. |
| `update` | `void update(Table& table, float deltaTime)` | Memperbarui gerak, gesekan, tumbukan, cushion, dan deteksi pocket untuk satu langkah simulasi. |
| `resolveBallCollisions` | `void resolveBallCollisions(Table& table)` | Menyelesaikan tumbukan antarb bola dan mencatat kontak. |
| `resolveCushionCollisions` | `void resolveCushionCollisions(Table& table)` | Menyelesaikan pantulan cushion dan mencatat kontak. |
| `detectPocketedBalls` | `void detectPocketedBalls(Table& table)` | Menandai bola yang masuk pocket dan mencatat nomornya. |
| `areAllBallsStopped` | `bool areAllBallsStopped(const Table& table) const` | Memeriksa apakah seluruh bola telah berhenti. |
| `getShotResult` | `ShotResult getShotResult() const` | Mengembalikan fakta yang tercatat selama pukulan. |

**Collaborator:**
- `Table`
- `Ball`
- `ShotResult`

**Fakta yang dicatat:**

Fakta fisik yang dibutuhkan untuk evaluasi aturan meliputi:

- Nomor bola pertama yang terkena cue ball.
- Daftar bola yang masuk pocket.
- Apakah cue ball masuk pocket.
- Apakah terdapat kontak cushion yang relevan setelah kontak bola.
- Apakah bola 8 masuk pocket.
- Apakah bola 9 masuk pocket.

**Batas tanggung jawab:**

`PhysicsEngine` hanya melaporkan fakta fisik. Class ini tidak menyimpulkan foul, kemenangan, ball-in-hand, atau pergantian giliran.

Keputusan tersebut menjadi tanggung jawab `GameRules` dan diterapkan oleh `MatchSession`.

---

### 13.5 Kelompok E — Aturan Permainan

#### 13.5.1 `GameRules`

**Deskripsi:**

Mengelola evaluasi aturan kedua jenis permainan berdasarkan `GameType`, termasuk target legal, kelompok bola, foul, scratch, ball-in-hand, respot, dan kondisi kemenangan.

**Responsibility:**

Mengevaluasi hasil pukulan berdasarkan aturan 8-Ball dan 9-Ball.

**Knowing Responsibility:**
- Jenis permainan aktif.
- Status open table pada 8-Ball.
- Kelompok bola setiap pemain.
- Target legal.
- Snapshot keadaan sebelum pukulan.
- Fakta hasil simulasi.
- Kondisi meja setelah simulasi.
- Status kelompok pemain dan bola yang telah diselesaikan.

**Doing Responsibility:**
- Memeriksa kontak pertama sesuai mode permainan.
- Menentukan foul berdasarkan fakta dan aturan yang diterapkan.
- Menentukan kelompok bola pada 8-Ball.
- Menentukan bola aktif terendah pada 9-Ball.
- Mengevaluasi kondisi kemenangan.
- Menentukan apakah giliran dipertahankan atau berpindah.
- Menentukan hak ball-in-hand.
- Menentukan bola yang harus dikembalikan ke meja.
- Menghasilkan `RuleOutcome`.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `gameType` | `GameType` |
| `tableOpen` | `bool` |
| `chosenPocketId` | `int` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `evaluateShot` | `RuleOutcome evaluateShot(GameType gameType, const ShotStartState& startState, const ShotResult& result, const Table& table, const Player& shooter, const Player& opponent) const` | Mengevaluasi satu pukulan dan mengembalikan keputusan aturan. |
| `isLegalFirstContact` | `bool isLegalFirstContact(GameType gameType, const ShotStartState& startState, const ShotResult& result, const Player& shooter) const` | Memeriksa kontak pertama sesuai jenis permainan dan kelompok pemain. |
| `isFoul` | `bool isFoul(const ShotResult& result, const ShotStartState& startState, GameType gameType, const Player& shooter) const` | Menilai foul yang termasuk dalam implementasi proyek. |
| `determineGroup` | `BallGroup determineGroup(const ShotResult& result) const` | Mengembalikan SOLID atau STRIPE hanya jika satu kelompok tunggal dapat ditentukan; selain itu NONE. |
| `getLowestActiveBall` | `int getLowestActiveBall(const Table& table) const` | Mengambil nomor bola aktif terendah untuk 9-Ball. |
| `isEightBallWin` | `bool isEightBallWin(const ShotResult& result, const Player& shooter, const Table& table) const` | Memeriksa kondisi menang/kalah 8-Ball berdasarkan status kelompok dan bola 8. |
| `isNineBallWin` | `bool isNineBallWin(const ShotResult& result, const Table& table) const` | Memeriksa kemenangan 9-Ball yang sah. |
| `requiresBallInHand` | `bool requiresBallInHand(const RuleOutcome& outcome) const` | Memeriksa apakah hasil evaluasi memberikan hak ball-in-hand. |

**Collaborator:**
- `MatchSession`
- `Player`
- `Table`
- `ShotStartState`
- `ShotResult`
- `RuleOutcome`

**Batas tanggung jawab:**

`GameRules` mengevaluasi fakta dan keadaan permainan. Class ini tidak:

- Menjalankan simulasi fisika.
- Mengubah posisi bola secara langsung.
- Mengganti pemain aktif secara langsung.
- Menjalankan timer.
- Menyimpan hasil pertandingan ke file.

`GameRules` mengembalikan `RuleOutcome`, kemudian `MatchSession` menerapkan hasil tersebut.

**Catatan aturan 8-Ball:**

Penentuan kelompok harus mengikuti keputusan final proyek:

- Meja awalnya terbuka.
- Kelompok belum ditentukan.
- Kelompok ditentukan ketika satu pukulan sah memasukkan bola dari satu kelompok saja.
- Jika Solid dan Stripe masuk bersamaan ketika meja terbuka, kelompok tetap belum ditentukan.
- Kelompok baru ditentukan pada pukulan berikutnya yang secara sah memasukkan bola dari satu kelompok saja.

**Catatan aturan 9-Ball:**

Kontak pertama harus mengenai bola aktif bernomor terendah. Kemenangan hanya diberikan ketika bola 9 masuk secara sah.

---

### 13.6 Kelompok F — Penyimpanan dan Audio

#### 13.6.1 `StorageManager`

**Deskripsi:**

Menangani pembacaan dan penyimpanan pengaturan aplikasi serta riwayat pertandingan menggunakan file teks lokal.

**Responsibility:**

Mengelola penyimpanan dan pemuatan pengaturan serta riwayat pertandingan lokal.

**Knowing Responsibility:**
- Lokasi file pengaturan.
- Lokasi file riwayat.
- Pengaturan aplikasi yang sedang digunakan.
- Kumpulan catatan pertandingan yang telah dibaca.

**Doing Responsibility:**
- Memuat pengaturan ketika aplikasi dimulai.
- Menyimpan perubahan pengaturan.
- Memuat riwayat pertandingan.
- Menambahkan catatan pertandingan yang telah selesai.
- Menyediakan data riwayat untuk ditampilkan.
- Menangani file yang tidak tersedia atau tidak dapat dibaca.
- Mencegah satu hasil pertandingan tersimpan lebih dari sekali.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `settingsFilePath` | `std::string` |
| `historyFilePath` | `std::string` |
| `cachedSettings` | `AppSettings` |
| `historyRecords` | `std::vector<MatchRecord>` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `loadSettings` | `bool loadSettings(AppSettings& settings)` | Membaca pengaturan. Jika file tidak tersedia atau rusak, mengisi nilai default. |
| `saveSettings` | `bool saveSettings(const AppSettings& settings)` | Menulis pengaturan ke file TXT. |
| `saveMatchRecord` | `bool saveMatchRecord(const MatchRecord& record)` | Menambahkan hasil pertandingan selesai ke riwayat. |
| `loadMatchHistory` | `std::vector<MatchRecord> loadMatchHistory() const` | Membaca record riwayat yang valid. |
| `deleteMatchRecord` | `bool deleteMatchRecord(int recordId)` | Opsional; hanya dibuat jika fitur hapus satu record disediakan pada UI. |
| `clearMatchHistory` | `bool clearMatchHistory()` | Opsional; hanya dibuat jika fitur hapus seluruh riwayat disediakan dan dikonfirmasi. |

**Collaborator:**
- `GameApp`
- `ScreenManager`
- `MatchSession`
- `AppSettings`
- `MatchRecord`

**Batas tanggung jawab:**

`StorageManager` hanya menangani baca dan tulis data lokal. Class ini tidak mengatur tampilan antarmuka atau menentukan aturan permainan.

File yang tidak tersedia atau rusak tidak boleh menyebabkan aplikasi langsung crash.

---

#### 13.6.2 `AudioManager`

**Deskripsi:**

Mengelola musik latar, efek suara, dan volume audio aplikasi.

**Responsibility:**

Mengelola pemutaran musik dan efek suara dalam aplikasi.

**Knowing Responsibility:**
- Sumber musik latar.
- Buffer efek suara.
- Volume musik.
- Volume SFX.
- Jenis efek suara yang tersedia.

**Doing Responsibility:**
- Menginisialisasi resource audio.
- Memuat musik dan efek suara.
- Memutar dan menghentikan musik.
- Memutar efek suara berdasarkan jenis kejadian.
- Mengatur volume musik.
- Mengatur volume SFX.
- Menerapkan pengaturan audio aplikasi.

**Atribut penting:**

| Atribut | Tipe |
|---|---|
| `backgroundMusic` | `sf::Music` |
| `soundBuffers` | `std::map<SoundType, sf::SoundBuffer>` |
| `activeSounds` | `std::vector<sf::Sound>` atau pengelolaan setara |
| `musicVolume` | `float` |
| `sfxVolume` | `float` |

**Kontrak method:**

| Method | Signature | Kontrak |
|---|---|---|
| `initialize` | `bool initialize()` | Memuat resource audio dan menyiapkan pengelola audio. |
| `playMusic` | `void playMusic()` | Memulai pemutaran musik latar. |
| `stopMusic` | `void stopMusic()` | Menghentikan musik latar. |
| `setMusicVolume` | `void setMusicVolume(float volume)` | Mengatur volume musik. |
| `setSfxVolume` | `void setSfxVolume(float volume)` | Mengatur volume efek suara. |
| `playSfx` | `void playSfx(SoundType sound)` | Memutar efek suara sesuai jenis kejadian. |
| `applySettings` | `void applySettings(const AppSettings& settings)` | Menerapkan volume musik dan SFX dari pengaturan aplikasi. |

**Collaborator:**
- `GameApp`
- `ScreenManager`
- `StorageManager`
- Komponen permainan yang meminta efek suara.

**Batas tanggung jawab:**

`AudioManager` mengelola pemutaran audio. Class ini tidak menentukan kapan kejadian permainan berlangsung atau menentukan hasil aturan.
---

## 14. Delapan Struct Pendukung

Struct merupakan wadah data pendukung dan tidak dihitung sebagai class utama. Delapan struct berikut digunakan untuk membawa data antarkomponen agar tanggung jawab setiap class tetap terpisah.

Struct tidak perlu memiliki method khusus. Atribut dan representasi internal dapat disesuaikan ketika implementasi dilakukan, selama fungsi datanya tetap konsisten dengan kontrak proyek.

### 14.1 `MatchConfig`

Menyimpan konfigurasi pertandingan sebelum sesi dimulai.

Data yang dicakup:
- Jenis permainan: 8-Ball atau 9-Ball.
- Jenis lawan: pemain lokal kedua atau Bot Easy.
- Nama pemain.
- Batas waktu per giliran.
- Status penggunaan timer tanpa batas.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `gameType` | `GameType` |
| `opponentType` | `OpponentType` |
| `playerNames` | `std::array<std::string, 2>` |
| `timeLimitSeconds` | `int` |
| `unlimitedTime` | `bool` |

### 14.2 `AppSettings`

Menyimpan pengaturan aplikasi yang berlaku lintas pertandingan dan dimuat ketika aplikasi dijalankan.

Data yang dicakup:
- Volume musik.
- Volume efek suara.
- Sensitivitas mouse.
- Mode tampilan Windowed atau Fullscreen.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `musicVolume` | `float` |
| `sfxVolume` | `float` |
| `mouseSensitivity` | `float` |
| `displayMode` | `DisplayMode` |

Pengaturan disimpan secara lokal menggunakan file TXT melalui `StorageManager`.

Perubahan pengaturan dari halaman Settings dapat diterapkan dan disimpan melalui tombol Terapkan/Simpan. Jika pengguna memilih Kembali sebelum menerapkan perubahan, perubahan yang belum diterapkan dibuang.

### 14.3 `MatchRecord`

Menyimpan ringkasan pertandingan yang telah selesai. Data digunakan untuk halaman Result dan Match History.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `matchId` | `int` atau identifier setara |
| `dateTime` | `std::string` |
| `gameType` | `GameType` |
| `opponentType` | `OpponentType` |
| `playerNames` | `std::array<std::string, 2>` |
| `winnerName` | `std::string` |
| `winReason` | `std::string` atau enum yang disepakati |
| `pocketedCounts` | `std::array<int, 2>` |
| `foulCounts` | `std::array<int, 2>` |
| `shotCounts` | `std::array<int, 2>` |
| `activeDurationSeconds` | `float` |
| `timeLimitSeconds` | `int` |

Hanya pertandingan yang selesai secara normal yang disimpan ke riwayat.

Pertandingan yang dibatalkan melalui Restart atau Main Menu dari Pause tidak menghasilkan `MatchRecord`.

### 14.4 `PocketData`

Menyimpan informasi posisi dan area deteksi satu pocket. Enam data pocket digunakan oleh `Table`.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `pocketID` | `int` |
| `centerPosition` | `sf::Vector2f` |
| `captureRadius` | `float` |

### 14.5 `ShotCommand`

Mewakili perintah pukulan yang dihasilkan oleh `HumanController` atau `BotController`.

Struct ini menjadi format perintah yang sama bagi kedua jenis controller.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `direction` | `sf::Vector2f` |
| `power` | `float` |
| `isValid` | `bool` |

`ShotCommand` tidak menjalankan pukulan sendiri. Perintah harus diterima dan diproses oleh `MatchSession`.

### 14.6 `ShotStartState`

Menyimpan snapshot kondisi penting sebelum impuls pukulan diberikan.

Snapshot diperlukan agar `GameRules` dapat mengevaluasi hasil berdasarkan kondisi yang benar-benar berlaku sebelum simulasi dimulai.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `legalTargets` | `std::vector<int>` |
| `tableOpen` | `bool` |
| `activePlayerIndex` | `int` |
| `isBreakShot` | `bool` |

Snapshot diambil satu kali untuk setiap pukulan yang diterima.

Snapshot tidak boleh dibuat ulang selama simulasi berjalan, ketika proses update berlangsung beberapa frame, atau ketika aplikasi melanjutkan sesi dari Pause.

### 14.7 `ShotResult`

Menyimpan fakta fisik yang terjadi selama simulasi satu pukulan.

Struct ini menjadi keluaran pencatatan kejadian dari `PhysicsEngine`, bukan tempat untuk menentukan foul atau kemenangan.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `firstHitBallNumber` | `int` |
| `pocketedBallNumbers` | `std::vector<int>` |
| `cueBallPocketed` | `bool` |
| `cushionAfterFirstContact` | `bool` |
| `numberedBallsHitCushionOnBreak` | `int` atau data setara |

Data yang benar-benar dicatat harus sesuai dengan kebutuhan evaluasi aturan yang diterapkan dalam proyek.

### 14.8 `RuleOutcome`

Menyimpan keputusan yang dihasilkan `GameRules` setelah seluruh bola berhenti dan hasil pukulan dievaluasi.

Atribut penting:

| Atribut | Tipe konseptual |
|---|---|
| `isFoul` | `bool` |
| `foulType` | `FoulType` |
| `retainTurn` | `bool` |
| `ballInHand` | `bool` |
| `matchFinished` | `bool` |
| `winnerIndex` | `int` |
| `ballsToSpot` | `std::vector<int>` |

`RuleOutcome` menjadi hasil evaluasi yang diterima `MatchSession`. `MatchSession` bertanggung jawab menerapkan keputusan tersebut ke dalam status pertandingan.

---

## 15. Enumerasi Pendukung

Enumerasi digunakan untuk membatasi pilihan status dan kategori agar tidak bergantung pada angka atau string bebas.

Enum bukan class atau struct tambahan dan tidak mengubah baseline 14 class serta 8 struct.

### 15.1 `GameType`

Menentukan jenis permainan yang sedang dijalankan.

| Nilai | Keterangan |
|---|---|
| `EIGHT_BALL` | Permainan 8-Ball. |
| `NINE_BALL` | Permainan 9-Ball. |

### 15.2 `OpponentType`

Menentukan jenis lawan dalam pertandingan.

| Nilai | Keterangan |
|---|---|
| `LOCAL_PLAYER` | Dua pemain bermain secara lokal pada satu perangkat. |
| `BOT` | Pemain manusia melawan Bot Easy. |

### 15.3 `DisplayMode`

Menentukan mode tampilan aplikasi.

| Nilai | Keterangan |
|---|---|
| `WINDOWED` | Aplikasi berjalan dalam window yang dapat diubah ukurannya. |
| `FULLSCREEN` | Aplikasi berjalan dalam mode layar penuh. |

### 15.4 `ScreenType`

Menentukan halaman antarmuka yang sedang aktif.

| Nilai | Keterangan |
|---|---|
| `MAIN_MENU` | Halaman utama. |
| `MATCH_SETUP` | Konfigurasi pertandingan. |
| `GAME` | Halaman permainan aktif. |
| `PAUSE` | Menu jeda pertandingan. |
| `RESULT` | Hasil pertandingan. |
| `HISTORY` | Daftar dan detail riwayat pertandingan. |
| `SETTINGS` | Pengaturan aplikasi. |
| `HOW_TO_PLAY` | Petunjuk permainan. |
| `EXIT_CONFIRM` | Konfirmasi keluar aplikasi. |

### 15.5 `MatchState`

Menentukan fase internal pertandingan.

| Nilai | Keterangan |
|---|---|
| `SETUP` | Sesi sedang disiapkan. |
| `WAITING` | Menunggu pemain siap melakukan tindakan. |
| `AIMING` | Pemain mengatur arah bidikan. |
| `POWER_SETTING` | Pemain sedang mengatur power. |
| `BALL_IN_HAND` | Pemain sedang menempatkan cue ball. |
| `SIMULATING` | Bola sedang bergerak dan simulasi berlangsung. |
| `PAUSED` | Pertandingan dihentikan sementara. |
| `FINISHED` | Pertandingan telah selesai. |

### 15.6 `BallGroup`

Menentukan kelompok bola pemain pada 8-Ball.

| Nilai | Keterangan |
|---|---|
| `NONE` | Kelompok belum ditentukan atau tidak berlaku. |
| `SOLID` | Kelompok bola 1–7. |
| `STRIPE` | Kelompok bola 9–15. |

### 15.7 `FoulType`

Mengidentifikasi jenis foul yang dikenali sistem.

| Nilai | Keterangan |
|---|---|
| `NONE` | Tidak terjadi foul. |
| `SCRATCH` | Cue ball masuk pocket. |
| Nilai foul tambahan | Hanya ditambahkan apabila jenis foul tersebut termasuk implementasi dan pengujian proyek. |

Timeout tidak dimasukkan sebagai `FoulType`, karena timeout bukan foul dalam keputusan proyek.

### 15.8 `SoundType`

Menentukan kategori efek suara yang dapat diminta dari `AudioManager`.

| Nilai | Keterangan |
|---|---|
| `BALL_COLLISION` | Tumbukan antarb bola. |
| `CUSHION_HIT` | Bola mengenai cushion. |
| `BALL_POCKETED` | Bola masuk pocket. |
| `CUE_HIT` | Cue mengenai cue ball. |
| `UI_CLICK` | Interaksi tombol atau elemen UI. |

### 15.9 Contoh deklarasi enum

Contoh berikut menggambarkan nilai baseline. Implementasi dapat menambahkan nilai teknis yang diperlukan selama tidak bertentangan dengan keputusan proyek.

```cpp
enum class GameType {
    EIGHT_BALL,
    NINE_BALL
};

enum class OpponentType {
    LOCAL_PLAYER,
    BOT
};

enum class DisplayMode {
    WINDOWED,
    FULLSCREEN
};

enum class ScreenType {
    MAIN_MENU,
    MATCH_SETUP,
    GAME,
    PAUSE,
    RESULT,
    HISTORY,
    SETTINGS,
    HOW_TO_PLAY,
    EXIT_CONFIRM
};

enum class MatchState {
    SETUP,
    WAITING,
    AIMING,
    POWER_SETTING,
    BALL_IN_HAND,
    SIMULATING,
    PAUSED,
    FINISHED
};

enum class BallGroup {
    NONE,
    SOLID,
    STRIPE
};

enum class FoulType {
    NONE,
    SCRATCH
};

enum class SoundType {
    BALL_COLLISION,
    CUSHION_HIT,
    BALL_POCKETED,
    CUE_HIT,
    UI_CLICK
};
---

## 16. Hubungan Antarkelas

Bagian ini menjelaskan hubungan konseptual antarkelas dalam YouKnowBall. Relasi digunakan sebagai acuan penyusunan Class Diagram dan implementasi komunikasi antarkomponen. Class Diagram akhir harus mengikuti lifetime objek, kepemilikan aktual, dan alur komunikasi yang benar-benar diterapkan. Tabel relasi di bawah merupakan rancangan konseptual, bukan pengganti pemeriksaan deklarasi atribut dan implementasi.

### 16.1 Relasi Utama

| Komponen Pertama | Jenis Hubungan | Komponen Kedua | Makna |
|---|---|---|---|
| `GameApp` | Association / koordinasi | `ScreenManager` | Aplikasi menginisialisasi dan mengoordinasikan pengelola layar. |
| `GameApp` | Association / koordinasi | `StorageManager` | Aplikasi menggunakan layanan pemuatan dan penyimpanan data. |
| `GameApp` | Association / koordinasi | `AudioManager` | Aplikasi menginisialisasi dan mengoordinasikan layanan audio. |
| `ScreenManager` | Association | `MatchSession` | Antarmuka meneruskan interaksi dan menampilkan keadaan sesi pertandingan. |
| `MatchSession` | Association / pengelolaan | `Player` | Sesi menggunakan data dua pemain selama pertandingan. |
| `MatchSession` | Association / pengelolaan | `PlayerController` | Sesi mengelola controller pemain melalui kontrak dasarnya. |
| `HumanController` | Inheritance | `PlayerController` | Controller manusia mengimplementasikan kontrak controller. |
| `BotController` | Inheritance | `PlayerController` | Controller Bot mengimplementasikan kontrak controller. |
| `MatchSession` | Association / pengelolaan | `Table` | Sesi menggunakan meja sebagai model keadaan permainan. |
| `MatchSession` | Association / pengelolaan | `Cue` | Sesi menggunakan Cue untuk memproses arah, power, dan impuls pukulan. |
| `MatchSession` | Association / pengelolaan | `PhysicsEngine` | Sesi mengoordinasikan simulasi fisika. |
| `MatchSession` | Association / pengelolaan | `GameRules` | Sesi meminta evaluasi dan menerapkan hasil aturan. |
| `Table` | Composition | `Ball` | Meja menyimpan kumpulan bola yang menjadi bagian dari keadaan meja. |
| `Table` | Composition | `PocketData` | Meja menyimpan enam data pocket. |
| `HumanController` | Association | `Cue` | Controller manusia mengubah input arah dan power melalui Cue. |
| `BotController` | Association | `Table` | Bot membaca kondisi meja untuk memilih pukulan. |
| `BotController` | Association | `Player` | Bot membaca informasi pemain dan kelompok bola. |
| `BotController` | Association | `Cue` | Bot menggunakan parameter bidikan dan power yang diproses melalui Cue. |
| `PhysicsEngine` | Association | `Table` | Mesin fisika membaca dan memperbarui keadaan bola melalui Table. |
| `GameRules` | Association | `Table` | Evaluasi aturan membutuhkan keadaan meja. |
| `GameRules` | Association | `Player` | Evaluasi aturan membutuhkan kelompok dan data pemain. |
| `GameRules` | Association | `ShotStartState` | Evaluasi menggunakan snapshot sebelum pukulan. |
| `GameRules` | Association | `ShotResult` | Evaluasi menggunakan fakta hasil simulasi. |
| `MatchSession` | Association | `ShotCommand` | Sesi menerima perintah pukulan dari controller. |
| `MatchSession` | Association | `RuleOutcome` | Sesi menerapkan keputusan aturan. |
| `StorageManager` | Association | `AppSettings` | Penyimpanan membaca dan menulis pengaturan. |
| `StorageManager` | Association | `MatchRecord` | Penyimpanan membaca dan menulis riwayat pertandingan. |
| Komponen pemicu audio | Association | `AudioManager` / `SoundType` | Komponen yang mengetahui terjadinya kejadian meminta AudioManager memutar efek suara yang sesuai. |

Jenis hubungan pada tabel di atas menjelaskan kolaborasi konseptual. Notasi kepemilikan, multiplicity, dan navigability pada Class Diagram final harus mengikuti deklarasi atribut, lifetime objek, serta implementasi aktual; jangan mengubah association menjadi composition hanya karena satu class menggunakan class lain. `Table`–`Ball` dan `Table`–`PocketData` merupakan komposisi pada rancangan ini.\n\n### 16.2 Prinsip Komunikasi Antarkelas

1. `GameApp` menjadi titik koordinasi siklus aplikasi.
2. `ScreenManager` mengelola halaman dan interaksi antarmuka.
3. `MatchSession` menjadi pusat koordinasi pertandingan.
4. Controller tidak mengubah keadaan bola secara langsung.
5. `Cue` mengubah arah dan power menjadi data impuls.
6. `PhysicsEngine` mengubah keadaan fisik bola dan mencatat fakta kejadian.
7. `GameRules` membaca snapshot awal dan hasil simulasi untuk menentukan konsekuensi aturan.
8. `MatchSession` menerapkan hasil evaluasi terhadap giliran dan status pertandingan.
9. `StorageManager` menangani penyimpanan data, bukan keputusan gameplay.
10. `AudioManager` menangani pemutaran audio, bukan penentuan kejadian gameplay.

### 16.3 Prinsip Pemisahan Data dan Perilaku

Data yang dibawa oleh struct tidak boleh mengambil alih tanggung jawab class pemilik proses.

| Struct | Pembawa Data | Penanggung Jawab Proses |
|---|---|---|
| `MatchConfig` | Konfigurasi pertandingan | `MatchSession` |
| `AppSettings` | Pengaturan aplikasi | `GameApp`, `ScreenManager`, dan `AudioManager` sesuai kebutuhan |
| `MatchRecord` | Ringkasan pertandingan | `StorageManager` |
| `PocketData` | Posisi dan area pocket | `Table` |
| `ShotCommand` | Data perintah pukulan | Controller menghasilkan, `MatchSession` menerima dan memproses |
| `ShotStartState` | Snapshot sebelum pukulan | `MatchSession` memastikan waktu pengambilan snapshot |
| `ShotResult` | Fakta fisik selama simulasi | `PhysicsEngine` mengumpulkan fakta |
| `RuleOutcome` | Keputusan evaluasi aturan | `GameRules` menghasilkan, `MatchSession` menerapkan |

---

## 17. Alur Kolaborasi Satu Pukulan

Satu pukulan harus melewati satu jalur pemrosesan yang sama, baik berasal dari pemain manusia maupun Bot Easy.

### 17.1 Alur Umum

1. Pemain aktif melakukan tindakan melalui controller.
2. Controller menghasilkan `ShotCommand`.
3. `MatchSession` memeriksa bahwa perintah dapat diterima pada fase pertandingan yang sesuai.
4. `MatchSession` mengambil `ShotStartState` tepat satu kali.
5. `Cue` menghitung impuls akhir berdasarkan arah dan power pada `ShotCommand`.
6. `PhysicsEngine` memulai pencatatan pukulan melalui `beginShot()`.
7. Impuls diberikan kepada cue ball.
8. `PhysicsEngine` menjalankan simulasi gerak bola.
9. Selama simulasi, `PhysicsEngine` memperbarui posisi dan kecepatan, menangani tumbukan, cushion, gesekan, serta pocket.
10. `PhysicsEngine` mencatat kejadian ke `ShotResult`.
11. Simulasi berlanjut sampai seluruh bola berhenti.
12. `GameRules` menerima `ShotStartState`, `ShotResult`, kondisi meja, dan data pemain.
13. `GameRules` menghasilkan `RuleOutcome`.
14. `MatchSession` menerapkan hasil evaluasi.
15. Jika pertandingan selesai, `MatchSession` membentuk `MatchRecord` dan meminta `StorageManager` menyimpannya.
16. Jika pertandingan berlanjut, `MatchSession` menyiapkan giliran atau fase berikutnya.
17. `ScreenManager` menampilkan keadaan permainan berikutnya atau halaman Result.

### 17.2 Urutan Tanggung Jawab

| Tahap | Komponen | Tanggung Jawab |
|---:|---|---|
| 1 | `HumanController` / `BotController` | Menghasilkan `ShotCommand`. |
| 2 | `MatchSession` | Memvalidasi dan menerima perintah. |
| 3 | `MatchSession` | Mengambil `ShotStartState` satu kali. |
| 4 | `Cue` | Menghitung impuls dari arah dan power. |
| 5 | `PhysicsEngine` | Memulai pencatatan kejadian pukulan. |
| 6 | `PhysicsEngine` dan `Ball` | Menjalankan simulasi gerak dan tumbukan. |
| 7 | `PhysicsEngine` | Menghasilkan `ShotResult`. |
| 8 | `GameRules` | Mengevaluasi aturan dan menghasilkan `RuleOutcome`. |
| 9 | `MatchSession` | Menerapkan hasil dan mengatur fase berikutnya. |
| 10 | `StorageManager` | Menyimpan hasil apabila pertandingan telah selesai. |
| 11 | `ScreenManager` | Menampilkan perubahan keadaan permainan. |

### 17.3 Ketentuan Snapshot dan Impuls

Untuk setiap pukulan yang diterima:

- `ShotStartState` dibuat tepat satu kali.
- Snapshot dibuat sebelum impuls diberikan kepada cue ball.
- `Cue` menghitung impuls akhir setelah perintah diterima.
- `PhysicsEngine` menerima impuls dan menjalankan simulasi.
- Snapshot tidak dibuat ulang selama simulasi.
- Resume tidak mengulang pengambilan snapshot.
- Resume tidak memberikan impuls kedua.
- Satu `ShotCommand` tidak boleh diproses lebih dari satu kali.

Ketentuan ini mencegah satu pukulan dihitung sebagai beberapa pukulan akibat update berulang atau transisi state.

### 17.4 Pemrosesan Setelah Bola Berhenti

`PhysicsEngine` hanya menyatakan bahwa simulasi telah selesai dan menyediakan `ShotResult`.

Setelah itu:

1. `MatchSession` memastikan seluruh bola telah berhenti.
2. `GameRules` mengevaluasi hasil berdasarkan snapshot awal dan fakta simulasi.
3. `GameRules` menghasilkan `RuleOutcome`.
4. `MatchSession` menerapkan foul, ball-in-hand, pergantian giliran, kelanjutan giliran, respot, atau hasil akhir sesuai keputusan.
5. Jika permainan belum selesai, timer untuk pemain berikutnya disiapkan.
6. Jika permainan selesai, hasil pertandingan disimpan satu kali.

### 17.5 Jalur Pemain Manusia dan Bot

| Aspek | Pemain Manusia | Bot Easy |
|---|---|---|
| Sumber Keputusan | Mouse dan keyboard | Heuristik sederhana |
| Pengendali | `HumanController` | `BotController` |
| Format Perintah | `ShotCommand` | `ShotCommand` |
| Penerima Perintah | `MatchSession` | `MatchSession` |
| Simulasi | `PhysicsEngine` | `PhysicsEngine` |
| Evaluasi Aturan | `GameRules` | `GameRules` |

Perbedaan hanya berada pada cara controller menghasilkan perintah. Proses simulasi, evaluasi aturan, dan pengelolaan hasil tetap sama.

---

## 18. Use Case dan Skenario Penggunaan Menyeluruh

Bagian ini menjelaskan interaksi pengguna dengan YouKnowBall sejak aplikasi dijalankan hingga pengguna menyelesaikan pertandingan atau keluar dari aplikasi.

Penjelasan dibagi menjadi dua bagian utama, yaitu narasi skenario penggunaan dan urutan langkah penggunaan sistem.

### 18.1 Aktor Sistem

| Aktor | Deskripsi |
|---|---|
| Player 1 | Pemain pertama yang bermain menggunakan kontrol mouse dan keyboard. |
| Player 2 | Pemain kedua dalam mode Local Multiplayer yang bermain pada perangkat yang sama. |
| Bot Easy | Lawan komputer dengan tingkat kesulitan mudah yang dikendalikan oleh sistem. |

Pada mode Local Multiplayer, Player 1 dan Player 2 bermain secara bergantian menggunakan perangkat yang sama.

Pada mode Human vs Bot, pengguna bermain melawan Bot Easy. Bot mengambil keputusan pukulan secara otomatis berdasarkan kondisi permainan dan strategi sederhana.

### 18.2 Identitas Skenario

| Elemen | Keterangan |
|---|---|
| Nama Skenario | Menggunakan YouKnowBall dan Memainkan Pertandingan hingga Selesai |
| Tujuan | Mengatur pertandingan, memainkan 8-Ball atau 9-Ball, melihat hasil, dan mengakses fitur pendukung aplikasi. |
| Aktor Utama | Pemain |
| Aktor Pendukung | Bot Easy jika dipilih |
| Pemicu | Pemain menjalankan aplikasi YouKnowBall. |
| Prasyarat | Aplikasi telah terpasang dan dapat dijalankan. |
| Kondisi Akhir Sukses | Pertandingan selesai, hasil ditampilkan dan disimpan, serta pemain dapat melanjutkan ke menu lain atau keluar. |
| Kondisi Akhir Alternatif | Jika pertandingan dibatalkan sebelum selesai, pertandingan tidak disimpan sebagai hasil pertandingan. |

### 18.3 Narasi Skenario Penggunaan

Ketika aplikasi YouKnowBall dijalankan, sistem menampilkan halaman Main Menu sebagai halaman utama. Pada halaman ini, pengguna dapat memilih permainan 8-Ball melalui tombol **Main 8-Ball** atau permainan 9-Ball melalui tombol **Main 9-Ball**. Kedua tombol tersebut tersedia secara langsung pada Main Menu sehingga pengguna tidak perlu memilih mode permainan melalui tombol Start Match terlebih dahulu.

Selain pilihan permainan, Main Menu menyediakan akses menuju Match History, Application Settings, How to Play, dan Exit.

Jika pengguna memilih Main 8-Ball atau Main 9-Ball, sistem menampilkan halaman pengaturan pertandingan. Pada halaman tersebut, pengguna dapat menentukan jenis lawan yang akan dihadapi, yaitu Local Multiplayer atau Human vs Bot. Pengguna juga dapat mengisi nama pemain dan menentukan batas waktu setiap giliran. Pilihan waktu yang tersedia adalah Unlimited, 15 Seconds, 30 Seconds, dan 60 Seconds.

Setelah pengaturan pertandingan selesai, pengguna memulai pertandingan. Sistem menyiapkan meja, susunan bola, pemain, dan giliran awal, kemudian menampilkan halaman permainan.

Pada saat giliran pemain aktif, pemain dapat mengarahkan cue stick untuk menentukan arah tembakan. Setelah arah ditentukan, pemain mengatur kekuatan tembakan menggunakan indikator pengaturan power berbentuk cue stick yang terpisah dari cue stick pada meja. Indikator power hanya mengatur kekuatan tembakan dan tidak mengubah arah bidikan.

Apabila pemain ingin membatalkan pengaturan power sebelum melepaskan kontrol mouse, pemain dapat menekan tombol Space. Tindakan tersebut membatalkan proses pengaturan power sehingga pemain dapat kembali mengatur arah tembakan.

Ketika tembakan dilepaskan, sistem menjalankan simulasi fisika. Bola bergerak berdasarkan arah dan kekuatan tembakan, mengalami tumbukan dengan bola lain, pantulan pada cushion, perlambatan akibat gesekan, dan kemungkinan masuk ke pocket. Sistem juga menampilkan prediksi lintasan sederhana yang membantu pemain memperkirakan arah cue ball hingga tumbukan pertama dan arah awal bola objek setelah tumbukan.

Sistem menunggu hingga seluruh bola berhenti bergerak sebelum mengevaluasi hasil tembakan. Setelah itu, sistem menentukan apakah tembakan termasuk legal atau foul, apakah pemain mempertahankan giliran, apakah giliran berpindah, apakah cue ball harus ditempatkan kembali, dan apakah pertandingan telah berakhir.

Pada permainan 8-Ball, meja pada awalnya berstatus terbuka. Kelompok Solid atau Stripe ditentukan ketika satu pukulan sah memasukkan bola dari satu kelompok saja. Jika Solid dan Stripe masuk bersamaan ketika meja masih terbuka, kelompok belum ditentukan dan meja tetap terbuka. Pemain harus memasukkan seluruh bola kelompoknya sebelum memasukkan bola 8 secara sah.

Jika bola 8 masuk saat break, bola 8 dikembalikan ke meja dan permainan dilanjutkan. Jika bola 8 masuk sebelum seluruh kelompok pemain habis, pemain yang melakukan pukulan kalah. Jika bola 8 masuk secara sah setelah seluruh kelompoknya habis, pemain tersebut menang. Bola 8 yang masuk bersama scratch atau foul juga menyebabkan pemain yang melakukan pukulan kalah.

Pada permainan 9-Ball, pemain harus mengenai bola bernomor paling kecil yang masih aktif sebagai bola pertama yang terkena cue ball. Bola lain boleh masuk selama kontak pertama memenuhi ketentuan tersebut. Pemain yang memasukkan bola 9 secara sah memenangkan pertandingan. Jika bola 9 masuk bersama foul, pemain tidak menang, bola 9 dikembalikan ke meja, dan foul tetap diproses. Jika bola 9 masuk saat break, bola 9 dikembalikan ke meja dan permainan dilanjutkan.

Jika terjadi foul atau scratch, sistem mengalihkan giliran kepada lawan dan memberikan hak ball-in-hand. Pemain yang memperoleh ball-in-hand dapat menempatkan cue ball pada posisi yang valid di area permainan.

Pada mode Bot Easy, bot mengambil giliran secara otomatis. Bot membaca kondisi meja, memilih target, menentukan arah dan power sederhana, kemudian menghasilkan perintah pukulan. Tembakan bot diproses melalui jalur simulasi dan evaluasi aturan yang sama dengan pemain manusia.

Timer berjalan sesuai pilihan batas waktu. Jika waktu habis ketika pemain sedang mengatur power, sistem langsung menjalankan tembakan menggunakan power yang telah tercapai pada saat waktu habis. Jika waktu habis ketika pemain tidak sedang mengatur power, giliran langsung berpindah kepada lawan. Timeout tidak dianggap sebagai foul dan tidak memberikan ball-in-hand.

Selama pertandingan berlangsung, pemain dapat menekan tombol Escape untuk membuka Pause Menu. Sistem menghentikan sementara timer dan simulasi permainan. Jika pemain sedang melakukan drag yang belum menghasilkan pukulan, input tersebut dibatalkan agar tidak terjadi tembakan yang tidak disengaja.

Pada Pause Menu, pemain dapat melanjutkan pertandingan, membuka pengaturan, memulai ulang pertandingan, atau kembali ke Main Menu. Jika pemain membuka Settings, pengguna dapat mengatur volume musik, volume efek suara, sensitivitas mouse, dan display mode Windowed atau Fullscreen. Simulasi dan timer tetap berhenti selama halaman Settings dibuka.

Perubahan pengaturan dapat diterapkan dan disimpan melalui tombol Apply/Save. Jika pengguna memilih Back sebelum menerapkan perubahan, perubahan yang belum diterapkan dibatalkan dan sistem kembali ke halaman sebelumnya.

Apabila pemain memilih Restart, sistem menampilkan konfirmasi sebelum memulai ulang pertandingan dengan konfigurasi yang sama. Pertandingan yang dihentikan melalui Restart tidak disimpan sebagai hasil pertandingan pada Match History.

Jika pemain memilih Main Menu dari Pause Menu, sistem juga menampilkan konfirmasi. Jika disetujui, pertandingan aktif dibatalkan dan tidak disimpan sebagai hasil pertandingan.

Jika pertandingan selesai, sistem menampilkan Result Page yang berisi nama pemain, pemenang, jenis permainan, statistik bola masuk, statistik foul, dan durasi pertandingan. Hasil pertandingan yang telah selesai disimpan ke penyimpanan lokal dan tersedia pada Match History.

Pengguna dapat memilih Rematch untuk langsung memulai pertandingan baru menggunakan konfigurasi pertandingan sebelumnya. Hasil pertandingan sebelumnya tetap tersimpan. Jika pengguna ingin mengubah konfigurasi, pengguna harus kembali ke Main Menu dan memilih Main 8-Ball atau Main 9-Ball sesuai mode yang diinginkan.

Pengguna juga dapat membuka Match History dari Main Menu untuk melihat daftar pertandingan yang telah selesai dan memilih salah satu catatan untuk melihat detail pertandingan. Pengguna dapat membuka How to Play untuk mempelajari kontrol, aturan 8-Ball, aturan 9-Ball, foul, scratch, dan ball-in-hand.

Jika pengguna memilih Exit pada Main Menu, sistem menampilkan konfirmasi sebelum menutup aplikasi. Jika pengguna membatalkan, aplikasi tetap berjalan. Jika pengguna menyetujui, sistem menutup aplikasi dan melepaskan resource yang digunakan.

### 18.4 Urutan Langkah Penggunaan Sistem

#### A. Menjalankan Aplikasi dan Membuka Main Menu

1. Pengguna menjalankan aplikasi YouKnowBall.
2. Sistem melakukan inisialisasi aplikasi.
3. Sistem memuat pengaturan aplikasi yang tersimpan.
4. Sistem menyiapkan komponen audio dan tampilan.
5. Sistem menampilkan Main Menu.
6. Pengguna dapat memilih:
   - Main 8-Ball.
   - Main 9-Ball.
   - Match History.
   - Application Settings.
   - How to Play.
   - Exit.

#### B. Memulai Pertandingan 8-Ball

1. Pengguna memilih tombol Main 8-Ball.
2. Sistem membuka halaman pengaturan pertandingan dengan mode 8-Ball yang sudah ditentukan.
3. Pengguna memilih jenis lawan:
   - Local Multiplayer.
   - Human vs Bot.
4. Jika pengguna memilih Local Multiplayer, sistem menyediakan pengaturan nama Player 1 dan Player 2.
5. Jika pengguna memilih Human vs Bot, sistem menyediakan pengaturan nama pemain dan menggunakan Bot Easy sebagai lawan.
6. Pengguna memilih batas waktu setiap giliran:
   - Unlimited.
   - 15 Seconds.
   - 30 Seconds.
   - 60 Seconds.
7. Pengguna mengonfirmasi pengaturan pertandingan.
8. Sistem menyiapkan meja dan susunan bola untuk permainan 8-Ball.
9. Sistem menentukan pemain yang melakukan break sesuai mekanisme awal pertandingan.
10. Sistem memulai pertandingan dan menampilkan halaman permainan.

#### C. Memulai Pertandingan 9-Ball

1. Pengguna memilih tombol Main 9-Ball.
2. Sistem membuka halaman pengaturan pertandingan dengan mode 9-Ball yang sudah ditentukan.
3. Pengguna memilih jenis lawan:
   - Local Multiplayer.
   - Human vs Bot.
4. Pengguna mengisi nama pemain sesuai jenis pertandingan.
5. Jika memilih Human vs Bot, sistem menggunakan Bot Easy sebagai lawan.
6. Pengguna menentukan batas waktu setiap giliran.
7. Pengguna mengonfirmasi pengaturan pertandingan.
8. Sistem menyiapkan meja dan susunan bola untuk permainan 9-Ball.
9. Sistem menentukan pemain yang melakukan break sesuai mekanisme awal pertandingan.
10. Sistem memulai pertandingan dan menampilkan halaman permainan.

#### D. Melakukan Tembakan

1. Sistem menampilkan pemain yang sedang mendapatkan giliran.
2. Sistem mengaktifkan timer jika pertandingan menggunakan batas waktu.
3. Pemain mengarahkan cue stick menggunakan mouse untuk menentukan arah tembakan.
4. Sistem menampilkan prediksi lintasan sederhana.
5. Pemain mengatur kekuatan tembakan melalui indikator power berbentuk cue stick yang terpisah dari cue stick pada meja.
6. Sistem mengunci arah bidikan selama power sedang diatur.
7. Pemain dapat menekan tombol Space untuk membatalkan pengaturan power sebelum melepaskan kontrol mouse.
8. Jika pengaturan power dibatalkan, pemain dapat kembali menentukan arah tembakan.
9. Jika pemain melepaskan kontrol power secara normal, sistem memproses tembakan.
10. Sistem mengambil snapshot kondisi sebelum impuls diberikan.
11. Sistem menerapkan arah dan kekuatan tembakan pada cue ball.
12. Sistem menjalankan simulasi pergerakan bola.
13. Sistem mendeteksi tumbukan antarb bola, pantulan cushion, perlambatan, dan bola yang masuk pocket.
14. Sistem menunggu sampai seluruh bola berhenti bergerak.
15. Sistem mengevaluasi hasil tembakan berdasarkan aturan mode permainan.
16. Sistem menentukan apakah pemain tetap mendapatkan giliran atau giliran berpindah.
17. Jika terjadi foul atau scratch, sistem menerapkan konsekuensi sesuai aturan permainan.
18. Jika pertandingan belum selesai, sistem mempersiapkan giliran berikutnya.

#### E. Menghadapi Bot Easy

1. Pemain manusia menyelesaikan gilirannya.
2. Sistem mengevaluasi hasil tembakan pemain.
3. Jika giliran berpindah kepada bot, sistem mengaktifkan Bot Easy.
4. Bot membaca kondisi meja dan bola yang tersedia.
5. Bot menentukan target, arah, dan kekuatan tembakan menggunakan strategi sederhana.
6. Bot menghasilkan `ShotCommand`.
7. Sistem memproses tembakan bot melalui alur simulasi yang sama dengan tembakan pemain manusia.
8. Sistem menunggu seluruh bola berhenti.
9. Sistem mengevaluasi hasil tembakan bot.
10. Sistem menentukan giliran berikutnya berdasarkan hasil evaluasi.
11. Proses berulang hingga pertandingan selesai.

#### F. Menghadapi Timer dan Batas Waktu Giliran

1. Timer berjalan selama giliran pemain aktif apabila batas waktu yang dipilih bukan Unlimited.
2. Jika pemain menyelesaikan tembakan sebelum waktu habis, timer dihentikan untuk giliran tersebut.
3. Jika waktu habis ketika pemain sedang mengatur power, sistem langsung menjalankan tembakan menggunakan kekuatan yang telah dicapai saat itu.
4. Jika waktu habis ketika pemain tidak sedang mengatur power, sistem langsung memindahkan giliran kepada pemain berikutnya.
5. Timeout tidak dianggap sebagai foul.
6. Timeout tidak memberikan ball-in-hand.
7. Sistem mempersiapkan giliran berikutnya sesuai kondisi pertandingan.

#### G. Membuka Pause Menu

1. Pemain menekan tombol Escape ketika pertandingan berlangsung.
2. Sistem menghentikan sementara simulasi permainan dan timer.
3. Jika terdapat input drag yang belum menghasilkan pukulan, sistem membatalkan input tersebut.
4. Sistem menampilkan Pause Menu.
5. Pengguna dapat memilih:
   - Continue.
   - Settings.
   - Restart.
   - Main Menu.

**Continue**

1. Pengguna memilih Continue.
2. Sistem menutup Pause Menu.
3. Sistem melanjutkan pertandingan dari kondisi sebelumnya.
4. Timer dilanjutkan dengan sisa waktu sebelumnya.
5. Sistem tidak mengulang snapshot atau menjalankan impuls pukulan yang sama.

**Settings**

1. Pengguna memilih Settings.
2. Sistem menampilkan pengaturan aplikasi.
3. Pengguna dapat mengubah:
   - Music Volume.
   - SFX Volume.
   - Mouse Sensitivity.
   - Display Mode.
4. Pengguna memilih Apply/Save untuk menerapkan dan menyimpan perubahan.
5. Sistem menyimpan pengaturan ke file TXT.
6. Jika pengguna memilih Back sebelum menerapkan perubahan, sistem membatalkan perubahan yang belum diterapkan.
7. Sistem kembali ke Pause Menu.
8. Timer dan simulasi tetap berhenti sampai pengguna memilih Continue.

**Restart**

1. Pengguna memilih Restart.
2. Sistem menampilkan konfirmasi restart.
3. Jika pengguna membatalkan, sistem kembali ke Pause Menu.
4. Jika pengguna menyetujui, sistem mengakhiri pertandingan aktif tanpa menyimpannya ke Match History.
5. Sistem memulai ulang pertandingan menggunakan konfigurasi yang sama.
6. Sistem menyiapkan kembali kondisi awal pertandingan.

**Main Menu**

1. Pengguna memilih Main Menu.
2. Sistem menampilkan konfirmasi untuk meninggalkan pertandingan.
3. Jika pengguna membatalkan, sistem kembali ke Pause Menu.
4. Jika pengguna menyetujui, sistem meninggalkan pertandingan aktif dan kembali ke Main Menu.
5. Pertandingan yang belum selesai tidak disimpan sebagai hasil pertandingan.

#### H. Menampilkan Hasil Pertandingan

1. Sistem mendeteksi kondisi kemenangan berdasarkan aturan mode permainan.
2. Sistem mengakhiri pertandingan.
3. Sistem menentukan pemenang.
4. Sistem menyusun ringkasan pertandingan.
5. Sistem menyimpan hasil pertandingan ke penyimpanan lokal satu kali.
6. Sistem menampilkan Result Page.
7. Result Page menampilkan:
   - Nama pemain.
   - Nama pemenang.
   - Jenis permainan.
   - Statistik bola masuk.
   - Statistik foul.
   - Durasi pertandingan.
8. Pengguna dapat memilih:
   - Rematch.
   - Main Menu.

**Rematch**

1. Pengguna memilih Rematch.
2. Sistem mempertahankan konfigurasi pertandingan sebelumnya.
3. Sistem membuat pertandingan baru dengan konfigurasi yang sama.
4. Sistem menyiapkan kondisi awal pertandingan baru.
5. Pertandingan sebelumnya tetap tersimpan di Match History.
6. Hasil pertandingan baru akan disimpan setelah pertandingan tersebut selesai.

**Main Menu**

1. Pengguna memilih Main Menu.
2. Sistem kembali ke halaman utama.
3. Pengguna dapat memulai pertandingan baru atau membuka menu lainnya.

#### I. Membuka Match History

1. Pengguna memilih Match History dari Main Menu.
2. Sistem membaca data riwayat pertandingan dari penyimpanan lokal.
3. Sistem menampilkan daftar pertandingan yang telah selesai.
4. Jika belum ada riwayat, sistem menampilkan informasi bahwa belum ada pertandingan yang tersimpan.
5. Pengguna memilih salah satu pertandingan.
6. Sistem menampilkan detail hasil pertandingan yang dipilih.
7. Pengguna dapat kembali ke daftar riwayat atau kembali ke Main Menu.

#### J. Membuka How to Play

1. Pengguna memilih How to Play dari Main Menu.
2. Sistem menampilkan panduan permainan.
3. Pengguna dapat membaca informasi mengenai:
   - Kontrol permainan.
   - Cara mengarahkan cue stick.
   - Cara mengatur power.
   - Fungsi tombol Space.
   - Prediksi lintasan.
   - Aturan permainan 8-Ball.
   - Aturan permainan 9-Ball.
   - Foul dan scratch.
   - Ball-in-hand.
4. Pengguna kembali ke Main Menu setelah selesai membaca panduan.

#### K. Mengubah Application Settings dari Main Menu

1. Pengguna memilih Application Settings.
2. Sistem menampilkan halaman pengaturan aplikasi.
3. Pengguna dapat mengubah Music Volume, SFX Volume, Mouse Sensitivity, dan Display Mode.
4. Pengguna memilih Apply/Save untuk menerapkan dan menyimpan perubahan.
5. Sistem menyimpan pengaturan ke file TXT.
6. Jika pengguna memilih Back sebelum menerapkan perubahan, sistem membatalkan perubahan yang belum diterapkan.
7. Sistem kembali ke Main Menu.

#### L. Keluar dari Aplikasi

1. Pengguna memilih Exit pada Main Menu.
2. Sistem menampilkan konfirmasi keluar.
3. Jika pengguna membatalkan, sistem kembali ke aplikasi.
4. Jika pengguna menyetujui, sistem menjalankan proses penutupan aplikasi.
5. Sistem menghentikan audio dan proses yang masih berjalan.
6. Sistem melepaskan resource yang digunakan.
7. Aplikasi YouKnowBall ditutup.

### 18.5 Alur Alternatif dan Kondisi Khusus

| ID | Kondisi | Respons Sistem |
|---|---|---|
| A1 | Pengaturan dibatalkan | Perubahan yang belum diterapkan dibatalkan dan sistem kembali ke halaman sebelumnya. |
| A2 | Match Setup belum lengkap | Sistem meminta pengguna melengkapi data yang diperlukan. |
| A3 | Power dibatalkan menggunakan Space | Tarikan power dibatalkan dan pemain dapat mengatur arah kembali. |
| A4 | Timeout saat tidak mengatur power | Giliran berpindah tanpa foul dan tanpa ball-in-hand. |
| A5 | Timeout saat power sedang ditarik | Tembakan langsung dijalankan menggunakan power saat itu. |
| A6 | Terjadi foul atau scratch | Giliran berpindah kepada lawan dan lawan memperoleh ball-in-hand. |
| A7 | Posisi cue ball tidak valid | Sistem menolak posisi dan meminta pemain memilih posisi lain. |
| A8 | Pause saat drag belum selesai | Input dibatalkan, tidak ada tembakan, timer dan simulasi berhenti. |
| A9 | Restart disetujui | Pertandingan aktif dibatalkan, rack baru disiapkan, dan hasil lama tidak disimpan. |
| A10 | Kembali ke Main Menu disetujui sebelum pertandingan selesai | Sesi dibatalkan dan tidak disimpan sebagai pertandingan selesai. |
| A11 | Bola 8 masuk saat break | Bola 8 dikembalikan ke meja dan permainan dilanjutkan. |
| A12 | Bola 9 masuk saat break | Bola 9 di-respot dan permainan dilanjutkan. |
| A13 | Solid dan Stripe masuk bersamaan saat meja terbuka | Kelompok belum ditentukan dan meja tetap terbuka. |
| A14 | Bola 8 masuk sebelum kelompok sendiri habis | Pemain yang melakukan pukulan kalah. |
| A15 | Bola 8 masuk bersama scratch atau foul | Pemain yang melakukan pukulan kalah. |
| A16 | Bola 9 masuk bersama foul | Tidak menghasilkan kemenangan; bola 9 di-respot dan foul diproses. |
| A17 | Rematch dipilih | Pertandingan baru dimulai dengan konfigurasi sebelumnya. |
| A18 | Match History kosong | Sistem menampilkan informasi bahwa belum ada pertandingan selesai. |
| A19 | Exit dibatalkan | Dialog ditutup dan aplikasi tetap berjalan. |
| A20 | Window di-resize | Konten tetap mempertahankan rasio 16:9 dan koordinat mouse tetap akurat. |
| A21 | File TXT tidak tersedia atau rusak | Sistem menggunakan pengaturan default atau riwayat kosong tanpa crash. |

---

## 19. Pembagian Peran Anggota

Pembagian peran dilakukan agar setiap anggota memiliki tanggung jawab yang jelas selama proses pengembangan YouKnowBall.

PIC (Person in Charge) merupakan anggota yang bertanggung jawab mengoordinasikan dan memastikan penyelesaian pekerjaan pada bagian yang ditugaskan. Penetapan PIC tidak berarti pekerjaan hanya boleh dilakukan oleh satu orang. Anggota lain tetap dapat membantu coding, pengujian, debugging, dan integrasi sesuai kebutuhan.

### 19.1 Pembagian Tanggung Jawab Utama

| Anggota | Tanggung Jawab Utama | Ruang Lingkup |
|---|---|---|
| Rapid Akbar Sinatria | Antarmuka dan tampilan aplikasi | UI, layout, halaman, navigasi, HUD, window SFML, Windowed/Fullscreen, viewport, musik, dan efek suara. |
| Satya Firma Ashari | Fisika, kontrol pukulan, dan Bot Easy | Ball, Table, PocketData, PhysicsEngine, Cue, HumanController, serta BotController. |
| Muhammad Argo Iman | Data pemain, aturan, dan pengelolaan pertandingan | Player, MatchConfig, AppSettings, GameRules, RuleOutcome, MatchSession, StorageManager, dan MatchRecord. |
| Seluruh Anggota | Integrasi, pengujian, dokumentasi, dan finalisasi | Integrasi lintas modul, review kode, pengujian, perbaikan bug, laporan akhir, dan demo. |

### 19.2 Tanggung Jawab Berdasarkan Area Pekerjaan

#### A. Rapid Akbar Sinatria — Antarmuka, Window, dan Audio

Tanggung jawab utama:

1. Mengembangkan tampilan dan layout aplikasi.
2. Mengembangkan Main Menu.
3. Mengembangkan halaman pengaturan pertandingan.
4. Mengembangkan halaman permainan dan HUD.
5. Mengembangkan Pause Menu.
6. Mengembangkan halaman Application Settings.
7. Mengembangkan Result Page.
8. Mengembangkan Match History dan detail riwayat.
9. Mengembangkan How to Play.
10. Mengelola navigasi dan perpindahan halaman.
11. Mengelola window SFML dan game loop pada tingkat aplikasi.
12. Mengimplementasikan Windowed dan Fullscreen.
13. Menjaga rasio konten 16:9 ketika window di-resize.
14. Memastikan pemetaan koordinat mouse tetap akurat setelah perubahan ukuran window.
15. Mengelola musik latar, efek suara, dan volume audio.

Bagian yang menjadi fokus:

- `GameApp`.
- `ScreenManager`.
- `AudioManager`.
- Tampilan halaman aplikasi dan HUD.

#### B. Satya Firma Ashari — Fisika, Kontrol Pukulan, dan Bot Easy

Tanggung jawab utama:

1. Mengembangkan representasi objek bola.
2. Mengembangkan meja, pocket, dan geometri permainan.
3. Menentukan ukuran meja, radius bola, dan posisi pocket.
4. Mengimplementasikan pergerakan bola.
5. Mengimplementasikan gesekan dan perlambatan bola.
6. Mengimplementasikan tumbukan antarb bola.
7. Mengimplementasikan pantulan cushion.
8. Mengimplementasikan deteksi pocket.
9. Memastikan simulasi berjalan hingga seluruh bola berhenti.
10. Mengembangkan kontrol arah dan power tembakan.
11. Mengimplementasikan indikator power terpisah.
12. Mengimplementasikan pembatalan power menggunakan Space.
13. Mengembangkan prediksi lintasan sederhana.
14. Mengembangkan Bot Easy menggunakan strategi heuristik sederhana.
15. Menghasilkan fakta fisik yang dibutuhkan oleh evaluasi aturan.

Bagian yang menjadi fokus:

- `Ball`.
- `Table`.
- `Cue`.
- `PhysicsEngine`.
- `HumanController`.
- `BotController`.
- `PocketData`.
- `ShotCommand`.
- `ShotResult`.

#### C. Muhammad Argo Iman — Data Pemain, Aturan, dan Pengelolaan Pertandingan

Tanggung jawab utama:

1. Mengembangkan data identitas dan statistik pemain.
2. Mengembangkan konfigurasi pertandingan.
3. Mengembangkan pengaturan aplikasi.
4. Mengimplementasikan aturan permainan 8-Ball.
5. Mengimplementasikan aturan permainan 9-Ball.
6. Mengelola evaluasi foul dan scratch sesuai aturan proyek.
7. Mengelola penentuan kelompok Solid dan Stripe.
8. Mengelola kondisi kemenangan dan kekalahan.
9. Mengelola ball-in-hand.
10. Mengelola giliran pemain.
11. Mengelola timer dan timeout.
12. Mengelola Pause, Resume, dan Restart.
13. Mengelola penyelesaian pertandingan.
14. Menyusun hasil pertandingan.
15. Mengelola penyimpanan pengaturan dan riwayat pertandingan melalui file TXT.

Bagian yang menjadi fokus:

- `Player`.
- `MatchSession`.
- `GameRules`.
- `StorageManager`.
- `MatchConfig`.
- `AppSettings`.
- `MatchRecord`.
- `ShotStartState`.
- `RuleOutcome`.

### 19.3 Kolaborasi Antaranggota

Walaupun setiap anggota memiliki fokus tanggung jawab, pengembangan YouKnowBall tetap dilakukan secara kolaboratif.

Bentuk kolaborasi yang dilakukan meliputi:

1. **Integrasi antarmodul**

   Setiap anggota memastikan bagian yang dikerjakan dapat berkomunikasi dengan bagian lain melalui antarmuka dan struktur data yang telah disepakati.

2. **Review kode**

   Anggota lain dapat memeriksa kode untuk menemukan kesalahan logika, masalah integrasi, atau ketidaksesuaian dengan rancangan.

3. **Pengujian bersama**

   Pengujian dilakukan secara bersama untuk memastikan fitur dapat berjalan sesuai skenario penggunaan.

4. **Penyelesaian masalah**

   Jika ditemukan masalah pada bagian tertentu, anggota yang bertanggung jawab mengoordinasikan penyelesaian dengan anggota lain yang berkaitan.

5. **Dokumentasi**

   Setiap anggota membantu memastikan perubahan implementasi tercermin pada dokumentasi proyek.

### 19.4 Prinsip Pembagian Tanggung Jawab

Pembagian kerja mengikuti prinsip berikut:

- Setiap pekerjaan memiliki PIC yang jelas.
- PIC bertanggung jawab terhadap progres dan hasil pekerjaan.
- Pekerjaan dapat dibantu oleh anggota lain.
- Perubahan pada struktur data atau antarmuka antarmodul harus dikomunikasikan kepada anggota terkait.
- Integrasi dilakukan secara bertahap, bukan hanya pada akhir pengembangan.
- Setiap fitur perlu diuji sebelum dinyatakan selesai.
- Perubahan yang memengaruhi scope proyek harus disepakati bersama.

---

## 20. Pembagian Kerja dan Work Breakdown Structure (WBS) Minggu 9–15

Work Breakdown Structure (WBS) digunakan untuk membagi pekerjaan proyek YouKnowBall menjadi beberapa tahapan yang lebih kecil dan terukur. Pembagian ini membantu tim mengetahui pekerjaan yang harus diselesaikan setiap minggu, anggota yang bertanggung jawab, ketergantungan pekerjaan, serta hasil yang diharapkan.

Semua pekerjaan, termasuk laporan akhir dan persiapan demo, harus selesai paling lambat **13 Desember 2026**.

### 20.1 Ringkasan WBS

| Minggu | Periode | Kegiatan Utama | Target Keluaran | PIC |
|---|---|---|---|---|
| 9 | 1–4 November 2026 | Finalisasi kebutuhan, scope, skenario, use case, class/struct, dan pembagian awal. | Dasar kebutuhan dan rancangan awal. | Argo |
| 10 | 5–8 November 2026 | Finalisasi relasi class, kontrak method, dan struktur proyek. | Acuan desain siap implementasi. | Argo |
| 11 | 9–15 November 2026 | Ball, Table, pocket, geometri, gerak dasar, gesekan, tumbukan, cushion, dan pocket detection. | Meja dan simulasi dasar dapat diuji. | Satya |
| 12 | 16–22 November 2026 | Cue, HumanController, ShotCommand, aturan dasar, dan hasil pukulan. | Input pukulan dan evaluasi aturan awal. | Satya (Cue/controller), Argo (aturan) |
| 13 | 23–29 November 2026 | MatchSession, giliran, timer, pause/resume, foul, ball-in-hand, dan hasil. | Siklus pertandingan berjalan. | Argo |
| 14 | 30 November–6 Desember 2026 | Bot Easy, halaman/HUD, mode tampilan, StorageManager, riwayat, AudioManager, dan How to Play. | Fitur pendukung terintegrasi. | Rapid (UI/window/audio), Satya (Bot), Argo (storage) |
| 15 | 7–13 Desember 2026 | Integrasi final, uji skenario, perbaikan bug, laporan akhir, pemeriksaan, dan demo. | Build dan laporan final selesai. | Seluruh anggota |

### 20.2 Rincian Target Minggu 9

**Periode: 1–4 November 2026**

Fokus utama minggu ini adalah finalisasi rancangan proyek sebelum implementasi.

Pekerjaan:

1. Finalisasi deskripsi dan tujuan proyek.
2. Finalisasi ruang lingkup fitur.
3. Finalisasi kebutuhan sistem.
4. Finalisasi use case dan skenario penggunaan.
5. Finalisasi rancangan 14 class dan 8 struct.
6. Memeriksa tanggung jawab dan relasi antarkelas.
7. Menentukan pembagian tugas awal.
8. Menyelaraskan rancangan dengan kebutuhan implementasi.

**Target akhir Minggu 9:**

- Scope proyek disepakati.
- Kebutuhan dan fitur utama terdokumentasi.
- Skenario penggunaan dan use case tersedia.
- Rancangan class dan struct disepakati.
- Pembagian tanggung jawab awal tersedia.

### 20.3 Rincian Target Minggu 10

**Periode: 5–8 November 2026**

Fokus utama minggu ini adalah finalisasi desain dan struktur yang akan digunakan pada tahap implementasi.

Pekerjaan:

1. Menyelesaikan desain wireframe YouKnowBall (wireframe telah dipresentasikan).
2. Memeriksa relasi antarkelas.
3. Memfinalisasi kontrak method utama.
4. Menyepakati aliran data antarmodul.
5. Menyiapkan struktur folder dan file proyek.
6. Memastikan kebutuhan implementasi sesuai dengan rancangan.

**Target akhir Minggu 10:**

- Wireframe selesai dan telah dipresentasikan.
- Relasi class dan tanggung jawab disepakati.
- Kontrak method utama tersedia.
- Struktur proyek siap digunakan untuk implementasi.

### 20.4 Rincian Target Minggu 11

**Periode: 9–15 November 2026**

PIC utama: **Satya Firma Ashari**.

Fokus utama minggu ini adalah implementasi objek permainan dan mekanisme fisika dasar.

Pekerjaan:

1. Menentukan ukuran meja.
2. Menentukan radius bola.
3. Menentukan posisi dan area deteksi pocket.
4. Menentukan batas area permainan.
5. Mengembangkan `Ball` dan `Table`.
6. Membuat susunan awal bola 8-Ball dan 9-Ball.
7. Mengimplementasikan pergerakan bola.
8. Mengimplementasikan gesekan dan perlambatan.
9. Menentukan ambang kecepatan untuk menyatakan bola berhenti.
10. Mengimplementasikan tumbukan antarb bola.
11. Mengimplementasikan pantulan cushion.
12. Mengimplementasikan deteksi pocket.
13. Menguji bola tunggal, tumbukan dua bola, pantulan, dan pocket.

**Target akhir Minggu 11:**

- Meja dan bola dapat ditampilkan.
- Bola dapat bergerak.
- Gesekan dan perlambatan bekerja.
- Tumbukan dan pantulan dapat diamati.
- Bola dapat terdeteksi masuk pocket.
- Simulasi dasar dapat diuji.

### 20.5 Rincian Target Minggu 12

**Periode: 16–22 November 2026**

PIC utama: **Satya Firma Ashari dan Muhammad Argo Iman**, sesuai area pekerjaan.

Fokus utama minggu ini adalah implementasi kontrol pukulan dan evaluasi aturan dasar.

Pekerjaan Satya:

1. Mengembangkan arah cue.
2. Mengembangkan pengaturan power.
3. Mengimplementasikan input mouse.
4. Membuat indikator power yang terpisah dari arah bidikan.
5. Mengimplementasikan penguncian arah ketika power sedang diatur.
6. Mengimplementasikan tombol Space untuk membatalkan pengaturan power.
7. Menghasilkan `ShotCommand`.
8. Menyiapkan snapshot awal dan hasil fakta fisika untuk proses evaluasi.

Pekerjaan Argo:

1. Menyiapkan struktur evaluasi aturan dasar.
2. Mengembangkan evaluasi hasil pukulan.
3. Menghubungkan `ShotStartState` dan `ShotResult` dengan `GameRules`.
4. Menghasilkan `RuleOutcome`.
5. Menyiapkan evaluasi dasar 8-Ball dan 9-Ball.

Pengujian:

- Menguji arah cue.
- Menguji perubahan power tanpa mengubah arah.
- Menguji pembatalan power menggunakan Space.
- Menguji satu pukulan sampai seluruh bola berhenti.
- Menguji timeout ketika power sedang diatur.
- Menguji timeout ketika pemain tidak sedang mengatur power.

**Target akhir Minggu 12:**

- Pemain dapat menghasilkan perintah pukulan.
- Arah dan power dapat diatur secara terpisah.
- Pembatalan power bekerja.
- Hasil fisika dapat dicatat.
- Evaluasi aturan dasar dapat dilakukan.

### 20.6 Rincian Target Minggu 13

**Periode: 23–29 November 2026**

PIC utama: **Muhammad Argo Iman**.

Fokus utama minggu ini adalah integrasi siklus pertandingan dan aturan permainan.

Pekerjaan:

1. Mengintegrasikan controller, Cue, fisika, dan aturan melalui `MatchSession`.
2. Mengimplementasikan status dan pergantian giliran.
3. Mengimplementasikan timer per giliran.
4. Mengimplementasikan Pause dan Resume.
5. Mengimplementasikan Restart.
6. Mengimplementasikan foul dan scratch sesuai aturan proyek.
7. Mengimplementasikan ball-in-hand.
8. Mengimplementasikan kondisi akhir permainan 8-Ball.
9. Mengimplementasikan kondisi akhir permainan 9-Ball.
10. Menghubungkan hasil evaluasi dengan statistik pemain.
11. Menguji kondisi khusus break.
12. Menguji dua kelompok bola yang masuk bersamaan.
13. Menguji bola 8 atau bola 9 yang masuk bersama foul.

**Target akhir Minggu 13:**

- Siklus pertandingan dapat berjalan.
- Pergantian giliran berfungsi.
- Timer, Pause, dan Resume terhubung.
- Foul dan ball-in-hand dapat diproses.
- Kondisi kemenangan 8-Ball dan 9-Ball dapat dievaluasi.

### 20.7 Rincian Target Minggu 14

**Periode: 30 November–6 Desember 2026**

Fokus pekerjaan dibagi berdasarkan area masing-masing anggota.

**Satya Firma Ashari:**

1. Mengembangkan Bot Easy menggunakan strategi heuristik sederhana.
2. Memastikan Bot menghasilkan `ShotCommand`.
3. Memastikan Bot menggunakan alur simulasi dan evaluasi yang sama dengan pemain manusia.

**Rapid Akbar Sinatria:**

1. Menyelesaikan halaman aplikasi yang masuk scope.
2. Mengembangkan dan mengintegrasikan HUD.
3. Mengembangkan Pause Menu dan navigasi halaman.
4. Mengimplementasikan Windowed dan Fullscreen.
5. Menjaga rasio tampilan 16:9.
6. Mengintegrasikan AudioManager, musik, dan efek suara.
7. Menghubungkan tampilan dengan status pertandingan.

**Muhammad Argo Iman:**

1. Mengembangkan StorageManager.
2. Menyimpan dan membaca pengaturan aplikasi menggunakan TXT.
3. Menyimpan dan membaca riwayat pertandingan menggunakan TXT.
4. Mengintegrasikan `MatchRecord` dan struct data terkait.
5. Memastikan hasil pertandingan hanya disimpan satu kali setelah pertandingan selesai.

**Target akhir Minggu 14:**

- Bot Easy dapat bermain.
- Halaman dan HUD terintegrasi.
- Windowed dan Fullscreen dapat digunakan.
- Musik dan efek suara terintegrasi.
- Pengaturan dan riwayat lokal dapat dibaca serta disimpan.
- How to Play tersedia.

### 20.8 Rincian Target Minggu 15

**Periode: 7–13 Desember 2026**

PIC: **Seluruh anggota**.

Fokus utama minggu ini adalah integrasi final, pengujian, perbaikan bug, dan penyelesaian laporan.

Pekerjaan:

1. Mengintegrasikan seluruh modul ke dalam build final.
2. Menguji alur pertandingan 8-Ball dan 9-Ball.
3. Menguji Local Multiplayer dan Human vs Bot.
4. Menguji kontrol arah dan power.
5. Menguji timeout, Pause, Resume, dan Restart.
6. Menguji foul, scratch, ball-in-hand, dan kondisi kemenangan.
7. Menguji penyimpanan pengaturan dan riwayat.
8. Memperbaiki bug crash, mekanik, aturan, dan integrasi.
9. Memeriksa source code, aset, dan struktur folder.
10. Menyelesaikan laporan akhir.
11. Memeriksa diagram, kontrak method, WBS, dan hasil pengujian.
12. Menyiapkan build dan demo.
13. Melakukan pemeriksaan akhir oleh seluruh anggota.

**Target akhir Minggu 15 — 13 Desember 2026:**

- Build final dapat dijalankan.
- Fitur utama telah terintegrasi.
- Pengujian utama dan alternatif telah dilakukan.
- Bug prioritas telah diperbaiki.
- Source code dan aset telah dirapikan.
- Laporan akhir selesai.
- Dokumentasi dan berkas pengumpulan siap.
- Tidak ada pekerjaan wajib yang dijadwalkan setelah 13 Desember 2026.

### 20.9 Ketergantungan Pekerjaan

| Pekerjaan Awal | Pekerjaan Berikutnya | Alasan Ketergantungan |
|---|---|---|
| Scope dan kebutuhan sistem | Relasi class dan kontrak method | Struktur sistem harus mengikuti kebutuhan yang telah ditentukan. |
| Wireframe dan rancangan | Implementasi antarmuka | Implementasi menggunakan rancangan sebagai acuan. |
| Geometri meja dan objek bola | Simulasi fisika | Simulasi membutuhkan objek dan batas fisik yang tersedia. |
| Simulasi fisika | `ShotResult` | Fakta fisik harus tersedia sebelum hasil pukulan dapat dievaluasi. |
| `ShotCommand` dan `ShotStartState` | Integrasi pukulan | Sesi membutuhkan perintah dan snapshot sebelum simulasi. |
| `ShotResult` | `GameRules` | Evaluasi membutuhkan fakta hasil simulasi. |
| `RuleOutcome` | `MatchSession` | Sesi menerapkan hasil evaluasi terhadap status pertandingan. |
| Siklus pertandingan | Bot Easy dan UI terintegrasi | Bot dan UI harus mengikuti alur pertandingan yang sudah tersedia. |
| StorageManager dan struct data | Match History dan pengaturan | Halaman membutuhkan data yang dapat dibaca dan disimpan. |
| Integrasi modul | Pengujian menyeluruh | Pengujian alur lengkap membutuhkan modul yang telah terhubung. |
| Pengujian | Finalisasi | Perbaikan akhir dilakukan berdasarkan hasil pengujian. |

### 20.10 Indikator Penyelesaian Proyek

Proyek YouKnowBall dinyatakan siap diserahkan apabila memenuhi indikator berikut.

**A. Fitur Permainan**

- [ ] Main 8-Ball dapat dimulai dari Main Menu.
- [ ] Main 9-Ball dapat dimulai dari Main Menu.
- [ ] Local Multiplayer dapat dimainkan.
- [ ] Human vs Bot dapat dimainkan menggunakan Bot Easy.
- [ ] Pemain dapat mengarahkan cue stick.
- [ ] Pemain dapat mengatur power tembakan.
- [ ] Tombol Space dapat membatalkan pengaturan power.
- [ ] Prediksi lintasan sederhana dapat ditampilkan.
- [ ] Simulasi pergerakan bola berjalan dengan baik.
- [ ] Tumbukan dan pantulan bola berjalan dengan baik.
- [ ] Bola dapat masuk ke pocket.
- [ ] Sistem menunggu seluruh bola berhenti sebelum mengevaluasi hasil tembakan.
- [ ] Aturan 8-Ball dan 9-Ball berjalan sesuai rancangan.
- [ ] Foul, scratch, dan ball-in-hand dapat ditangani.
- [ ] Pergantian giliran berjalan sesuai hasil evaluasi.
- [ ] Timer berjalan sesuai pilihan pengguna.
- [ ] Timeout ditangani sesuai kondisi pemain ketika waktu habis.

**B. Fitur Antarmuka dan Pengaturan**

- [ ] Main Menu memiliki tombol Main 8-Ball dan Main 9-Ball secara langsung.
- [ ] Match Setup dapat digunakan.
- [ ] Pause Menu dapat digunakan.
- [ ] Restart memiliki konfirmasi.
- [ ] Kembali ke Main Menu dari pertandingan memiliki konfirmasi.
- [ ] Application Settings dapat digunakan.
- [ ] Pengaturan dapat diterapkan dan disimpan.
- [ ] Display Mode Windowed dan Fullscreen tersedia.
- [ ] Konten mempertahankan rasio 16:9.
- [ ] Result Page dapat menampilkan hasil pertandingan.
- [ ] Rematch dapat memulai pertandingan baru dengan konfigurasi sebelumnya.
- [ ] Match History dapat menampilkan daftar dan detail pertandingan.
- [ ] How to Play dapat menampilkan panduan permainan.
- [ ] Exit memiliki konfirmasi.

**C. Penyimpanan dan Finalisasi**

- [ ] Pengaturan aplikasi tersimpan dalam file TXT.
- [ ] Hasil pertandingan selesai tersimpan dalam file TXT.
- [ ] Pertandingan yang dihentikan melalui Restart tidak masuk ke Match History.
- [ ] Pertandingan yang ditinggalkan sebelum selesai tidak disimpan sebagai hasil pertandingan.
- [ ] Aplikasi dapat dikompilasi dan dijalankan.
- [ ] Tidak terdapat bug kritis yang menghalangi fitur utama.
- [ ] README dan dokumentasi sesuai dengan implementasi.
- [ ] Laporan akhir telah selesai.
- [ ] Seluruh berkas proyek siap dikumpulkan paling lambat 13 Desember 2026.

---

## 21. Kontrak Perilaku dan Ketentuan Integrasi

Bagian ini menetapkan perilaku yang harus dipenuhi setiap komponen ketika berinteraksi dengan komponen lain. Tujuannya adalah menjaga agar implementasi setiap anggota tetap konsisten meskipun dikerjakan secara terpisah.

### 21.1 Kontrak Perilaku Utama

| Proses | Prakondisi | Hasil yang Diharapkan |
|---|---|---|
| Memulai pertandingan | Konfigurasi pertandingan valid. | Pemain, controller, meja, giliran, timer, dan state awal disiapkan. |
| Menerima pukulan | Giliran valid, state mengizinkan, seluruh bola diam, perintah valid, dan waktu tersedia. | Snapshot kondisi dibuat, timer giliran berhenti selama simulasi, dan impuls diberikan. |
| Menolak pukulan | Salah satu prasyarat pukulan tidak terpenuhi. | Tidak ada impuls atau simulasi baru. |
| Menyelesaikan simulasi | Seluruh bola berhenti dan `ShotStartState` serta `ShotResult` tersedia. | `GameRules` menghasilkan `RuleOutcome`. |
| Foul/scratch | Hasil pukulan memenuhi kondisi foul yang telah ditetapkan. | Giliran berpindah dan lawan mendapat ball-in-hand. |
| Timeout tanpa power drag | Timer habis ketika pemain tidak sedang mengatur power. | Giliran berpindah tanpa foul dan tanpa ball-in-hand. |
| Timeout saat power drag | Timer habis ketika pemain sedang mengatur power. | Pukulan langsung dijalankan dengan power saat itu. |
| Pause | Pertandingan belum selesai. | Timer dan simulasi berhenti; state sebelumnya disimpan; input yang belum menjadi pukulan dibatalkan. |
| Resume | Sesi sedang paused. | State sebelumnya dan sisa timer dipulihkan. |
| Restart | Pemain mengonfirmasi restart. | Sesi aktif dibatalkan tanpa catatan hasil, lalu rack baru disiapkan. |
| Kembali ke menu | Pemain mengonfirmasi pembatalan pertandingan aktif. | Sesi dibatalkan dan tidak dicatat sebagai pertandingan selesai. |
| Simpan hasil | Pertandingan selesai dan hasil belum pernah disimpan. | Satu `MatchRecord` disimpan. |
| Rematch | Hasil pertandingan sebelumnya tersedia. | Pertandingan baru dimulai menggunakan konfigurasi sebelumnya. |
| Penempatan cue ball | Ball-in-hand aktif. | Posisi hanya diterima jika memenuhi validasi area, overlap, dan pocket. |
| Pengaturan aplikasi | Halaman Settings aktif. | Perubahan dapat diterapkan dan disimpan atau dibatalkan sebelum diterapkan. |

### 21.2 Batas Integrasi Antarsubsistem

- Controller menghasilkan `ShotCommand`; controller tidak menjalankan fisika.
- `MatchSession` memvalidasi perintah dan mengatur siklus pukulan.
- `Cue` mengubah arah dan power menjadi impuls.
- `PhysicsEngine` menjalankan simulasi dan mencatat fakta.
- `GameRules` mengevaluasi fakta dan mengembalikan `RuleOutcome`.
- `MatchSession` menerapkan hasil evaluasi pada pemain, giliran, timer, dan status pertandingan.
- `StorageManager` menyimpan hasil hanya setelah pertandingan selesai.
- `ScreenManager` menampilkan keadaan sistem kepada pemain.
- `AudioManager` memutar audio berdasarkan permintaan komponen yang memicu kejadian.
- Tidak ada controller yang boleh mengubah posisi atau kecepatan bola secara langsung.

### 21.3 Ketentuan Integrasi Pause dan Resume

1. Pause menghentikan timer pertandingan.
2. Pause menghentikan simulasi fisika.
3. Input drag yang belum menghasilkan pukulan harus dibatalkan.
4. Resume mengembalikan state pertandingan sebelumnya.
5. Resume memulihkan sisa timer, bukan mengatur ulang timer.
6. Resume tidak membuat `ShotStartState` baru untuk pukulan yang sudah diproses.
7. Resume tidak memberikan impuls kedua.
8. Pengaturan aplikasi yang dibuka dari Pause tidak boleh membuat simulasi atau timer berjalan kembali sebelum pengguna memilih Continue.

### 21.4 Ketentuan Penyimpanan Hasil

1. Hanya pertandingan yang telah selesai yang boleh disimpan sebagai `MatchRecord`.
2. Hasil pertandingan harus disimpan satu kali.
3. Restart tidak menghasilkan catatan pertandingan selesai.
4. Kembali ke Main Menu sebelum pertandingan selesai tidak menghasilkan catatan pertandingan selesai.
5. Rematch membuat sesi baru dan tidak menghapus catatan pertandingan sebelumnya.
6. `StorageManager` bertanggung jawab terhadap pembacaan dan penulisan data, bukan penentuan pemenang.

---

## 22. Pengujian Minimum

Pengujian dilakukan untuk memastikan setiap fitur berjalan sesuai rancangan. Pengujian dilakukan secara bertahap pada masing-masing modul dan dilanjutkan dengan pengujian integrasi.

| ID | Skenario Pengujian | Hasil yang Diharapkan |
|---|---|---|
| T01 | Membuka aplikasi dengan pengaturan default | Main Menu tampil tanpa error. |
| T02 | Memulai 8-Ball Local Multiplayer | Susunan 8-Ball tampil dengan dua pemain lokal. |
| T03 | Memulai 9-Ball Human vs Bot | Susunan 9-Ball tampil dengan Bot Easy sebagai lawan. |
| T04 | Menggerakkan mouse untuk membidik | Arah cue berubah sesuai input. |
| T05 | Mengatur power | Power berubah, arah bidikan tetap terkunci. |
| T06 | Menekan Space saat mengatur power | Power dibatalkan dan belum ada tembakan. |
| T07 | Melepas mouse secara normal | Satu pukulan dijalankan. |
| T08 | Pause saat drag belum selesai | Input dibatalkan dan tidak ada tembakan tak sengaja. |
| T09 | Timeout tanpa mengatur power | Giliran berpindah tanpa foul dan ball-in-hand. |
| T10 | Timeout saat mengatur power | Pukulan dijalankan dengan power saat itu. |
| T11 | Seluruh bola berhenti | Simulasi berakhir dan hasil dapat dievaluasi. |
| T12 | Cue ball masuk pocket | Scratch/foul tercatat. |
| T13 | Terjadi foul | Lawan mendapat giliran dan ball-in-hand. |
| T14 | Penempatan cue ball tidak valid | Posisi ditolak. |
| T15 | Solid dan Stripe masuk bersamaan saat meja terbuka | Kelompok belum ditetapkan dan meja tetap terbuka; kelompok baru ditentukan pada pukulan sah berikutnya yang memasukkan satu kelompok saja. |
| T16 | Bola 8 masuk sebelum kelompok sendiri habis | Pemain yang memukul kalah. |
| T17 | Bola 8 masuk bersama scratch/foul | Pemain yang memukul kalah. |
| T18 | Bola 8 masuk saat break | Bola 8 dikembalikan ke meja dan permainan dilanjutkan. |
| T19 | Bola 9 masuk secara sah | Pemain yang memukul menang. |
| T20 | Bola 9 masuk saat break | Bola 9 di-respot dan permainan dilanjutkan. |
| T21 | Bola 9 masuk bersama foul | Tidak menang; bola 9 di-respot dan foul diproses. |
| T22 | Bot mendapat giliran | Bot menghasilkan satu perintah lewat alur normal. |
| T23 | Pertandingan selesai | Result Page menampilkan data yang benar. |
| T24 | Membuka riwayat setelah pertandingan selesai | Record pertandingan muncul. |
| T25 | Mengubah audio dan sensitivitas | Nilai diterapkan dan tersimpan. |
| T26 | Resize Windowed | Rasio tetap 16:9 dan koordinat mouse tetap akurat. |
| T27 | Fullscreen pada layar non-16:9 | Letterbox/pillarbox digunakan dan konten tidak meregang. |
| T28 | File TXT tidak tersedia atau rusak | Sistem menggunakan default/riwayat kosong tanpa crash. |
| T29 | Restart atau membatalkan pertandingan | Pertandingan yang belum selesai tidak disimpan sebagai hasil. |
| T30 | Keluar melalui konfirmasi | Aplikasi hanya tertutup setelah pengguna menyetujui. |
| T31 | Rematch setelah pertandingan selesai | Pertandingan baru dimulai dengan konfigurasi sebelumnya. |
| T32 | Resume setelah Pause | State dan sisa timer dipulihkan tanpa mengulang impuls. |
| T33 | Membuka Settings dari Pause | Timer dan simulasi tetap berhenti. |
| T34 | Membatalkan perubahan Settings dengan Back | Perubahan yang belum diterapkan dibatalkan. |

### 22.1 Prioritas Pengujian

Jika waktu pengujian terbatas, urutan prioritas adalah:

1. Aplikasi dapat berjalan tanpa crash.
2. Pukulan, gerak bola, tumbukan, dan pocket bekerja.
3. Aturan inti dan penentuan pemenang benar.
4. Giliran, timer, Pause, Resume, dan ball-in-hand benar.
5. Bot Easy berfungsi melalui alur yang sama.
6. Navigasi dan halaman utama dapat digunakan.
7. Riwayat dan pengaturan tersimpan.
8. Audio, dekorasi, animasi, dan penyempurnaan visual.

---

## 23. Risiko dan Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| Fisika tidak stabil | Bola bergerak tidak wajar atau simulasi tidak berhenti. | Uji per kasus, kendalikan delta time, dan tetapkan ambang berhenti. |
| Method memiliki tanggung jawab tumpang tindih | Integrasi menjadi sulit dan logika tersebar. | Pertahankan batas `PhysicsEngine` = fakta, `GameRules` = keputusan, `MatchSession` = orkestrasi. |
| Input mouse salah setelah resize | Arah cue tidak sesuai posisi mouse. | Gunakan viewport dan konversi koordinat logis. |
| Bot terlalu kompleks | Waktu pengembangan tidak cukup. | Batasi strategi pada pemilihan target, arah, dan power sederhana. |
| File TXT gagal dibaca | Pengaturan atau riwayat tidak tersedia. | Tetapkan format data, validasi pembacaan, dan sediakan fallback. |
| Integrasi terlambat | Fitur tidak dapat diuji sebagai satu sistem. | Lakukan integrasi bertahap setiap minggu. |
| Perubahan arsitektur tanpa koordinasi | Class dan kontrak method tidak konsisten. | Komunikasikan perubahan kepada anggota terkait sebelum diterapkan. |
| Dekorasi menyita waktu | Mekanik inti terlambat selesai. | Dahulukan mekanik, aturan, dan fitur wajib. |
| Prediksi lintasan terlalu kompleks | Waktu implementasi meningkat. | Batasi prediksi pada cue ball sampai perkiraan tumbukan pertama dan arah sederhana bola objek. |
| Pengelolaan timer tidak konsisten | Timeout terjadi pada fase yang salah. | Uji timeout saat power ditarik, saat tidak menarik power, dan saat Pause. |

---

## 24. Kriteria Penyelesaian

Proyek YouKnowBall dinyatakan siap diserahkan apabila memenuhi kriteria berikut:

### 24.1 Kriteria Fungsional

- Aplikasi dapat dijalankan pada lingkungan yang disepakati.
- Mode 8-Ball dan 9-Ball dapat dimulai.
- Local Multiplayer dapat dimainkan.
- Human vs Bot dapat dimainkan menggunakan Bot Easy.
- Kontrol arah dan power berjalan sesuai ketentuan.
- Pembatalan power menggunakan Space berfungsi.
- Prediksi lintasan sederhana dapat ditampilkan.
- Simulasi bola, tumbukan, cushion, gesekan, dan pocket berjalan.
- Aturan inti, foul, scratch, giliran, ball-in-hand, dan kondisi kemenangan berjalan sesuai rancangan.
- Timer, timeout, Pause, Resume, dan Restart berjalan sesuai ketentuan.
- Hasil pertandingan ditampilkan dan disimpan ke TXT.
- Pengaturan aplikasi dapat disimpan dan dimuat.
- Match History dapat menampilkan daftar dan detail pertandingan.
- Windowed dan Fullscreen mempertahankan rasio konten 16:9.
- Halaman dan navigasi yang masuk scope dapat digunakan.

### 24.2 Kriteria Teknis

- Arsitektur mempertahankan 14 class utama dan 8 struct pendukung.
- Tanggung jawab setiap class tidak saling mengambil alih.
- Pemain manusia dan Bot menggunakan jalur pemrosesan pukulan yang sama.
- `ShotStartState` dibuat satu kali sebelum impuls.
- `ShotResult` berisi fakta fisik, bukan keputusan aturan.
- `RuleOutcome` berisi keputusan aturan.
- Hasil pertandingan tidak tersimpan lebih dari satu kali.
- Tidak terdapat bug kritis yang menghalangi fitur utama.

### 24.3 Kriteria Dokumentasi dan Pengumpulan

- README sesuai dengan rancangan dan implementasi.
- Class Diagram dan diagram pendukung telah diperiksa.
- Kontrak method telah disesuaikan dengan implementasi.
- WBS dan pembagian PIC telah diperiksa.
- Hasil pengujian minimum telah dicatat.
- Laporan akhir telah selesai.
- Source code, aset, build, dan berkas pendukung telah dirapikan.
- Seluruh pekerjaan selesai paling lambat **13 Desember 2026**.

---

## 25. Nilai Teknis yang Ditetapkan Saat Implementasi

Beberapa nilai teknis tidak perlu ditetapkan secara sembarang di dalam dokumen perencanaan. Nilai tersebut harus ditentukan melalui implementasi dan pengujian.

Nilai yang perlu ditentukan:

- Ukuran logis meja dan posisi bola awal.
- Radius bola dan pocket.
- Massa dan parameter fisika bola.
- Koefisien gesekan.
- Kekuatan pantulan cushion.
- Ambang kecepatan untuk menyatakan bola berhenti.
- Interval atau substep simulasi.
- Batas minimum dan maksimum power.
- Rumus sensitivitas mouse.
- Ukuran minimum window dengan rasio 16:9.
- Format file TXT dan delimiter.
- Perilaku sistem ketika file TXT rusak atau tidak ditemukan.
- Posisi respot bola 8 atau bola 9.
- Detail algoritma Bot Easy.
- Detail perhitungan prediksi lintasan.

Nilai tersebut sebaiknya dicatat sebagai konstanta atau konfigurasi internal. Jangan menjadikan seluruh nilai teknis sebagai pengaturan pengguna apabila tidak diperlukan.

---

## 26. Hal yang Belum Dikunci

Bagian ini membedakan keputusan yang sudah disepakati dari rincian yang masih perlu ditentukan. Hal yang belum dikunci tidak boleh dianggap sebagai fitur yang sudah selesai atau sebagai keputusan final.

### 26.1 Aturan Permainan

- Daftar lengkap kondisi foul selain scratch.
- Rincian break selain kasus khusus bola 8 dan bola 9 yang telah ditentukan.
- Detail posisi respot untuk bola yang harus dikembalikan ke meja.
- Penanganan kontak pertama yang terjadi hampir bersamaan.
- Aturan untuk kondisi permainan macet atau tidak mengalami kemajuan.
- Detail aturan tambahan yang mungkin diperlukan setelah pengujian.

### 26.2 Implementasi Teknis

- Nilai koefisien gesekan, restitusi, stop threshold, ukuran bola, skala meja, dan substep simulasi.
- Rumus sensitivitas mouse dan batas minimum/maksimum power.
- Algoritma rinci Bot Easy dan fallback jika target tidak tersedia.
- Detail perhitungan prediksi lintasan.
- Format TXT, delimiter, ID catatan, serta penanganan file hilang atau rusak.
- Definisi pasti statistik pukulan dan bola masuk.
- Aset visual, audio, font, serta lisensinya.
- Kecocokan versi SFML 2.4.2 dengan compiler dan toolchain yang digunakan.

### 26.3 Konsistensi Dokumen dan Implementasi

- Signature method dan tipe data final harus dicocokkan dengan implementasi.
- Relasi dan multiplicity Class Diagram harus diverifikasi berdasarkan kepemilikan objek yang benar-benar diterapkan.
- Daftar foul yang dicantumkan sebagai fitur harus sesuai dengan aturan yang benar-benar disepakati, diimplementasikan, dan diuji.
- Use Case Diagram dapat memisahkan tujuan pengguna seperti bermain, melihat riwayat, mengubah pengaturan, membaca panduan, dan keluar, walaupun README ini menggunakan satu skenario penggunaan menyeluruh.
- Pembagian PIC pada WBS harus tetap konsisten dengan pembagian tanggung jawab utama pada Bagian 19.

Hal yang belum dikunci tidak membatalkan scope yang sudah ditetapkan. Jangan menambahkan fitur baru hanya karena rincian teknisnya belum selesai.

---

## 27. Rujukan

1. Materi perkuliahan Desain dan Pemrograman Berorientasi Objek (DPBO): *Studi Kasus*. Digunakan sebagai acuan pendekatan Responsibility-Driven Design (RDD), CRC, dan rancangan berorientasi objek.
2. World Pool-Billiard Association. (2026, 21 Oktober). *WPA Rules*.  
   https://wpapool.com/wp-content/uploads/2026/10/WPA-Rules-2026-10-21-211.pdf

**Catatan rujukan:**

Dokumen WPA digunakan sebagai referensi aturan biliar. YouKnowBall menerapkan adaptasi aturan untuk ruang lingkup proyek, sehingga tidak semua ketentuan WPA otomatis diterapkan. Materi perkuliahan digunakan sebagai acuan pendekatan RDD, CRC, dan rancangan berorientasi objek.

---

## 28. Riwayat Perubahan

### Versi 04 — 11 November 2026

- Mengonsolidasikan dokumentasi proyek berdasarkan acuan v02, keputusan arsitektur dan kontrak method v03, serta keputusan tambahan yang telah disepakati.
- Memastikan scope YouKnowBall menggunakan 8-Ball, 9-Ball, Local Multiplayer, dan Bot Easy.
- Memastikan Main Menu menggunakan tombol langsung Main 8-Ball dan Main 9-Ball.
- Mempertahankan baseline 14 class utama dan 8 struct pendukung.
- Menyelaraskan hubungan antarkelas dan alur kolaborasi satu pukulan.
- Memperjelas pemisahan fakta fisika, evaluasi aturan, dan pengelolaan sesi pertandingan.
- Memperjelas skenario penggunaan dari Main Menu hingga keluar aplikasi.
- Menyelaraskan pembagian tanggung jawab anggota dengan PIC pada v03.
- Menyelaraskan WBS minggu 9–15 dengan urutan pekerjaan dan ketergantungan implementasi.
- Menambahkan kontrak perilaku, pengujian minimum, risiko, kriteria penyelesaian, dan hal yang belum dikunci.
- Memastikan target penyelesaian proyek dan laporan akhir adalah 13 Desember 2026.

### Versi 03 — 11 November 2026

- Memperjelas kontrak method dan batas tanggung jawab setiap class.
- Memperjelas data dan alur `ShotCommand`, `ShotStartState`, `ShotResult`, dan `RuleOutcome`.
- Menyelaraskan pembagian PIC berdasarkan area pekerjaan.
- Memperjelas urutan WBS minggu 9–15.
- Menambahkan ketentuan pengujian, risiko, dan integrasi.

### Versi 02 — 10 November 2026

- Mengonsolidasikan keputusan produk dan arsitektur dari dokumen acuan sebelumnya serta pembahasan lanjutan.
- Memastikan nama produk YouKnowBall, mode 8-Ball/9-Ball, Pemain Lokal/Bot Easy, pilihan timer, kontrol arah dan power terpisah, serta penyimpanan TXT tercatat konsisten.
- Mempertahankan baseline 14 class utama dan 8 struct pendukung.
- Menyempurnakan uraian CRC, Knowing, Doing, atribut, method utama, dan collaborator untuk seluruh class.
- Memperluas skenario penggunaan hingga mencakup pertandingan dan fitur pendukung aplikasi.
- Menambahkan pembagian peran anggota serta WBS minggu ke-9 sampai minggu ke-15.
- Memisahkan keputusan yang telah ditetapkan dari rincian yang masih perlu dikonfirmasi.

### Versi 01 — 8 November 2026

Dokumen acuan awal yang mengonsolidasikan ruang lingkup, kontrol, aturan dasar, arsitektur 14 class, 8 struct, alur pukulan, dan skenario penggunaan.

---

**Acuan utama proyek YouKnowBall — Kelompok 9.**

Gunakan dokumen ini sebagai referensi bersama selama pengembangan. Jika terdapat keputusan baru yang disepakati, perbarui bagian terkait dan riwayat perubahan agar seluruh anggota menggunakan acuan versi yang sama.

# YouKnowBall — README Proyek

> **Versi:** 05 (ringkasan konsolidasi)  
> **Mata kuliah:** Desain dan Pemrograman Berorientasi Objek (DPBO)  
> **Kelompok:** 9  
> **Anggota:** Rapid Akbar Sinatria, Muhammad Argo Iman, Satya Firma Ashari  
> **Teknologi:** C++ · SFML 2.4.2 · PC/Desktop  
> **Produk:** Game biliar 2D top-down  
> **Target akhir proyek:** 13 Desember 2026

YouKnowBall adalah permainan biliar 2D dengan mode **8-Ball** dan **9-Ball**. Pemain dapat bermain melawan pemain lokal lain pada satu perangkat atau melawan **Bot Easy**. README ini menjadi acuan bersama untuk ruang lingkup, perilaku permainan, antarmuka, arsitektur OOP, kontrak integrasi, pembagian kerja, dan pengujian.

**Status:** dokumen ini menjelaskan rancangan yang disepakati, bukan bukti bahwa fitur sudah selesai dibuat atau diuji. Hal yang belum diputuskan ditandai sebagai **Belum dikunci** atau **Ditentukan saat implementasi**. Jangan menganggap contoh teknis sebagai keputusan final.

## Daftar Isi

1. [Identitas dan prinsip rancangan](#1-identitas-dan-prinsip-rancangan)
2. [Ruang lingkup](#2-ruang-lingkup)
3. [Halaman dan navigasi](#3-halaman-dan-navigasi)
4. [Konfigurasi pertandingan](#4-konfigurasi-pertandingan)
5. [Kontrol, timer, dan giliran](#5-kontrol-timer-dan-giliran)
6. [Aturan permainan](#6-aturan-permainan)
7. [Prediksi lintasan dan Bot Easy](#7-prediksi-lintasan-dan-bot-easy)
8. [Hasil, riwayat, dan pengaturan](#8-hasil-riwayat-dan-pengaturan)
9. [Arsitektur: 14 class](#9-arsitektur-14-class)
10. [Delapan struct dan enum](#10-delapan-struct-dan-enum)
11. [Relasi dan alur satu pukulan](#11-relasi-dan-alur-satu-pukulan)
12. [Use case ringkas](#12-use-case-ringkas)
13. [Pembagian peran](#13-pembagian-peran)
14. [WBS Minggu 9–15](#14-wbs-minggu-915)
15. [Kontrak integrasi dan pengujian](#15-kontrak-integrasi-dan-pengujian)
16. [Risiko dan kriteria selesai](#16-risiko-dan-kriteria-selesai)
17. [Hal yang belum dikunci](#17-hal-yang-belum-dikunci)
18. [Rujukan dan riwayat](#18-rujukan-dan-riwayat)

---

## 1. Identitas dan prinsip rancangan

### 1.1 Identitas proyek

| Elemen | Ketetapan |
|---|---|
| Nama | YouKnowBall |
| Kelompok | 9 |
| Anggota | Rapid Akbar Sinatria; Muhammad Argo Iman; Satya Firma Ashari |
| Bahasa/library | C++ dan SFML 2.4.2 |
| Platform | PC/Desktop |
| Jenis | Biliar 2D top-down |
| Mode | 8-Ball dan 9-Ball |
| Lawan | Pemain lokal atau Bot Easy |

### 1.2 Prinsip OOP

Rancangan memakai **Responsibility-Driven Design (RDD)** dan CRC (Class–Responsibility–Collaborator). Setiap class harus memiliki tanggung jawab yang jelas: informasi yang dikelola (*knowing*), tindakan yang dilakukan (*doing*), dan kolaborator yang diperlukan.

Prinsip wajib:
- Pertahankan baseline **14 class utama dan 8 struct pendukung**. Penambahan class/struct harus memiliki alasan teknis dan disepakati tim.
- Jangan membuat class hanya untuk setiap tombol, halaman, atau elemen visual.
- Gabungkan fungsi yang sejenis selama tanggung jawabnya tetap jelas.
- Pisahkan simulasi fisika, evaluasi aturan, pengelolaan pertandingan, input, tampilan, dan penyimpanan.
- Pemain manusia dan Bot harus memakai jalur eksekusi pukulan yang sama.
- Detail yang belum disepakati tetap ditandai, bukan diasumsikan final.

## 2. Ruang lingkup

### 2.1 Termasuk

- Mode 8-Ball dan 9-Ball.
- Dua pemain lokal bergantian pada satu perangkat.
- Satu pemain melawan Bot Easy.
- Pengaturan nama pemain dan timer per giliran.
- Kontrol arah dan power pukulan yang terpisah.
- Meja, bola, cue, enam pocket, dan cushion.
- Gerak bola, gesekan/perlambatan, tumbukan, pantulan, dan deteksi pocket.
- Evaluasi aturan, pergantian giliran, foul, scratch, ball-in-hand, serta kondisi menang.
- Prediksi lintasan sederhana.
- Pause, resume, restart, rematch, dan kembali ke Main Menu.
- Results Screen, Match History, App Settings, How to Play.
- Penyimpanan pengaturan dan pertandingan selesai ke file TXT lokal.

### 2.2 Tidak termasuk

Multiplayer online/LAN, akun/login, server atau database eksternal, matchmaking, Bot Normal/Hard, Pocket Challenge, spin shot, jump shot, replay, turnamen, dan melanjutkan pertandingan yang belum selesai setelah aplikasi ditutup.

### 2.3 Batas ruang lingkup

Nilai fisika, strategi Bot, format detail TXT, dan parameter teknis dapat dipilih saat implementasi. Penyesuaian tersebut tidak dianggap fitur baru jika tetap berada dalam ruang lingkup di atas.

## 3. Halaman dan navigasi

### 3.1 Main Menu

Tombol utama:
1. **Main 8-Ball** — langsung memilih mode 8-Ball.
2. **Main 9-Ball** — langsung memilih mode 9-Ball.
3. **Match History**
4. **App Settings**
5. **How to Play**
6. **Exit** — tampilkan konfirmasi sebelum keluar.

Pemilihan mode dilakukan di Main Menu. **Jangan** menggantinya dengan satu tombol Start Match yang baru meminta pilihan 8-Ball/9-Ball di halaman berikutnya.

### 3.2 Match Setup

Dibuka setelah mode dipilih. Pemain mengatur jenis lawan (Pemain Lokal/Bot Easy), nama pemain, dan timer (Unlimited/15/30/60 detik), lalu memulai pertandingan atau kembali ke Main Menu. Mode permainan yang dipilih tetap ditampilkan dan tidak dipilih ulang.

### 3.3 Game Screen

Tampilkan meja, bola, pocket, cue, indikator arah, indikator power terpisah, prediksi lintasan, nama pemain aktif, kelompok bola/status mode, timer (jika aktif), dan akses Pause.

### 3.4 Pause Menu

Diakses dengan Esc. Pilihan: **Continue**, **Settings**, **Restart**, dan **Main Menu**. Restart dan Main Menu meminta konfirmasi. Selama Pause, simulasi dan timer berhenti.

### 3.5 Results Screen

Tampilkan pemenang, ringkasan/statistik pertandingan, serta **Rematch** dan **Main Menu**.

### 3.6 Match History, Settings, dan How to Play

- **Match History:** daftar pertandingan selesai dan tampilan detail catatan pertandingan.
- **Settings:** volume musik, volume SFX, sensitivitas mouse, dan Display Mode (Windowed/Fullscreen).
- **How to Play:** petunjuk kontrol dan ringkasan aturan 8-Ball/9-Ball.
- **Exit:** konfirmasi sebelum aplikasi ditutup.

`ScreenManager` mengelola perpindahan halaman; tidak perlu class terpisah untuk tiap halaman.

## 4. Konfigurasi pertandingan

Dua konfigurasi lawan:
- **Pemain Lokal:** dua orang menggunakan satu perangkat dan bergantian.
- **Bot Easy:** satu pemain manusia melawan Bot Easy.

Nama pemain diatur sebelum pertandingan. Timer per giliran: **Unlimited, 15, 30, atau 60 detik**. Konfigurasi aktif disimpan sebagai `MatchConfig`.

**Rematch** dari Results Screen membuat pertandingan baru dengan konfigurasi sebelumnya (mode, lawan, nama, timer) tanpa mengubahnya. Hasil pertandingan sebelumnya tetap tersimpan. Hasil baru disimpan setelah pertandingan baru selesai.

**Restart** dari Pause memulai ulang pertandingan aktif dengan konfigurasi yang sama. Pertandingan yang dibatalkan melalui Restart atau kembali ke Main Menu tidak dicatat sebagai pertandingan selesai.

## 5. Kontrol, timer, dan giliran

### 5.1 Kontrol pukulan

- Cue stick di meja menunjukkan arah bidikan. Pemain mengatur arah dengan klik/tahan dan menggerakkan mouse.
- Power diatur melalui **indikator/kontrol terpisah berbentuk cue stick di layar**, bukan dengan menarik cue stick yang berada di meja.
- Saat mengatur power, tekan **Space** untuk membatalkan proses power sebelum mouse dilepas; setelah batal pemain dapat mengatur arah lagi.
- Ketika perintah pukulan sah diterima, controller menghasilkan `ShotCommand`; proses selanjutnya ditangani oleh `MatchSession` dan subsistem terkait.

### 5.2 Timer dan timeout

- Timer berjalan pada giliran pemain aktif.
- **Unlimited** tidak memiliki batas waktu.
- Pause menghentikan timer dan simulasi; Resume melanjutkan dengan sisa waktu yang sama, bukan mengatur ulang timer.
- Jika timeout terjadi saat pemain **tidak** sedang mengatur power, giliran berpindah langsung. Timeout ini **bukan foul** dan tidak memberikan ball-in-hand.
- Jika timeout terjadi saat pemain **sedang** mengatur power, sistem langsung melepas/menjalankan pukulan dengan power yang sudah tercapai saat timeout.
- Timer giliran baru dimulai sesuai siklus giliran setelah proses pukulan sebelumnya selesai dan hasilnya dievaluasi.

### 5.3 Siklus giliran

Pemain melakukan input → pukulan dieksekusi → semua bola harus berhenti → aturan dievaluasi → hasil diterapkan (giliran, foul, ball-in-hand, atau akhir pertandingan) → giliran berikutnya dimulai jika pertandingan berlanjut.

## 6. Aturan permainan

### 6.1 Aturan umum

- Evaluasi hasil pukulan dilakukan setelah seluruh bola berhenti.
- `PhysicsEngine` hanya mencatat fakta fisika; `GameRules` memutuskan konsekuensi aturan.
- YouKnowBall mengadaptasi aturan biliar untuk kebutuhan proyek; jangan mengklaim implementasi penuh seluruh detail regulasi WPA jika belum dibuat.
- Foul yang belum disepakati secara rinci tidak boleh ditambahkan sebagai keputusan final tanpa persetujuan tim.

### 6.2 8-Ball

- Bola dibagi menjadi kelompok **solid (1–7)** dan **stripe (9–15)**; bola 8 adalah bola target akhir.
- Kelompok pemain ditentukan dari bola solid/stripe pertama yang masuk secara sah setelah meja terbuka.
- Jika kedua kelompok masuk bersamaan pada kondisi meja masih terbuka, meja tetap terbuka/tidak menetapkan kelompok sampai ada keputusan sah berikutnya.
- Pemain harus menyelesaikan kelompoknya sebelum memasukkan bola 8 sesuai aturan adaptasi proyek.
- Memasukkan bola 8 sebelum waktunya atau pada kondisi yang ditetapkan sebagai kekalahan menyebabkan pemain kalah.
- Detail break dan kondisi khusus bola 8 yang belum dipastikan tetap **Belum dikunci**.

### 6.3 9-Ball

- Bola sasaran pertama yang wajib terkena adalah bola bernomor paling kecil yang masih berada di meja.
- Pemain dapat memenangkan pertandingan dengan memasukkan bola 9 secara sah.
- Jika bola 9 masuk bersamaan dengan foul, keputusan kemenangan tidak boleh diberikan; terapkan konsekuensi foul dan penempatan ulang bola 9 sesuai aturan adaptasi.
- Bola 9 yang masuk pada break di-*re-spot* (dikembalikan ke posisi penempatan yang ditentukan), bukan langsung menjadi kemenangan.

### 6.4 Foul, scratch, dan ball-in-hand

- **Scratch** berarti cue ball masuk pocket; ini merupakan foul.
- Foul menyebabkan giliran berpindah kepada lawan.
- Setelah scratch/foul yang memenuhi ketentuan, lawan memperoleh **ball-in-hand**.
- Ball-in-hand pada rancangan ini mengizinkan cue ball ditempatkan bebas di area meja yang diperbolehkan oleh validasi posisi.
- Daftar foul lengkap dan rincian pengecualian masih perlu dikunci; jangan mengarang daftar final.

## 7. Prediksi lintasan dan Bot Easy

### 7.1 Prediksi lintasan

Prediksi lintasan merupakan bantuan visual untuk memperkirakan arah gerak cue ball dan/atau bola sasaran berdasarkan arah dan power saat ini. Prediksi bersifat visual, bukan jaminan hasil simulasi. Kompleksitas dan akurasi prediksi ditentukan saat implementasi.

### 7.2 Bot Easy

Bot Easy hanya tersedia sebagai lawan satu pemain manusia. Bot membaca keadaan meja dan memilih tindakan sederhana, lalu mengirim perintah melalui jalur `ShotCommand` yang sama dengan pemain manusia. Bot tidak boleh memiliki jalur simulasi fisika atau evaluasi aturan tersendiri.

Strategi, tingkat akurasi, dan algoritma pemilihan tembakan Bot Easy ditentukan saat implementasi. Bot Normal/Hard berada di luar ruang lingkup.

## 8. Hasil, riwayat, dan pengaturan

### 8.1 Hasil dan riwayat

`MatchRecord` menyimpan informasi pertandingan yang telah selesai, setidaknya identitas/nama pemain, mode, lawan, pemenang, dan ringkasan statistik yang disepakati. `StorageManager` menyimpan dan membaca riwayat lokal dari file TXT. Pertandingan yang belum selesai atau dibatalkan tidak masuk Match History.

### 8.2 Pengaturan aplikasi

`AppSettings` mencakup:
- volume musik;
- volume efek suara (SFX);
- sensitivitas mouse;
- Display Mode: Windowed atau Fullscreen.

Windowed mempertahankan rasio konten **16:9** tanpa peregangan; ukuran jendela dapat diubah dengan tetap menjaga rasio. Fullscreen juga didukung. Nilai teknis ukuran minimum, resolusi, dan implementasi resize ditetapkan saat implementasi.

### 8.3 Settings saat pertandingan

Settings dapat dibuka dari Main Menu maupun Pause Menu. Jika dibuka dari Pause, pertandingan dan timer tetap berhenti. **Apply/Save** menyimpan perubahan ke TXT; **Back** membuang perubahan yang belum diterapkan dan kembali ke Pause. Pengaturan yang disimpan berlaku sesuai mekanisme aplikasi.

## 9. Arsitektur: 14 class

Jumlah class utama dipertahankan tepat **14**. Nama class dan batas tanggung jawab berikut menjadi baseline.

| Class | Tanggung jawab utama | Kolaborator/kontrak penting |
|---|---|---|
| `GameApp` | Siklus hidup aplikasi, inisialisasi, loop utama, shutdown. | `ScreenManager`, `StorageManager`, `AudioManager`. |
| `ScreenManager` | Halaman, navigasi, input antarmuka, render UI. | `GameApp`, `MatchSession`, `StorageManager`, `AudioManager`. |
| `MatchSession` | State pertandingan, pemain aktif, giliran, timer, orkestrasi pukulan, hasil akhir. | `Player`, controller, `Table`, `Cue`, `PhysicsEngine`, `GameRules`, `StorageManager`. |
| `Player` | Identitas, nama, kelompok bola, dan statistik pemain. | `MatchSession`; bukan pengolah input atau strategi. |
| `PlayerController` (abstract) | Kontrak umum untuk memperoleh tindakan pemain. | Diimplementasikan oleh `HumanController` dan `BotController`. |
| `HumanController` | Mengolah input manusia menjadi arah/power dan `ShotCommand`. | `PlayerController`, `Cue`, konteks permainan. |
| `BotController` | Memilih tembakan sederhana untuk Bot Easy. | `PlayerController`, `Table`, `Player`, `Cue`; menghasilkan `ShotCommand`. |
| `Table` | Menyimpan/mengelola bola, pocket, batas meja, dan validasi posisi. | `Ball`, `PocketData`, `PhysicsEngine`, `GameRules`. |
| `Ball` | Posisi, kecepatan, radius, status aktif/masuk pocket, dan data fisik bola. | Dikelola melalui `Table` dan diproses `PhysicsEngine`. |
| `Cue` | Arah bidikan, power, impulse, dan kalkulasi prediksi lintasan. | Controller, `MatchSession`, `PhysicsEngine` melalui perintah tembakan. |
| `PhysicsEngine` | Integrasi gerak, gesekan, tumbukan, pantulan cushion, dan deteksi pocket. | Mengakses bola melalui `Table`; menghasilkan fakta `ShotResult`. |
| `GameRules` | Evaluasi 8-Ball/9-Ball, foul, kelompok, ball-in-hand, dan kemenangan. | `Table`, `Player`, `ShotStartState`, `ShotResult`; menghasilkan `RuleOutcome`. |
| `StorageManager` | Baca/tulis `AppSettings` dan `MatchRecord` ke file lokal. | `GameApp`, `MatchSession`. |
| `AudioManager` | Musik dan efek suara berdasarkan permintaan sistem. | `GameApp`, `ScreenManager`, subsistem pemicu audio. |

### 9.1 Batas tanggung jawab

- `GameApp` tidak mengelola aturan permainan.
- `ScreenManager` tidak menghitung fisika.
- `MatchSession` tidak mengolah raw mouse input atau menghitung collision.
- `Player` tidak menentukan strategi Bot dan tidak membaca input.
- `PlayerController` menghasilkan perintah, bukan menjalankan simulasi.
- `Cue` menghitung parameter tembakan, bukan memutuskan foul/pemenang.
- `PhysicsEngine` tidak menentukan foul, pemenang, atau pergantian giliran.
- `GameRules` tidak menjalankan simulasi fisika atau menyimpan file.
- `StorageManager` tidak mengambil keputusan gameplay.
- `AudioManager` tidak menentukan kapan suatu peristiwa gameplay terjadi.

## 10. Delapan struct dan enum

### 10.1 Delapan struct

| Struct | Fungsi |
|---|---|
| `MatchConfig` | Konfigurasi mode, lawan, nama pemain, dan timer pertandingan. |
| `AppSettings` | Nilai pengaturan aplikasi. |
| `MatchRecord` | Data hasil pertandingan selesai dan statistik ringkas. |
| `PocketData` | Posisi, ukuran, dan data pocket meja. |
| `ShotCommand` | Perintah tembakan dari controller (arah dan power/parameter tembakan). |
| `ShotStartState` | Snapshot kondisi yang diambil tepat sebelum impulse diberikan. |
| `ShotResult` | Fakta hasil simulasi satu pukulan; tidak memuat keputusan aturan. |
| `RuleOutcome` | Hasil evaluasi aturan untuk diterapkan oleh `MatchSession`. |

Struct adalah wadah data; jangan memindahkan tanggung jawab proses kompleks ke dalamnya tanpa alasan.

### 10.2 Enum pendukung

Enum yang digunakan sebagai tipe status/pilihan:
- `GameType`
- `OpponentType`
- `DisplayMode`
- `ScreenType`
- `MatchState`
- `BallGroup`
- `FoulType`
- `SoundType`

Enum bukan class atau struct dan tidak dihitung dalam baseline 14 class/8 struct. Nilai anggota enum ditentukan mengikuti kebutuhan implementasi dan konsistensi seluruh modul.

## 11. Relasi dan alur satu pukulan

### 11.1 Relasi utama

- `GameApp` mengoordinasikan layanan aplikasi; `ScreenManager` mengelola tampilan.
- `MatchSession` mengoordinasikan objek pertandingan: pemain, controller, meja, cue, fisika, dan aturan.
- `HumanController` dan `BotController` mewarisi `PlayerController`.
- `Table` mengelola kumpulan `Ball` dan data pocket (`PocketData`).
- `PhysicsEngine` mengubah kondisi fisik bola melalui `Table`; jangan menggambarkan seolah-olah engine memiliki siklus hidup bola terpisah.
- `GameRules` membaca fakta snapshot dan hasil simulasi untuk menghasilkan `RuleOutcome`.
- `StorageManager` menangani `AppSettings` dan `MatchRecord`; `AudioManager` menangani pemutaran audio.

Relasi pada diagram harus mencerminkan struktur anggota dan siklus hidup objek yang benar-benar diimplementasikan. Gunakan komposisi hanya jika objek memang dimiliki dan siklus hidupnya bergantung pada pemilik; relasi “menggunakan/mengelola” tidak otomatis berarti komposisi.

### 11.2 Alur satu pukulan

1. Controller aktif memperoleh input manusia atau keputusan Bot dan membentuk `ShotCommand`.
2. `MatchSession` memvalidasi bahwa fase pertandingan mengizinkan tembakan.
3. Tepat sebelum tembakan, `MatchSession` mengambil satu `ShotStartState`.
4. `Cue` mengubah arah dan power menjadi impulse/parameter tembakan final.
5. `PhysicsEngine` menerapkan impulse dan menjalankan simulasi.
6. `PhysicsEngine` mencatat fakta fisik (gerak, kontak, pantulan, bola masuk pocket) ke `ShotResult`.
7. Sistem menunggu sampai seluruh bola berhenti.
8. `GameRules` mengevaluasi `ShotStartState`, `ShotResult`, dan keadaan meja/pemain, lalu menghasilkan `RuleOutcome`.
9. `MatchSession` menerapkan hasil: foul, ball-in-hand, kelompok, re-spot, giliran, atau status menang/kalah.
10. Jika pertandingan berakhir, `MatchSession` membuat dan meminta `StorageManager` menyimpan satu `MatchRecord`.

### 11.3 Kontrak snapshot, impulse, dan resume

- Snapshot diambil **sekali** sebelum impulse pada satu pukulan.
- Resume tidak boleh mengambil snapshot baru atau menerapkan impulse ulang.
- `ShotResult` berisi fakta fisika, bukan kesimpulan aturan.
- `RuleOutcome` berisi keputusan aturan, bukan hasil perhitungan collision.
- Pukulan manusia dan Bot melewati alur yang sama setelah `ShotCommand` terbentuk.

## 12. Use case ringkas

**Aktor:** Pemain (manusia); Bot Easy berperan sebagai pengendali lawan otomatis pada mode Bot.

### 12.1 Memulai pertandingan

1. Pemain menjalankan aplikasi dan melihat Main Menu.
2. Pemain memilih **Main 8-Ball** atau **Main 9-Ball**.
3. Sistem membuka Match Setup untuk mode tersebut.
4. Pemain memilih Pemain Lokal atau Bot Easy, mengisi nama, dan memilih timer.
5. Pemain memulai pertandingan; sistem menyiapkan meja, pemain, controller, dan state awal.

### 12.2 Melakukan tembakan dan pergantian giliran

1. Pemain mengatur arah menggunakan cue di meja.
2. Pemain mengatur power melalui kontrol power terpisah.
3. Pemain menjalankan tembakan; sistem mensimulasikan sampai semua bola berhenti.
4. Sistem mengevaluasi aturan dan memperbarui status, giliran, timer, atau ball-in-hand.
5. Pada mode Bot, Bot memilih tembakan dan mengirimkannya melalui jalur perintah yang sama.

### 12.3 Timeout dan Pause

- Timeout saat tidak mengatur power: giliran berpindah, bukan foul, tanpa ball-in-hand.
- Timeout saat mengatur power: tembakan dijalankan dengan power yang tercapai.
- Esc membuka Pause Menu; Continue melanjutkan simulasi/timer dari kondisi tersimpan.
- Settings dari Pause tidak menjalankan pertandingan di latar belakang.
- Restart atau kembali ke Main Menu meminta konfirmasi.

### 12.4 Akhir pertandingan dan fitur lain

- Setelah kondisi menang terpenuhi, Results Screen menampilkan pemenang dan ringkasan.
- Rematch memulai pertandingan baru dengan konfigurasi sebelumnya; hasil lama tetap tersimpan.
- Match History menampilkan pertandingan selesai beserta detail.
- Settings dapat dibuka dari Main Menu.
- How to Play menampilkan petunjuk.
- Exit menutup aplikasi setelah konfirmasi.

## 13. Pembagian peran

PIC adalah penanggung jawab utama area, bukan berarti anggota lain dilarang membantu. Integrasi dan pengujian tetap dilakukan bersama.

| Anggota | Fokus/PIC | Area utama |
|---|---|---|
| **Rapid Akbar Sinatria** | UI, window, audio | `ScreenManager`, halaman, HUD, navigasi, display mode, `AudioManager`. |
| **Satya Firma Ashari** | Fisika dan kontrol tembakan | `Ball`, `Table`, `PhysicsEngine`, `Cue`, kontrol tembakan, Bot Easy. |
| **Muhammad Argo Iman** | Data pemain, aturan, dan alur pertandingan | `Player`, `GameRules`, `MatchSession`, giliran/timer, ball-in-hand, `StorageManager`. |

Semua anggota berkolaborasi pada kontrak antarmodul, integrasi, pengujian, perbaikan bug, dokumentasi, dan demo. Perubahan pembagian PIC perlu dikomunikasikan agar tidak ada modul tanpa penanggung jawab.

## 14. WBS Minggu 9–15

Tanggal mengikuti penyesuaian jadwal terbaru. PIC menunjukkan pemimpin pekerjaan; kolaborasi tim tetap berlaku.

| Minggu | Periode | Target dan hasil utama | PIC/fokus |
|---|---|---|---|
| 9 | **1–4 Nov 2026** | Finalisasi scope, kebutuhan, skenario/use case, baseline class/struct, dan pembagian kerja. | Argo; seluruh tim menyepakati. |
| 10 | **5–8 Nov 2026** | Relasi class, kontrak method, struktur proyek, rancangan UI/wireframe dan presentasinya. | Argo (arsitektur); Rapid (UI); kolaborasi. |
| 11 | 9–15 Nov 2026 | Fondasi `Ball`, `Table`, pocket/geometri, gerak, gesekan, tumbukan, dan cushion. | Satya. |
| 12 | 16–22 Nov 2026 | `Cue`, `HumanController`, `ShotCommand`, alur tembakan, hasil simulasi, dan aturan dasar. | Satya dan Argo. |
| 13 | 23–29 Nov 2026 | `MatchSession`, giliran, timer, pause/resume, foul, ball-in-hand, dan hasil pertandingan. | Argo; integrasi tim. |
| 14 | 30 Nov–6 Des 2026 | Bot Easy, halaman/HUD, display mode, `StorageManager`, history, `AudioManager`, How to Play. | Rapid (UI/audio); Satya (Bot); Argo (storage/aturan). |
| 15 | **7–13 Des 2026** | Integrasi akhir, pengujian skenario, perbaikan bug, laporan, demo, dan pengumpulan. | Seluruh anggota. |

### 14.1 Ketergantungan pekerjaan

- UI pertandingan memerlukan kontrak `MatchSession` dan data permainan yang stabil.
- Controller memerlukan kontrak `ShotCommand` dan `Cue`.
- Evaluasi aturan memerlukan fakta `ShotResult` dan snapshot `ShotStartState`.
- Bot harus memakai jalur tembakan yang sudah digunakan HumanController.
- History memerlukan format `MatchRecord` dan integrasi `StorageManager`.
- Pengujian end-to-end dilakukan setelah modul inti terintegrasi.

## 15. Kontrak integrasi dan pengujian

### 15.1 Kontrak integrasi

- Semua modul menggunakan nama tipe, enum, dan kontrak data yang disepakati.
- Controller hanya menghasilkan perintah tembakan; `MatchSession` mengatur kapan perintah boleh dijalankan.
- Snapshot diambil sekali sebelum impulse.
- Physics mencatat fakta; Rules memutuskan; MatchSession menerapkan.
- Semua bola harus berhenti sebelum hasil pukulan dievaluasi.
- Pause menghentikan timer dan simulasi; Resume melanjutkan tanpa mengulang pukulan.
- Hasil pertandingan disimpan satu kali hanya ketika pertandingan selesai.
- Settings dari Pause tidak boleh membuat timer atau simulasi berjalan.
- Perubahan struktur class/struct atau method bersama harus dikomunikasikan sebelum integrasi.

### 15.2 Pengujian minimum

| Area | Skenario minimum |
|---|---|
| Navigasi | Main Menu ke 8-Ball/9-Ball, Setup, History, Settings, How to Play, Exit. |
| Konfigurasi | Pemain Lokal/Bot Easy, nama, semua pilihan timer. |
| Kontrol | Arah, power terpisah, Space membatalkan power, tembakan sah. |
| Fisika | Gerak, perlambatan, tumbukan bola, cushion, pocket, bola berhenti. |
| Aturan | 8-Ball, 9-Ball, kelompok, foul/scratch, ball-in-hand, menang/kalah. |
| Timer | Unlimited, timeout saat idle, timeout saat power aktif. |
| Pause | Pause/resume mempertahankan sisa timer dan tidak mengulang impulse. |
| Bot | Bot menghasilkan `ShotCommand` melalui alur yang sama. |
| Hasil/storage | Hasil selesai tersimpan sekali; pertandingan dibatalkan tidak tersimpan. |
| Settings | Save/Apply, Back membuang perubahan, Windowed/Fullscreen. |
| Integrasi | Satu pertandingan penuh untuk 8-Ball dan 9-Ball pada kedua jenis lawan. |

Jika waktu terbatas, prioritaskan alur satu pukulan, aturan dan pergantian giliran, timeout, pause/resume, penyimpanan hasil, serta satu pertandingan penuh per mode.

## 16. Risiko dan kriteria selesai

### 16.1 Risiko dan mitigasi

| Risiko | Mitigasi |
|---|---|
| Tanggung jawab class tumpang tindih | Ikuti tabel 14 class dan kontrak integrasi. |
| Physics dan Rules tercampur | Physics hanya menghasilkan fakta; Rules mengevaluasi. |
| Perbedaan kontrak antanggota | Sepakati header, tipe data, dan method sebelum integrasi. |
| Timer/pause menyebabkan state tidak konsisten | Uji timeout idle, timeout saat power, dan resume. |
| Aturan belum lengkap | Tandai TBD dan sepakati sebelum implementasi aturan terkait. |
| Integrasi terlambat | Integrasikan modul bertahap dan uji kontrak sejak awal. |
| Data TXT rusak/tidak terbaca | Validasi input file dan sediakan perilaku saat file belum tersedia/tidak valid. |

### 16.2 Kriteria selesai

Proyek dapat dinyatakan memenuhi target apabila:
- Mode 8-Ball dan 9-Ball dapat dimainkan.
- Pemain Lokal dan Bot Easy dapat menyelesaikan pertandingan.
- Kontrol tembakan, fisika dasar, aturan inti, timer, pause/resume berjalan sesuai keputusan.
- Hasil, riwayat, dan pengaturan lokal dapat disimpan/dibaca.
- Navigasi, Results Screen, Settings, History, dan How to Play berfungsi.
- Tidak ada crash atau bug kritis pada skenario utama.
- Class dan struct sesuai baseline atau perubahan telah disepakati.
- Dokumentasi, laporan, dan demo siap dikumpulkan paling lambat 13 Desember 2026.

## 17. Hal yang belum dikunci

Hal berikut tidak boleh dianggap sudah diputuskan hanya berdasarkan asumsi:
1. Daftar lengkap foul dan seluruh pengecualian aturan 8-Ball/9-Ball.
2. Detail break 8-Ball dan seluruh kondisi khusus bola 8.
3. Detail posisi re-spot bola 9 dan aturan penempatan yang lebih rinci.
4. Parameter fisika: massa efektif, gesekan, restitusi, kecepatan, dan toleransi numerik.
5. Akurasi/algoritma prediksi lintasan dan strategi Bot Easy.
6. Resolusi, ukuran minimum jendela, dan detail teknis resize 16:9.
7. Format final file TXT, validasi, dan perilaku pemulihan jika file rusak.
8. Rincian statistik yang ditampilkan pada Results dan Match History.
9. Detail implementasi teknis yang memang harus dipilih berdasarkan hasil uji.

Keputusan atas hal-hal tersebut perlu dicatat dan diselaraskan pada kode, diagram, README, serta pembagian tugas. Jangan menambahkan fitur di luar scope tanpa persetujuan kelompok.

## 18. Rujukan dan riwayat

### 18.1 Dasar dokumen

README ini merupakan konsolidasi dari:
- `YouKnowBall_Acuan_Proyek_Final_v02.md` — dasar kelengkapan acuan dan skenario.
- `YouKnowBall_Acuan_Proyek_Final_v03.md` — keputusan terbaru produk, kontrak method, arsitektur, dan pembagian kerja.
- `Dasar_Arsitektur_SimulasiBilliard.md` — dasar responsibility, kolaborasi class, struct, dan batas arsitektur.

Jika terdapat perbedaan, keputusan proyek terbaru yang sudah disepakati dan ditegaskan dalam README ini menjadi acuan. Bagian yang belum dipastikan tetap dicatat pada Bagian 17.

### 18.2 Riwayat perubahan

| Versi | Keterangan |
|---|---|
| 05 | Pemadatan dan konsolidasi seluruh bagian agar mudah dibaca tanpa menghilangkan keputusan inti, kontrak arsitektur, jadwal, dan TBD. |
| 04 | Konsolidasi struktur lengkap README dan keputusan proyek. |
| 03 | Pembaruan keputusan produk, kontrak method, arsitektur, dan pembagian kerja. |
| 02 | Acuan proyek dan spesifikasi awal yang diperluas. |
| 01 | Rancangan awal proyek. |

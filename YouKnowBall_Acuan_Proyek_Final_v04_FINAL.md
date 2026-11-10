# YouKnowBall --- Dokumen Acuan Proyek Final v04

> **Dokumen utama kelompok untuk menyelesaikan proyek YouKnowBall.**\
> Menggabungkan kelengkapan MD v02 dengan keputusan terbaru dan
> penyelarasan MD v03.

  Metadata                    Keterangan
  --------------------------- --------------------------------------------------
  Produk                      YouKnowBall
  Mata kuliah                 Desain dan Pemrograman Berorientasi Objek (DPBO)
  Teknologi                   C++ dan SFML
  Kelompok                    Kelompok 9
  Versi                       v04
  Tanggal finalisasi          10 November 2026
  Batas penyelesaian proyek   13 Desember 2026
  Status                      Acuan kerja kelompok

## Cara Menggunakan Dokumen Ini

MD v02 dipertahankan sebagai kerangka kelengkapan dan kedalaman
pembahasan. MD v03 menjadi lapisan keputusan terbaru untuk memperbarui
atau menyelaraskan ketentuan yang berubah.

**Urutan prioritas jika terdapat perbedaan:** 1. Keputusan eksplisit
terbaru pada Bagian B (MD v03). 2. Ketentuan rinci Bagian A (MD v02)
yang tidak diubah oleh MD v03. 3. Dokumen turunan seperti diagram,
laporan, dan kode harus mengikuti v04.

Penggabungan atau perubahan judul tidak boleh menghilangkan substansi,
ketentuan, atau detail implementasi. Perubahan baru harus disepakati dan
dicatat.

## Daftar Isi

-   [Bagian A --- Acuan Lengkap Proyek (MD
    v02)](#bagian-a--acuan-lengkap-proyek-md-v02)
-   [Bagian B --- Penyelarasan Keputusan Terbaru (MD
    v03)](#bagian-b--penyelarasan-keputusan-terbaru-md-v03)
-   [Bagian C --- Aturan Pemeliharaan
    Dokumen](#bagian-c--aturan-pemeliharaan-dokumen)

------------------------------------------------------------------------

# Bagian A --- Acuan Lengkap Proyek (MD v02)

Seluruh 24 bagian MD v02 dipertahankan di bagian ini sebagai fondasi
kelengkapan proyek.

## 1. Identitas dan Gambaran Proyek

YouKnowBall merupakan game simulasi biliar 2D dengan sudut pandang
top-down yang dikembangkan menggunakan C++ dan SFML. Permainan
menyediakan mode 8-Ball dan 9-Ball. Pemain dapat bertanding melawan
pemain lokal lain pada satu perangkat atau melawan Bot Easy.

Proyek ini dikerjakan oleh Kelompok 9 untuk memenuhi tugas mata kuliah
DPBO. Rancangan menekankan penerapan Object-Oriented Programming (OOP)
melalui pembagian tanggung jawab class, kolaborasi objek, enkapsulasi,
dan polimorfisme.

### 1.1 Identitas kelompok

  Informasi            Keterangan
  -------------------- ----------------------
  Kelompok             9
  Anggota 1            Rapid Akbar Sinatria
  Anggota 2            Muhammad Argo Iman
  Anggota 3            Satya Firma Ashari
  Nama produk          YouKnowBall
  Bahasa pemrograman   C++
  Library              SFML
  Platform             PC/Desktop
  Bentuk permainan     Biliar 2D top-down

### 1.2 Tujuan dokumen

Dokumen ini digunakan sebagai sumber acuan untuk: - Menjaga agar scope
produk tidak berubah tanpa keputusan kelompok. - Menjadi dasar
penyusunan DOCX rencana proyek dan PPT. - Menjadi dasar CRC card,
spesifikasi class, Class Diagram, Sequence Diagram, dan State Diagram. -
Menjaga konsistensi tanggung jawab antarkelas selama implementasi. -
Menjadi rujukan pembagian kerja, WBS, dan pengujian.

------------------------------------------------------------------------

## 2. Tujuan dan Prinsip Rancangan

Rancangan menggunakan pendekatan **Responsibility-Driven Design (RDD)**.
Setiap class memiliki tanggung jawab yang jelas, mengetahui informasi
yang menjadi bagiannya (*Knowing Responsibility*), melakukan tindakan
yang menjadi kewenangannya (*Doing Responsibility*), dan berkolaborasi
dengan class lain bila proses membutuhkan tanggung jawab tersebut.

Prinsip desain yang dipertahankan:

1.  Arsitektur baseline terdiri dari **14 class utama dan 8 struct
    pendukung**.
2.  Class tidak dibuat hanya untuk mewakili setiap halaman, tombol, atau
    elemen visual.
3.  Fungsi yang sejenis digabung apabila masih berada dalam satu
    tanggung jawab yang utuh.
4.  `PhysicsEngine` mencatat fakta fisik, sedangkan `GameRules` menilai
    fakta tersebut berdasarkan aturan permainan.
5.  `Player` menyimpan identitas dan statistik; controller menentukan
    tindakan pemain.
6.  Pemain manusia dan Bot menggunakan jalur eksekusi pukulan yang sama.
7.  Use case scenario menjelaskan interaksi aktor dengan sistem, bukan
    komunikasi internal class.
8.  Detail teknis yang belum diputuskan harus ditandai sebagai usulan
    atau hal yang perlu dikonfirmasi, bukan diperlakukan sebagai
    ketentuan final.

### 2.1 Prinsip Knowing dan Doing

-   **Knowing Responsibility** menjelaskan data atau informasi yang
    diketahui dan dikelola oleh suatu class.
-   **Doing Responsibility** menjelaskan tindakan atau proses yang
    menjadi tanggung jawab class.
-   **Collaborator** adalah class lain yang diajak bekerja sama untuk
    menyelesaikan tanggung jawab tertentu.

Untuk kebutuhan PPT, responsibility setiap class dapat diringkas menjadi
satu kalimat. CRC lengkap tetap memuat Knowing, Doing, atribut, method,
dan collaborator sebagaimana dijelaskan pada Bagian 13.

------------------------------------------------------------------------

## 3. Ruang Lingkup Produk

### 3.1 Fitur yang termasuk

-   Mode permainan **8-Ball** dan **9-Ball**.
-   Mode lawan **Pemain Lokal** (dua pemain pada satu perangkat) dan
    **Bot Easy**.
-   Bot Easy tersedia untuk kedua mode permainan.
-   Pengaturan nama pemain sebelum pertandingan.
-   Pilihan waktu per giliran: **tanpa batas, 15 detik, 30 detik, atau
    60 detik**.
-   Kontrol arah dan kekuatan pukulan yang terpisah.
-   Meja biliar, cue ball, object ball, cue stick, dan enam pocket.
-   Fisika dasar: pergerakan bola, gesekan/perlambatan, tumbukan antarb
    bola, pantulan bantalan, dan deteksi pocket.
-   Aturan permainan, target legal, pergantian/kelanjutan giliran, foul,
    scratch, ball-in-hand, dan kondisi menang.
-   Prediksi lintasan sederhana.
-   Pause, resume, restart, rematch, dan kembali ke menu.
-   Halaman menu, pengaturan pertandingan, permainan, pause, hasil,
    riwayat, pengaturan aplikasi, cara bermain, dan konfirmasi keluar.
-   Riwayat pertandingan dan pengaturan aplikasi disimpan secara lokal
    menggunakan file TXT.
-   Evaluasi hasil pertandingan dan statistik dasar.

### 3.2 Fitur yang tidak termasuk

-   Multiplayer online atau LAN.
-   Login, akun pengguna, server, atau database eksternal.
-   Bot Normal dan Bot Hard.
-   Pocket Challenge.
-   Spin shot dan jump shot.
-   Replay pertandingan.
-   Turnamen atau matchmaking online.
-   Pengaturan display/resolusi/fullscreen pada scope pengaturan
    aplikasi saat ini.

### 3.3 Batasan interpretasi

Daftar fitur pada Bagian 3.1 merupakan ruang lingkup produk. Rincian
seperti rumus fisika, strategi internal Bot Easy, format penyimpanan
TXT, dan beberapa kasus batas aturan masih dapat ditentukan pada tahap
implementasi tanpa otomatis dianggap sebagai penambahan fitur.

------------------------------------------------------------------------

## 4. Halaman, Navigasi, dan Informasi Antarmuka

### 4.1 Halaman aplikasi

1.  **Main Menu** --- pintu masuk ke Mulai Pertandingan, Riwayat
    Pertandingan, Pengaturan Aplikasi, Cara Bermain, dan Keluar.
2.  **Match Setup** --- memilih 8-Ball/9-Ball, mode lawan, nama pemain,
    dan batas waktu, kemudian memulai pertandingan.
3.  **Game** --- menampilkan meja, bola, cue, indikator arah, indikator
    power, pemain aktif, informasi target, dan timer jika digunakan.
4.  **Pause** --- menyediakan Lanjutkan, Pengaturan Aplikasi, Mulai
    Ulang, dan Menu Utama. Aksi yang mengakhiri pertandingan aktif
    memerlukan konfirmasi.
5.  **Result** --- menampilkan pemenang dan ringkasan pertandingan.
6.  **History** --- menampilkan daftar pertandingan selesai dan detail
    setiap catatan.
7.  **Settings** --- mengatur volume musik, volume efek suara (SFX), dan
    sensitivitas mouse.
8.  **How to Play** --- menjelaskan kontrol, aturan dasar 8-Ball/9-Ball,
    foul, scratch, dan ball-in-hand.
9.  **Exit Confirmation** --- meminta konfirmasi sebelum aplikasi
    ditutup.

Tidak dibuat class terpisah untuk setiap halaman pada baseline.
Pengelolaan halaman dilakukan melalui `ScreenManager`.

### 4.2 Navigasi dan perilaku kembali

-   Pengaturan aplikasi dapat dibuka dari Main Menu maupun Pause.
-   Pengaturan yang dibuka dari Pause harus kembali ke Pause setelah
    pengguna selesai mengubah pengaturan.
-   Pengaturan yang dibuka dari Main Menu kembali ke Main Menu.
-   Kembali ke Menu Utama ketika pertandingan masih aktif memerlukan
    konfirmasi.
-   Pertandingan yang dibatalkan sebelum selesai tidak disimpan sebagai
    hasil pertandingan.
-   Rematch membuat pertandingan baru dengan konfigurasi yang sama
    seperti pertandingan sebelumnya.

### 4.3 Informasi minimum pada halaman permainan

-   Meja dan seluruh bola yang masih aktif.
-   Cue stick dan indikator arah bidikan.
-   Indikator power yang terpisah dari kontrol arah.
-   Pemain yang sedang mendapat giliran.
-   Informasi target: kelompok bola pada 8-Ball atau bola bernomor
    terendah pada 9-Ball.
-   Timer jika batas waktu diaktifkan.
-   Akses Pause melalui tombol **Esc**.
-   Informasi ball-in-hand atau instruksi penempatan cue ball ketika
    kondisi tersebut aktif.

------------------------------------------------------------------------

## 5. Konfigurasi Pertandingan

  Pengaturan                         Pilihan
  ---------------------------------- ----------------------------------
  Jenis permainan                    8-Ball / 9-Ball
  Mode lawan                         Pemain Lokal / Bot Easy
  Nama pemain 1                      Diisi pengguna
  Nama pemain 2                      Diisi pengguna pada mode lokal
  Identitas pemain 2 pada mode Bot   Bot
  Batas waktu per giliran            Tanpa batas / 15 / 30 / 60 detik
  Aksi                               Mulai Pertandingan

Pada mode Pemain Lokal, dua pemain menggunakan perangkat yang sama
secara bergantian. Pada mode Bot Easy, pemain manusia bertanding melawan
Bot yang dikendalikan sistem.

------------------------------------------------------------------------

## 6. Kontrol Permainan

Kontrol arah dan power **dipisahkan**. Satu tindakan tidak boleh
mengubah arah dan kekuatan sekaligus.

### 6.1 Mengatur arah

Pemain menggerakkan mouse/cue pada area meja untuk menentukan arah
pukulan. Arah bidikan ditetapkan terlebih dahulu.

### 6.2 Mengatur kekuatan

Setelah arah ditetapkan, pemain menggunakan indikator berbentuk cue
stick yang terpisah dari area kontrol arah untuk mengatur power.
Indikator tersebut hanya mengatur kekuatan pukulan, bukan arah.

### 6.3 Penguncian dan pembatalan

-   Ketika pemain sedang mengatur power, arah bidikan dikunci.
-   Jika pemain menekan **Space sebelum mouse dilepas**, pengaturan
    power dibatalkan dan pemain dapat kembali mengatur arah.
-   Jika mouse dilepas tanpa pembatalan, pukulan langsung dijalankan
    menggunakan arah dan power yang sudah ditentukan.
-   Tampilan persentase power tidak diwajibkan. Power dapat
    direpresentasikan melalui posisi atau jarak indikator.
-   Pause membatalkan tindakan tarik yang belum menjadi pukulan agar
    tidak terjadi tembakan tidak sengaja ketika permainan dilanjutkan.

### 6.4 Timeout ketika power sedang diatur

Jika waktu habis ketika pemain sedang menarik indikator power, sistem
langsung mengeksekusi pukulan menggunakan power yang telah tercapai pada
saat waktu habis. Pemain tidak memperoleh tambahan waktu untuk
menyelesaikan tarikan.

------------------------------------------------------------------------

## 7. Timer dan Siklus Giliran

-   Pilihan timer adalah tanpa batas, 15 detik, 30 detik, atau 60 detik
    per giliran.
-   Timer berjalan ketika pemain sedang mengatur bidikan atau power.
-   Timer berhenti ketika bola sedang bergerak dalam simulasi.
-   Timer berhenti ketika permainan di-pause.
-   Resume melanjutkan timer dari sisa waktu sebelumnya.
-   Setelah seluruh bola berhenti, hasil pukulan dievaluasi sebelum
    giliran berikutnya dimulai.
-   Timeout **bukan jenis foul** dalam keputusan proyek saat ini.
-   Jika timeout terjadi ketika power sedang ditarik, sistem
    mengeksekusi pukulan dengan power yang sudah tercapai.

**Belum dikunci:** perilaku timeout ketika pemain tidak sedang menarik
power. Jangan menganggap timeout otomatis menjadi foul. Tindakan yang
akan digunakan (misalnya mengakhiri kesempatan dan mengalihkan giliran)
harus ditetapkan secara konsisten sebelum implementasi.

------------------------------------------------------------------------

## 8. Aturan Permainan

Aturan proyek mengacu pada dokumen WPA Rules yang diberikan sebagai
rujukan, tetapi implementasi YouKnowBall merupakan **adaptasi untuk
kebutuhan proyek**, bukan penerapan penuh seluruh peraturan turnamen
WPA. Ketentuan yang belum dikunci tidak boleh ditulis seolah telah
menjadi keputusan final.

### 8.1 Aturan umum yang telah ditetapkan

-   Permainan menggunakan cue ball untuk memukul object ball.
-   Pemain menunggu sampai seluruh bola berhenti sebelum melakukan
    pukulan berikutnya.
-   Foul menyebabkan giliran berpindah kepada lawan dan lawan memperoleh
    **ball-in-hand**.
-   Scratch (cue ball masuk pocket) termasuk foul.
-   Ball-in-hand memungkinkan pemain menempatkan cue ball pada posisi
    yang valid di area permainan.
-   Posisi cue ball tidak boleh berada di luar area permainan, bertumpuk
    dengan bola aktif, atau berada di dalam pocket.
-   `PhysicsEngine` mencatat kejadian fisik; `GameRules` menentukan
    konsekuensi aturan.

### 8.2 Aturan 8-Ball

-   Kelompok bola terdiri dari **Solid (1--7)** dan **Stripe (9--15)**.
    Bola 8 merupakan bola penentu.
-   Kelompok pemain ditetapkan setelah bola dari salah satu kelompok
    masuk secara sah.
-   Pemain yang secara sah memasukkan bola dari kelompoknya sendiri
    mempertahankan giliran.
-   Seluruh bola dari kelompok pemain harus diselesaikan sebelum bola 8
    dapat dimasukkan untuk menang.
-   Memasukkan bola 8 sebelum seluruh kelompok sendiri habis menyebabkan
    kekalahan.
-   Memasukkan bola 8 secara sah setelah kelompok sendiri habis
    menyebabkan kemenangan.
-   Jika bola 8 masuk bersamaan dengan scratch/foul pada pukulan normal,
    pemain yang melakukan pukulan kalah.
-   Jika bola 8 masuk saat break, rack diulang sesuai keputusan proyek.

**Belum dikunci:** penentuan kelompok ketika dua kelompok masuk dalam
satu pukulan, termasuk apakah pemain memilih kelompok. Jangan menetapkan
perilaku tersebut tanpa konfirmasi kelompok.

### 8.3 Aturan 9-Ball

-   Bola bernomor terendah yang masih aktif harus menjadi bola pertama
    yang terkena cue ball.
-   Bola lain boleh masuk selama kontak pertama dan ketentuan pukulan
    sah terpenuhi.
-   Memasukkan bola 9 secara sah menyebabkan kemenangan.
-   Jika bola 9 masuk dalam pukulan yang mengandung foul, kemenangan
    tidak diberikan.
-   Jika bola 9 masuk saat break, bola 9 di-respot dan permainan
    dilanjutkan.

### 8.4 Break

Keputusan khusus yang telah ditetapkan: - **8-Ball:** jika bola 8 masuk
saat break, rack diulang. - **9-Ball:** jika bola 9 masuk saat break,
bola 9 di-respot dan permainan dilanjutkan.

Ketentuan break lain, seperti jumlah bola yang harus menyentuh bantalan,
cue ball scratch saat break, dan konsekuensi break tidak sah, belum
dikunci dalam baseline terbaru.

### 8.5 Foul dan scratch

Ketentuan yang telah ditetapkan: - Foul mengalihkan giliran kepada
lawan. - Lawan memperoleh ball-in-hand. - Scratch diperlakukan sebagai
foul. - Timeout bukan foul.

Daftar lengkap kondisi foul selain scratch belum dikunci. Contoh seperti
salah kontak pertama, tidak mengenai bola, atau tidak ada bola menyentuh
bantalan setelah kontak tidak boleh dianggap sebagai keputusan final
sebelum disepakati untuk implementasi.

### 8.6 Ball-in-hand

Ketika memperoleh ball-in-hand, pemain dapat menempatkan cue ball pada
posisi yang memenuhi seluruh ketentuan berikut: 1. Berada di dalam area
bermain yang diizinkan. 2. Tidak overlap dengan object ball yang masih
aktif. 3. Tidak berada di area pocket. 4. Divalidasi sebelum pemain
kembali ke tahap membidik.

Secara desain, `Table` dapat memeriksa batas dan geometri posisi,
sedangkan `GameRules` menentukan apakah penempatan tersebut diizinkan
oleh keadaan pertandingan.

------------------------------------------------------------------------

## 9. Prediksi Lintasan

Prediksi lintasan merupakan fitur dalam ruang lingkup dengan bentuk
sederhana:

1.  Garis prediksi cue ball sampai titik tumbukan pertama.
2.  Prediksi arah object ball setelah tumbukan pertama.

Prediksi tersebut merupakan bantuan visual, bukan jaminan lintasan akhir
seluruh bola. Tumbukan lanjutan, pantulan, gesekan, dan interaksi bola
lain tetap dihitung oleh `PhysicsEngine`.

------------------------------------------------------------------------

## 10. Bot Easy

-   Bot Easy tersedia untuk mode 8-Ball dan 9-Ball.
-   Bot memilih target legal dengan mengacu pada aturan permainan.
-   Bot menentukan target, pilihan pocket, arah, dan kekuatan pukulan
    menggunakan heuristik sederhana.
-   Bot tidak memiliki mesin fisika sendiri.
-   Bot menghasilkan `ShotCommand` melalui jalur yang sama dengan pemain
    manusia.
-   Pukulan Bot disimulasikan oleh `PhysicsEngine` dan dievaluasi oleh
    `GameRules`.
-   Bot Normal dan Bot Hard tidak termasuk scope.
-   Strategi fallback dapat digunakan apabila Bot tidak menemukan pot
    langsung yang layak. Detail algoritma dan fallback merupakan
    keputusan implementasi, bukan aturan permainan.

------------------------------------------------------------------------

## 11. Hasil, Riwayat, dan Pengaturan Aplikasi

### 11.1 Informasi hasil pertandingan

Halaman Result menampilkan sekurang-kurangnya: - Nama kedua pemain. -
Nama pemenang. - Jenis permainan (8-Ball/9-Ball). - Jumlah bola masuk
sesuai pencatatan statistik proyek. - Jumlah foul setiap pemain. -
Durasi pertandingan.

### 11.2 Penyimpanan riwayat

-   Pertandingan yang telah selesai disimpan otomatis ke riwayat.
-   Penyimpanan dilakukan secara lokal menggunakan file TXT.
-   Daftar riwayat menampilkan tanggal/waktu, jenis permainan, pemain,
    dan pemenang.
-   Detail riwayat menampilkan ringkasan hasil, jumlah bola masuk, foul,
    dan durasi.
-   Pertandingan yang di-restart sebelum selesai atau ditinggalkan
    sebelum selesai tidak disimpan sebagai hasil pertandingan.
-   Rematch menggunakan kembali konfigurasi pertandingan sebelumnya.
-   Satu hasil pertandingan tidak boleh tersimpan lebih dari satu kali.

### 11.3 Data catatan pertandingan

Rancangan `MatchRecord` mencakup identitas catatan, tanggal/waktu, jenis
permainan, mode lawan, nama pemain, pemenang, alasan hasil, statistik
bola masuk, statistik foul, statistik pukulan, durasi aktif, dan batas
waktu yang digunakan.

Nama dan tipe atribut merupakan rancangan data. Format serialisasi TXT,
delimiter, dan kebijakan pengelolaan jumlah riwayat belum dikunci.

### 11.4 Pengaturan aplikasi

Pengaturan yang termasuk scope: - Volume musik. - Volume efek suara
(SFX). - Sensitivitas kontrol mouse.

Pengaturan disimpan secara lokal menggunakan file TXT dan dimuat kembali
ketika aplikasi dibuka. Pengaturan display, resolusi, dan fullscreen
tidak termasuk scope saat ini.

------------------------------------------------------------------------

## 12. Arsitektur dan Keputusan Penggabungan Class

### 12.1 Baseline arsitektur

Arsitektur YouKnowBall mempertahankan **14 class utama dan 8 struct
pendukung**. Angka ini merupakan baseline desain kelompok, bukan target
untuk memperbanyak class. Penambahan atau pemisahan class hanya
dilakukan jika ditemukan kebutuhan desain yang kuat dan disepakati
kelompok.

### 12.2 Daftar 14 class utama

  ----------------------------------------------------------------------------
                    No. Kelompok         Class                Responsibility
                                                              singkat
  --------------------- ---------------- -------------------- ----------------
                      1 Pengelolaan      `GameApp`            Mengelola
                        aplikasi                              inisialisasi,
                                                              siklus utama,
                                                              dan jalannya
                                                              aplikasi.

                      2 Pengelolaan      `ScreenManager`      Mengelola
                        aplikasi                              tampilan layar,
                                                              navigasi, dan
                                                              interaksi
                                                              antarmuka.

                      3 Pertandingan     `MatchSession`       Mengelola
                                                              konfigurasi,
                                                              alur, giliran,
                                                              timer, dan
                                                              status
                                                              pertandingan.

                      4 Pemain           `Player`             Menyimpan
                                                              identitas,
                                                              kelompok bola,
                                                              dan statistik
                                                              pemain.

                      5 Pengendali       `PlayerController`   Menyediakan
                        pemain                                kontrak dasar
                                                              bagi pengendali
                                                              tindakan pemain.

                      6 Pengendali       `HumanController`    Mengolah input
                        pemain                                pemain manusia
                                                              menjadi perintah
                                                              pukulan.

                      7 Pengendali       `BotController`      Menentukan
                        pemain                                strategi dan
                                                              perintah pukulan
                                                              untuk Bot Easy.

                      8 Objek permainan  `Table`              Mengelola area
                                                              permainan, bola,
                                                              pocket, dan
                                                              validasi posisi.

                      9 Objek permainan  `Ball`               Menyimpan dan
                                                              mengelola
                                                              kondisi fisik
                                                              setiap bola.

                     10 Objek permainan  `Cue`                Mengelola arah,
                                                              kekuatan, impuls
                                                              pukulan, dan
                                                              prediksi
                                                              lintasan.

                     11 Simulasi         `PhysicsEngine`      Menangani
                                                              pergerakan bola,
                                                              tumbukan,
                                                              pantulan, dan
                                                              deteksi pocket.

                     12 Aturan           `GameRules`          Mengevaluasi
                                                              hasil pukulan
                                                              berdasarkan
                                                              aturan 8-Ball
                                                              dan 9-Ball.

                     13 Penyimpanan      `StorageManager`     Mengelola
                                                              penyimpanan
                                                              pengaturan dan
                                                              riwayat
                                                              pertandingan
                                                              lokal.

                     14 Audio            `AudioManager`       Mengelola
                                                              pemutaran musik
                                                              dan efek suara.
  ----------------------------------------------------------------------------

### 12.3 Keputusan penggabungan class

  -----------------------------------------------------------------------
  Rancangan awal/alternatif           Keputusan akhir
  ----------------------------------- -----------------------------------
  `Game`                              Tanggung jawab aplikasi dan
                                      pertandingan dipisah menjadi
                                      `GameApp` dan `MatchSession`.

  `UIManager`                         Menggunakan `ScreenManager`.

  `GameTable`                         Menggunakan nama `Table`.

  `Pocket` sebagai class              Tidak dibuat sebagai class utama;
                                      data pocket menggunakan
                                      `PocketData` di dalam `Table`.

  `PhysicsSystem` dan                 Digabung menjadi `PhysicsEngine`.
  `CollisionSystem`                   

  `TurnManager` dan `GameTimer`       Dikelola oleh `MatchSession`.

  `GameRules`, `EightBallRules`, dan  Digabung dalam `GameRules`,
  `NineBallRules`                     dibedakan berdasarkan `GameType`.

  `Player` dan `AIPlayer`             `Player` menyimpan data pemain;
                                      `HumanController` dan
                                      `BotController` menjadi sumber
                                      keputusan.

  `MatchHistory`, `SettingsManager`,  Operasi penyimpanan digabung dalam
  dan `FileStorage`                   `StorageManager`.

  `GameResult`                        Ringkasan hasil menggunakan struct
                                      `MatchRecord`.
  -----------------------------------------------------------------------

### 12.4 Batas tanggung jawab utama

-   `GameApp` mengelola siklus hidup aplikasi; `MatchSession` mengelola
    satu pertandingan.
-   `ScreenManager` mengelola halaman dan interaksi antarmuka; bukan
    penentu aturan pertandingan.
-   `Player` menyimpan data; controller menentukan tindakan.
-   `PhysicsEngine` melaporkan fakta fisik; `GameRules` menilai
    konsekuensi aturan.
-   `Table` mengelola area permainan, kumpulan bola, dan pocket; `Ball`
    menyimpan keadaan satu bola.
-   `StorageManager` menangani file; `AppSettings` dan `MatchRecord`
    merupakan data yang disimpan.
-   `BotController` tidak membuat jalur simulasi terpisah.

------------------------------------------------------------------------

## 13. CRC dan Spesifikasi 14 Class

Bagian ini merangkum CRC (*Class--Responsibility--Collaborator*)
sekaligus atribut dan method utama. Responsibility ditulis sebagai satu
kalimat inti agar dapat langsung dipindahkan ke PPT. Knowing dan Doing
dijabarkan terpisah untuk dokumen desain.

### 13.1 Notasi spesifikasi

-   `+` = `public`.
-   `-` = `private`.
-   `#` = `protected`.
-   `virtual` dan `= 0` menunjukkan operasi virtual murni pada class
    abstrak.
-   Signature method merupakan rancangan konseptual untuk membantu
    pembagian tanggung jawab; penyesuaian teknis boleh dilakukan selama
    tidak mengubah tanggung jawab dan perilaku yang telah disepakati.
-   Atribut di bawah adalah atribut penting, bukan daftar yang melarang
    penambahan variabel lokal atau detail implementasi.

### 13.2 Kelompok A --- Pengelolaan Aplikasi dan Pertandingan

#### 13.2.1 `GameApp`

**Deskripsi:** Mengelola inisialisasi, jendela aplikasi, game loop, dan
koordinasi layanan tingkat aplikasi.

**Responsibility:** Mengelola inisialisasi, siklus utama, dan jalannya
aplikasi YouKnowBall.

**Knowing** - Status aplikasi berjalan atau berhenti. - Objek jendela
dan waktu antar-frame. - Layanan tingkat aplikasi yang digunakan.

**Doing** - Menginisialisasi window, aset, pengaturan, dan layanan. -
Menjalankan game loop. - Meneruskan event aplikasi. - Memanggil update
dan render. - Menutup aplikasi dan melepaskan sumber daya.

  Atribut penting   Tipe
  ----------------- --------------------
  `window`          `sf::RenderWindow`
  `running`         `bool`
  `frameClock`      `sf::Clock`

  Method utama      Signature konseptual
  ----------------- --------------------------------
  `initialize`      `bool initialize()`
  `run`             `void run()`
  `processEvents`   `void processEvents()`
  `update`          `void update(float deltaTime)`
  `render`          `void render()`
  `shutdown`        `void shutdown()`

**Collaborator:** `ScreenManager`, `StorageManager`, `AudioManager`,
`MatchSession`.

#### 13.2.2 `ScreenManager`

**Deskripsi:** Mengelola layar aktif, perpindahan halaman, penerimaan
event antarmuka, dan tampilan informasi aplikasi.

**Responsibility:** Mengelola tampilan layar, navigasi, dan interaksi
antarmuka aplikasi.

**Knowing** - Jenis layar yang sedang aktif. - Layar sebelumnya untuk
kebutuhan navigasi kembali. - Posisi pointer atau event antarmuka yang
sedang diproses.

**Doing** - Berpindah antarhalaman. - Menangani event UI. - Memperbarui
elemen antarmuka. - Menggambar halaman aktif. - Mengembalikan pengguna
ke halaman asal, termasuk kembali ke Pause apabila Settings dibuka dari
Pause.

  Atribut penting    Tipe
  ------------------ ----------------
  `currentScreen`    `ScreenType`
  `previousScreen`   `ScreenType`
  `mousePosition`    `sf::Vector2i`

  Method utama               Signature konseptual
  -------------------------- --------------------------------------------
  `changeScreen`             `void changeScreen(ScreenType type)`
  `handleEvent`              `void handleEvent(const sf::Event& event)`
  `update`                   `void update(float deltaTime)`
  `render`                   `void render(sf::RenderWindow& window)`
  `returnToPreviousScreen`   `void returnToPreviousScreen()`

**Collaborator:** `GameApp`, `MatchSession`, `StorageManager`,
`AudioManager`.

#### 13.2.3 `MatchSession`

**Deskripsi:** Mengelola satu sesi pertandingan dari inisialisasi rack
sampai pertandingan selesai, termasuk konfigurasi, pemain, controller,
giliran, timer, pause, restart, dan hasil.

**Responsibility:** Mengelola konfigurasi, alur, giliran, timer, dan
status pertandingan.

**Knowing** - Konfigurasi pertandingan. - Data dua pemain dan controller
masing-masing. - Pemain aktif dan status sesi. - Sisa timer dan durasi
aktif pertandingan. - Kondisi sebelum pukulan dan status penyimpanan
hasil.

**Doing** - Memulai pertandingan dan menyiapkan rack. - Memvalidasi
serta menerima perintah pukulan. - Mengelola timer dan pergantian
giliran. - Menjalankan evaluasi setelah simulasi selesai. - Mengelola
ball-in-hand, pause, resume, restart, dan penyelesaian. - Membentuk
catatan hasil dan meminta penyimpanan satu kali.

  Atribut penting        Tipe
  ---------------------- ----------------------------------------------------
  `config`               `MatchConfig`
  `state`                `MatchState`
  `players`              `std::array<Player, 2>`
  `controllers`          `std::array<std::unique_ptr<PlayerController>, 2>`
  `currentPlayerIndex`   `int`
  `remainingShotTime`    `float`
  `activeDuration`       `float`
  `isResultSaved`        `bool`
  `table`                `Table`
  `cue`                  `Cue`
  `physics`              `PhysicsEngine`
  `rules`                `GameRules`
  `shotStartState`       `ShotStartState`

  -------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- -------------------------------------------------------
  `startMatch`                        `void startMatch(const MatchConfig& config)`

  `submitShot`                        `bool submitShot(const ShotCommand& command)`

  `update`                            `void update(float deltaTime)`

  `onSimulationFinished`              `void onSimulationFinished(const ShotResult& result)`

  `placeCueBall`                      `bool placeCueBall(sf::Vector2f position)`

  `switchTurn`                        `void switchTurn()`

  `handleTimeout`                     `void handleTimeout()`

  `pause`                             `void pause()`

  `resume`                            `void resume()`

  `restart`                           `void restart()`

  `finishMatch`                       `MatchRecord finishMatch()`
  -------------------------------------------------------------------------------------------

**Collaborator:** `Player`, `PlayerController`, `Table`, `Cue`,
`PhysicsEngine`, `GameRules`, `StorageManager`.

**Catatan:** `handleTimeout()` adalah titik penanganan teknis. Perilaku
timeout ketika power sedang ditarik sudah ditetapkan; perilaku timeout
di luar kondisi tersebut masih perlu keputusan.

#### 13.2.4 `Player`

**Deskripsi:** Menyimpan identitas, kelompok bola, dan statistik pemain
selama satu pertandingan. `Player` tidak menentukan input atau strategi
pukulan.

**Responsibility:** Menyimpan identitas, kelompok bola, dan statistik
setiap pemain.

**Knowing** - Nama pemain. - Kelompok bola pada 8-Ball. - Jumlah
pukulan, foul, dan bola masuk yang dicatat.

**Doing** - Mengatur nama dan kelompok bola. - Mencatat pukulan, foul,
dan bola masuk. - Mengatur ulang statistik ketika pertandingan baru
dimulai.

  Atribut penting       Tipe
  --------------------- ---------------
  `name`                `std::string`
  `ballGroup`           `BallGroup`
  `shotCount`           `int`
  `foulCount`           `int`
  `pocketedBallCount`   `int`

  Method utama           Signature konseptual
  ---------------------- -----------------------------------------
  `setName`              `void setName(const std::string& name)`
  `setGroup`             `void setGroup(BallGroup group)`
  `recordShot`           `void recordShot()`
  `recordFoul`           `void recordFoul()`
  `recordPocketedBall`   `void recordPocketedBall()`
  `resetStatistics`      `void resetStatistics()`

**Collaborator:** `MatchSession`, `GameRules`.

### 13.3 Kelompok B --- Pengendali Pemain dan Aturan

#### 13.3.1 `PlayerController` (abstract)

**Deskripsi:** Menetapkan kontrak umum bagi sumber keputusan pemain agar
sistem pertandingan menggunakan jalur penerimaan pukulan yang sama untuk
manusia dan Bot.

**Responsibility:** Menyediakan kontrak dasar bagi pengendali tindakan
pemain.

**Knowing** - Kontrak operasi yang harus dimiliki setiap controller. -
Status tindakan yang dapat dibatalkan sebelum menjadi pukulan.

**Doing** - Menyediakan operasi abstrak untuk menghasilkan
`ShotCommand`. - Menyediakan operasi pembatalan tindakan. - Memungkinkan
polimorfisme antara `HumanController` dan `BotController`.

  Method utama     Signature konseptual
  ---------------- -------------------------------------------
  `createShot`     `virtual ShotCommand createShot(...) = 0`
  `cancelAction`   `virtual void cancelAction() = 0`
  Destructor       `virtual ~PlayerController()`

**Collaborator:** `HumanController`, `BotController`, `MatchSession`.

#### 13.3.2 `HumanController`

**Deskripsi:** Menerjemahkan input mouse menjadi keputusan arah dan
kekuatan pukulan manusia.

**Responsibility:** Mengolah input pemain manusia menjadi perintah
pukulan.

**Knowing** - Status proses drag. - Posisi awal dan posisi mouse
terkini. - Sensitivitas kontrol. - Arah dan power yang sedang dipilih.

**Doing** - Membaca input mouse. - Mengatur arah bidikan melalui
`Cue`. - Mengatur power melalui indikator terpisah. - Membatalkan
pengaturan power jika Space ditekan sebelum mouse dilepas. -
Menghasilkan `ShotCommand` ketika input dilepas secara sah.

  Atribut penting          Tipe
  ------------------------ ----------------
  `isDragging`             `bool`
  `dragStartPosition`      `sf::Vector2f`
  `currentMousePosition`   `sf::Vector2f`
  `dragSensitivity`        `float`
  `currentDirection`       `sf::Vector2f`
  `currentPower`           `float`

  Method utama     Signature konseptual
  ---------------- ------------------------------------------------
  `handleEvent`    `void handleEvent(const sf::Event& event)`
  `updateAim`      `void updateAim(sf::Vector2f mousePosition)`
  `updatePower`    `void updatePower(sf::Vector2f mousePosition)`
  `cancelAction`   `void cancelAction()`
  `createShot`     `ShotCommand createShot(...)`

**Collaborator:** `PlayerController`, `MatchSession`, `Cue`, `Table`.

#### 13.3.3 `BotController`

**Deskripsi:** Menghasilkan keputusan pukulan Bot Easy menggunakan
heuristik sederhana berdasarkan target sah, posisi bola, pocket, arah,
dan kekuatan.

**Responsibility:** Menentukan strategi dan menghasilkan perintah
pukulan untuk Bot Easy.

**Knowing** - Target bola legal. - Pilihan pocket. - Kandidat arah dan
power. - Kondisi meja dan informasi aturan yang relevan. - Status proses
pengambilan keputusan.

**Doing** - Memilih target legal. - Memilih pocket tujuan. - Menghitung
arah dan kekuatan pukulan. - Menghasilkan `ShotCommand`. - Memilih
posisi cue ball yang valid ketika Bot memperoleh ball-in-hand, sesuai
kebutuhan implementasi.

  Atribut penting        Tipe
  ---------------------- ----------------
  `targetBallNumber`     `int`
  `targetPocketId`       `int`
  `candidateDirection`   `sf::Vector2f`
  `candidatePower`       `float`
  `isThinking`           `bool`

  Method utama      Signature konseptual
  ----------------- ----------------------------------
  `chooseTarget`    `int chooseTarget(...)`
  `choosePocket`    `int choosePocket(...)`
  `calculateShot`   `ShotCommand calculateShot(...)`
  `createShot`      `ShotCommand createShot(...)`
  `cancelAction`    `void cancelAction()`

**Collaborator:** `PlayerController`, `MatchSession`, `Table`,
`GameRules`, `Cue`.

**Batas AI:** Bot Easy menggunakan heuristik sederhana. Bot tidak
mempunyai simulasi fisika terpisah dan tidak dijamin selalu menghasilkan
pot yang berhasil. Setiap pukulannya tetap melewati `PhysicsEngine` dan
`GameRules`.

#### 13.3.4 `GameRules`

**Deskripsi:** Mengelola aturan kedua jenis permainan berdasarkan
`GameType`, termasuk target legal, kelompok bola, foul, scratch,
ball-in-hand, dan kondisi kemenangan.

**Responsibility:** Mengevaluasi hasil pukulan berdasarkan aturan 8-Ball
dan 9-Ball.

**Knowing** - Jenis permainan aktif. - Status open table pada 8-Ball. -
Kelompok bola setiap pemain. - Target legal. - Informasi sebelum pukulan
dan fakta hasil simulasi. - Informasi pocket pilihan jika mekanisme
tersebut digunakan dalam implementasi.

**Doing** - Menentukan target legal. - Mengevaluasi `ShotStartState` dan
`ShotResult`. - Menetapkan kelompok bola sesuai keputusan aturan yang
berlaku. - Menentukan foul, scratch, kelanjutan giliran, ball-in-hand,
respot, dan kemenangan. - Memeriksa validitas posisi cue ball
berdasarkan keadaan permainan.

  Atribut penting    Tipe
  ------------------ ------------
  `gameType`         `GameType`
  `tableOpen`        `bool`
  `chosenPocketId`   `int`

  ---------------------------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- ---------------------------------------------------------------------------
  `getLegalTargets`                   `std::vector<int> getLegalTargets(...)`

  `evaluateShot`                      `RuleOutcome evaluateShot(const ShotStartState&, const ShotResult&, ...)`

  `assignBallGroup`                   `void assignBallGroup(...)`

  `checkWinCondition`                 `bool checkWinCondition(...)`

  `validateBallInHandPosition`        `bool validateBallInHandPosition(...)`

  `evaluateBreak`                     `RuleOutcome evaluateBreak(...)`
  ---------------------------------------------------------------------------------------------------------------

**Collaborator:** `MatchSession`, `Player`, `Table`, `ShotStartState`,
`ShotResult`, `RuleOutcome`.

**Batas tanggung jawab:** `GameRules` tidak menghitung gerak, tumbukan,
atau pantulan. Class ini menafsirkan fakta yang telah dicatat oleh
`PhysicsEngine`.

### 13.4 Kelompok C --- Objek Permainan dan Simulasi Fisika

#### 13.4.1 `Table`

**Deskripsi:** Menyimpan area bermain, kumpulan bola, dan enam data
pocket serta memvalidasi posisi bola.

**Responsibility:** Mengelola area permainan, bola, pocket, dan validasi
posisi bola.

**Knowing** - Batas area bermain. - Kumpulan bola yang berada di meja. -
Enam data pocket. - Posisi dan status cue ball serta object ball.

**Doing** - Menyiapkan susunan bola sesuai jenis permainan. -
Menyediakan akses ke kumpulan bola, cue ball, dan pocket. - Memeriksa
validitas posisi cue ball. - Mencari bola bernomor terendah yang masih
aktif untuk 9-Ball. - Mengatur ulang susunan meja ketika pertandingan
baru atau rack ulang dimulai.

  Atribut penting   Tipe
  ----------------- -----------------------------
  `playingArea`     `sf::FloatRect`
  `balls`           `std::vector<Ball>`
  `pockets`         `std::array<PocketData, 6>`

  -------------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- -------------------------------------------------------------
  `setupRack`                         `void setupRack(GameType gameType)`

  `getBalls`                          `std::vector<Ball>& getBalls()`

  `getCueBall`                        `Ball& getCueBall()`

  `getPockets`                        `const std::array<PocketData, 6>& getPockets()`

  `isPositionValid`                   `bool isPositionValid(sf::Vector2f position, float radius)`

  `findLowestBallNumber`              `int findLowestBallNumber()`

  `reset`                             `void reset(GameType gameType)`
  -------------------------------------------------------------------------------------------------

**Collaborator:** `Ball`, `PhysicsEngine`, `GameRules`, `BotController`,
`PocketData`.

#### 13.4.2 `Ball`

**Deskripsi:** Menyimpan keadaan fisik setiap bola dan menyediakan
operasi untuk mengubah posisi, kecepatan, serta statusnya.

**Responsibility:** Menyimpan dan mengelola kondisi fisik setiap bola
selama permainan.

**Knowing** - Nomor bola. - Posisi dan kecepatan. - Radius dan massa
jika diperlukan dalam perhitungan. - Status bola masih aktif atau sudah
masuk pocket.

**Doing** - Menerima impuls awal pukulan. - Memperbarui atau menyediakan
perubahan posisi dan kecepatan. - Menandai bola yang telah masuk
pocket. - Menyediakan informasi apakah bola dianggap diam.

  Atribut penting   Tipe
  ----------------- ----------------
  `number`          `int`
  `position`        `sf::Vector2f`
  `velocity`        `sf::Vector2f`
  `radius`          `float`
  `mass`            `float`
  `isPocketed`      `bool`

  Method utama     Signature konseptual
  ---------------- -------------------------------------------
  `applyImpulse`   `void applyImpulse(sf::Vector2f impulse)`
  `setPosition`    `void setPosition(sf::Vector2f position)`
  `setVelocity`    `void setVelocity(sf::Vector2f velocity)`
  `markPocketed`   `void markPocketed()`
  `isMoving`       `bool isMoving()`

**Collaborator:** `Table`, `PhysicsEngine`, `Cue`.

#### 13.4.3 `Cue`

**Deskripsi:** Mengelola informasi bidikan dan tampilan stik, serta
menghasilkan impuls dari arah dan power yang dipilih controller. Cue
juga menyediakan bantuan lintasan sederhana.

**Responsibility:** Mengelola arah, kekuatan, impuls pukulan, dan
prediksi lintasan bola.

**Knowing** - Sudut dan arah bidikan. - Jarak tarikan atau nilai
power. - Panjang garis bantu bidikan. - Parameter yang diperlukan untuk
menghasilkan impuls.

**Doing** - Memperbarui arah bidikan. - Menetapkan power. - Mengubah
arah dan power menjadi impuls. - Menghasilkan prediksi garis cue ball
sampai tumbukan pertama dan arah object ball setelah tumbukan. -
Menyediakan representasi visual cue dan indikator bidikan.

  Atribut penting     Tipe
  ------------------- ----------------
  `angleRadians`      `float`
  `pullDistance`      `float`
  `maxPullDistance`   `float`
  `power`             `float`
  `aimDirection`      `sf::Vector2f`
  `aimLineLength`     `float`

  ------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- ------------------------------------------------------
  `setAim`                            `void setAim(sf::Vector2f direction)`

  `updateAim`                         `void updateAim(...)`

  `setPower`                          `void setPower(float power)`

  `calculateImpulse`                  `sf::Vector2f calculateImpulse()`

  `calculateTrajectory`               `std::vector<sf::Vector2f> calculateTrajectory(...)`

  `cancelAim`                         `void cancelAim()`
  ------------------------------------------------------------------------------------------

**Collaborator:** `HumanController`, `BotController`, `Ball`, `Table`,
`PhysicsEngine`.

#### 13.4.4 `PhysicsEngine`

**Deskripsi:** Menghitung perubahan fisik bola dan mencatat fakta
kejadian selama satu pukulan. Class ini tidak menentukan apakah kejadian
merupakan foul atau kemenangan.

**Responsibility:** Menangani simulasi pergerakan bola, tumbukan,
pantulan, dan deteksi pocket.

**Knowing** - Parameter gesekan. - Parameter restitusi/pantulan. -
Ambang kecepatan untuk menentukan bola berhenti. - Interval pembaruan
simulasi. - Keadaan meja dan bola selama simulasi.

**Doing** - Memperbarui pergerakan bola. - Menghitung perlambatan akibat
gesekan. - Menangani tumbukan antarb bola. - Menangani pantulan pada
bantalan meja. - Mendeteksi bola yang masuk pocket. - Mencatat fakta
fisik ke `ShotResult`. - Menentukan apakah seluruh bola telah berhenti.

  Atribut penting         Tipe
  ----------------------- ---------
  `frictionCoefficient`   `float`
  `restitution`           `float`
  `stopThreshold`         `float`
  `substepDuration`       `float`

  ----------------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- ----------------------------------------------------------------
  `step`                              `void step(float deltaTime, Table& table, ShotResult& result)`

  `simulateShot`                      `void simulateShot(...)`

  `resolveBallCollision`              `void resolveBallCollision(Ball& ballA, Ball& ballB)`

  `resolveCushionCollision`           `void resolveCushionCollision(Ball& ball, ...)`

  `detectPocketedBalls`               `void detectPocketedBalls(Table& table, ShotResult& result)`

  `areAllBallsStopped`                `bool areAllBallsStopped(const Table& table)`
  ----------------------------------------------------------------------------------------------------

**Collaborator:** `Table`, `Ball`, `ShotResult`.

**Batas tanggung jawab:** `PhysicsEngine` hanya melaporkan kejadian
fisik. Penentuan foul, pergantian giliran, ball-in-hand, atau kemenangan
tetap berada pada `GameRules` dan `MatchSession`.

### 13.5 Kelompok D --- Penyimpanan dan Audio

#### 13.5.1 `StorageManager`

**Deskripsi:** Menangani pembacaan dan penyimpanan pengaturan aplikasi
serta riwayat pertandingan menggunakan file teks lokal.

**Responsibility:** Mengelola penyimpanan dan pemuatan pengaturan serta
riwayat pertandingan lokal.

**Knowing** - Lokasi file pengaturan. - Lokasi file riwayat. -
Pengaturan yang sedang digunakan. - Kumpulan catatan pertandingan yang
telah dibaca.

**Doing** - Memuat pengaturan ketika aplikasi dimulai. - Menyimpan
perubahan pengaturan. - Memuat riwayat pertandingan. - Menambahkan
catatan pertandingan yang selesai. - Menyediakan data riwayat untuk
ditampilkan. - Mencegah satu hasil pertandingan tersimpan lebih dari
sekali.

  Atribut penting      Tipe
  -------------------- ----------------------------
  `settingsFilePath`   `std::string`
  `historyFilePath`    `std::string`
  `cachedSettings`     `AppSettings`
  `historyRecords`     `std::vector<MatchRecord>`

  -----------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- -----------------------------------------------------
  `loadSettings`                      `AppSettings loadSettings()`

  `saveSettings`                      `bool saveSettings(const AppSettings& settings)`

  `loadHistory`                       `std::vector<MatchRecord> loadHistory()`

  `appendMatchRecord`                 `bool appendMatchRecord(const MatchRecord& record)`

  `getMatchRecords`                   `const std::vector<MatchRecord>& getMatchRecords()`
  -----------------------------------------------------------------------------------------

**Collaborator:** `GameApp`, `ScreenManager`, `MatchSession`,
`AppSettings`, `MatchRecord`.

#### 13.5.2 `AudioManager`

**Deskripsi:** Mengelola musik latar, efek suara, dan volume audio
aplikasi.

**Responsibility:** Mengelola pemutaran musik dan efek suara dalam
aplikasi.

**Knowing** - Sumber musik latar. - Buffer efek suara. - Volume musik
dan volume SFX. - Jenis efek suara yang tersedia.

**Doing** - Memuat musik dan efek suara. - Memutar atau menghentikan
musik. - Memutar efek suara berdasarkan kejadian. - Mengubah volume
musik dan SFX.

  Atribut penting     Tipe
  ------------------- --------------------------------------------------
  `backgroundMusic`   `sf::Music`
  `soundBuffers`      `std::map<SoundType, sf::SoundBuffer>`
  `activeSounds`      `std::vector<sf::Sound>` atau pengelolaan setara
  `musicVolume`       `float`
  `soundVolume`       `float`

  -----------------------------------------------------------------------------------------------
  Method utama                        Signature konseptual
  ----------------------------------- -----------------------------------------------------------
  `loadMusic`                         `bool loadMusic(const std::string& path)`

  `playMusic`                         `void playMusic()`

  `stopMusic`                         `void stopMusic()`

  `loadSound`                         `bool loadSound(SoundType type, const std::string& path)`

  `playSound`                         `void playSound(SoundType type)`

  `setMusicVolume`                    `void setMusicVolume(float volume)`

  `setSoundVolume`                    `void setSoundVolume(float volume)`
  -----------------------------------------------------------------------------------------------

**Collaborator:** `GameApp`, `ScreenManager`, `StorageManager`,
`PhysicsEngine`.

------------------------------------------------------------------------

## 14. Delapan Struct Pendukung

Struct merupakan wadah data dan tidak dihitung sebagai class utama.
Struct di bawah ini tidak diwajibkan memiliki method khusus. Bentuk
atribut dapat disesuaikan ketika implementasi dilakukan, selama peran
datanya tetap konsisten.

### 14.1 `MatchConfig`

Menyimpan konfigurasi pertandingan sebelum sesi dimulai, meliputi jenis
permainan, mode lawan, nama pemain, dan pengaturan waktu per giliran.

Atribut penting: - `gameType` - `opponentType` - `playerNames` -
`timeLimitSeconds` - `unlimitedTime`

### 14.2 `AppSettings`

Menyimpan pengaturan aplikasi yang berlaku lintas sesi, yaitu volume
musik, volume efek suara, dan sensitivitas kontrol mouse.

Atribut penting: - `musicVolume` - `soundVolume` - `mouseSensitivity`

### 14.3 `MatchRecord`

Menyimpan ringkasan satu pertandingan yang telah selesai, sehingga
hasilnya dapat ditampilkan pada halaman Result dan History.

Atribut penting: - `matchId` - `dateTime` - `gameType` -
`opponentType` - `playerNames` - `winnerName` - `winReason` -
`pocketedCounts` - `foulCounts` - `shotCounts` -
`activeDurationSeconds` - `timeLimitSeconds`

### 14.4 `PocketData`

Menyimpan informasi posisi dan area deteksi satu pocket. Enam objek
`PocketData` dimiliki oleh `Table`.

Atribut penting: - `pocketID` - `centerPosition` - `captureRadius`

### 14.5 `ShotCommand`

Mewakili perintah pukulan yang dihasilkan oleh controller manusia atau
Bot. Perintah berisi arah, kekuatan, dan status validasi sebelum
diterima oleh sesi pertandingan.

Atribut penting: - `direction` - `power` - `isValid`

### 14.6 `ShotStartState`

Menyimpan snapshot kondisi penting sebelum impuls pukulan diberikan.
Data ini diperlukan agar aturan dapat dievaluasi berdasarkan keadaan
meja dan pemain sebelum simulasi berlangsung.

Atribut penting: - `legalTargets` - `tableOpen` - `activePlayerIndex` -
`isBreakShot`

### 14.7 `ShotResult`

Menyimpan fakta yang terjadi selama simulasi satu pukulan, seperti
kontak pertama, bola yang masuk pocket, cue ball yang masuk pocket, dan
kontak bantalan yang relevan untuk evaluasi aturan.

Atribut penting: - `firstHitBallNumber` - `pocketedBallNumbers` -
`cueBallPocketed` - `cushionAfterFirstContact` -
`numberedBallsHitCushionOnBreak`

Atribut yang benar-benar diperlukan dapat disesuaikan dengan daftar
aturan dan kejadian fisik yang akhirnya disepakati. Struct ini tidak
memutuskan apakah suatu kejadian merupakan foul.

### 14.8 `RuleOutcome`

Menyimpan hasil evaluasi aturan setelah simulasi selesai, termasuk
status foul, jenis foul, kelanjutan giliran, ball-in-hand, status
pertandingan, pemenang, dan bola yang perlu di-respot.

Atribut penting: - `isFoul` - `foulType` - `retainTurn` - `ballInHand` -
`matchFinished` - `winnerIndex` - `ballsToSpot`

------------------------------------------------------------------------

## 15. Enumerasi Pendukung

Enumerasi digunakan agar status dan pilihan sistem tidak diwakili angka
atau string bebas.

  -----------------------------------------------------------------------
  Enum                    Nilai baseline          Keterangan
  ----------------------- ----------------------- -----------------------
  `GameType`              `EIGHT_BALL`,           Jenis permainan.
                          `NINE_BALL`             

  `OpponentType`          `LOCAL_PLAYER`, `BOT`   Mode lawan.

  `ScreenType`            `MAIN_MENU`,            Layar aktif.
                          `MATCH_SETUP`, `GAME`,  
                          `PAUSE`, `RESULT`,      
                          `HISTORY`, `SETTINGS`,  
                          `HOW_TO_PLAY`,          
                          `EXIT_CONFIRM`          

  `MatchState`            `SETUP`, `WAITING`,     Keadaan sesi
                          `AIMING`,               pertandingan.
                          `POWER_SETTING`,        
                          `BALL_IN_HAND`,         
                          `SIMULATING`, `PAUSED`, 
                          `FINISHED`              

  `BallGroup`             `NONE`, `SOLID`,        Kelompok bola pada
                          `STRIPE`                8-Ball.

  `FoulType`              `NONE`, `SCRATCH`,      Timeout tidak
                          serta jenis foul lain   dimasukkan sebagai
                          jika kelak disepakati   foul.

  `SoundType`             `BALL_COLLISION`,       Kategori efek suara.
                          `CUSHION_HIT`,          
                          `BALL_POCKETED`,        
                          `CUE_HIT`, `UI_CLICK`   
  -----------------------------------------------------------------------

**Catatan:** `TIMEOUT` tidak dimasukkan sebagai nilai `FoulType`, karena
timeout bukan foul menurut keputusan proyek saat ini. Perilaku timeout
di luar kondisi power sedang ditarik masih perlu ditentukan.

------------------------------------------------------------------------

## 16. Hubungan Antarkelas

Hubungan berikut menjelaskan struktur konseptual. Relasi dan
multiplicity pada Class Diagram akhir harus dicocokkan dengan
kepemilikan objek yang benar-benar diterapkan.

  ----------------------------------------------------------------------------------
  Komponen pertama    Jenis hubungan          Komponen kedua       Makna
  ------------------- ----------------------- -------------------- -----------------
  `GameApp`           Composition/ownership   `ScreenManager`      Aplikasi memiliki
                                                                   pengelola layar.

  `GameApp`           Composition/ownership   `StorageManager`     Aplikasi memiliki
                                                                   layanan
                                                                   penyimpanan.

  `GameApp`           Composition/ownership   `AudioManager`       Aplikasi memiliki
                                                                   layanan audio.

  `GameApp`           Association             `MatchSession`       Aplikasi membuat
                                                                   dan mengelola
                                                                   sesi ketika
                                                                   pertandingan
                                                                   dimulai.

  `MatchSession`      Composition/ownership   `Player`             Satu sesi
                                                                   memiliki dua data
                                                                   pemain.

  `MatchSession`      Composition/ownership   `PlayerController`   Sesi mengelola
                                                                   controller untuk
                                                                   kedua pemain.

  `HumanController`   Inheritance             `PlayerController`   Controller
                                                                   manusia memenuhi
                                                                   kontrak dasar.

  `BotController`     Inheritance             `PlayerController`   Controller Bot
                                                                   memenuhi kontrak
                                                                   dasar.

  `MatchSession`      Composition/ownership   `Table`, `Cue`,      Sesi memiliki
                                              `PhysicsEngine`,     atau mengelola
                                              `GameRules`          komponen inti
                                                                   pertandingan.

  `Table`             Composition             `Ball`               Meja memiliki
                                                                   kumpulan bola.

  `Table`             Composition             `PocketData`         Meja menyimpan
                                                                   enam data pocket.

  `PhysicsEngine`     Association             `Table`, `Ball`,     Mesin fisika
                                              `ShotResult`         memperbarui
                                                                   keadaan bola pada
                                                                   meja dan mencatat
                                                                   fakta.

  `GameRules`         Association             `Player`, `Table`,   Aturan membaca
                                              `ShotStartState`,    keadaan
                                              `ShotResult`         pemain/meja dan
                                                                   mengevaluasi
                                                                   hasil pukulan.

  `BotController`     Association             `Table`,             Bot membaca
                                              `GameRules`, `Cue`   kondisi permainan
                                                                   dan menghasilkan
                                                                   keputusan
                                                                   pukulan.

  `StorageManager`    Association             `AppSettings`,       Penyimpanan
                                              `MatchRecord`        membaca dan
                                                                   menulis data
                                                                   pengaturan serta
                                                                   hasil.

  `AudioManager`      Association             `SoundType`          Audio mengelola
                                                                   pemutaran
                                                                   berdasarkan
                                                                   kategori suara.
  ----------------------------------------------------------------------------------

### 16.1 Keputusan pemisahan tanggung jawab

  -----------------------------------------------------------------------
  Pemisahan                           Ketentuan
  ----------------------------------- -----------------------------------
  `Ball` dan `PhysicsEngine`          Ball menyimpan keadaan;
                                      PhysicsEngine menghitung perubahan
                                      keadaan.

  `PhysicsEngine` dan `GameRules`     PhysicsEngine mencatat fakta fisik;
                                      GameRules menilai konsekuensi
                                      aturan.

  `Player` dan controller             Player menyimpan
                                      identitas/statistik; controller
                                      menentukan aksi.

  `HumanController` dan               Sumber keputusan berbeda, tetapi
  `BotController`                     keduanya menghasilkan ShotCommand
                                      melalui kontrak yang sama.

  `GameApp` dan `MatchSession`        GameApp mengelola aplikasi;
                                      MatchSession mengelola satu
                                      pertandingan.

  `ScreenManager` dan logika          ScreenManager mengelola
  pertandingan                        tampilan/navigasi; MatchSession dan
                                      GameRules mengelola alur serta
                                      aturan.

  `StorageManager` dan struct data    StorageManager membaca/menulis;
                                      struct menyimpan data.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 17. Alur Kolaborasi Satu Pukulan

Bagian ini merupakan alur internal sistem sebagai dasar Sequence
Diagram, bukan narasi use case aktor.

1.  `MatchSession` memastikan pemain aktif, state mengizinkan pukulan,
    seluruh bola diam, dan waktu masih tersedia.
2.  Controller aktif menghasilkan `ShotCommand`.
3.  Untuk pemain manusia, `HumanController` membaca input arah dan power
    yang terpisah. Untuk Bot, `BotController` memilih target dan
    menghitung keputusan pukulan.
4.  `MatchSession` memvalidasi perintah. Perintah yang tidak valid
    ditolak tanpa memulai simulasi.
5.  Sebelum impuls diberikan, `MatchSession` menyiapkan
    `ShotStartState`.
6.  `Cue` mengubah arah dan power menjadi impuls.
7.  Cue ball menerima impuls dan `PhysicsEngine` menjalankan simulasi.
8.  Selama simulasi, `PhysicsEngine` memperbarui gerak, gesekan,
    tumbukan, pantulan, dan deteksi pocket sambil mengisi `ShotResult`.
9.  Ketika seluruh bola berhenti, `MatchSession` meminta `GameRules`
    mengevaluasi `ShotStartState` dan `ShotResult`.
10. `GameRules` menghasilkan `RuleOutcome`.
11. `MatchSession` memperbarui statistik, status giliran, timer, dan
    status pertandingan.
12. Jika pertandingan selesai, `MatchSession` membentuk `MatchRecord`
    dan `StorageManager` menyimpannya satu kali.
13. `ScreenManager` menampilkan keadaan permainan berikutnya atau
    halaman Result.

------------------------------------------------------------------------

## 18. Use Case dan Skenario Penggunaan Menyeluruh

### 18.1 Prinsip pemodelan

Use case menjelaskan tujuan aktor saat menggunakan sistem dan respons
sistem yang terlihat dari luar. Langkah skenario tidak menggunakan nama
class, struct, method, pointer, atau detail komunikasi internal.

Untuk kebutuhan dokumen rencana proyek, kelompok menggunakan **satu
skenario penggunaan menyeluruh** yang mencakup fitur utama aplikasi dari
menu awal sampai pengguna keluar. Secara UML yang lebih ketat, fitur
seperti memainkan pertandingan, melihat riwayat, mengubah pengaturan,
membaca cara bermain, dan keluar dapat dimodelkan sebagai use case
terpisah karena masing-masing memiliki tujuan pengguna sendiri. Skenario
menyeluruh ini tidak berarti seluruh fitur harus digabung menjadi satu
use case pada diagram.

### 18.2 Identitas skenario

  -----------------------------------------------------------------------
  Elemen                              Keterangan
  ----------------------------------- -----------------------------------
  Nama use case/skenario              Menggunakan YouKnowBall dan
                                      Memainkan Pertandingan hingga
                                      Selesai

  Goal                                Menggunakan fitur utama aplikasi,
                                      mulai dari konfigurasi dan
                                      memainkan 8-Ball/9-Ball hingga
                                      melihat hasil, serta mengakses
                                      fitur pendukung aplikasi.

  Level                               User-Goal / skenario penggunaan
                                      menyeluruh

  Primary Actor                       Pemain

  Supporting Actor                    Tidak ada aktor eksternal

  Trigger                             Pemain membuka aplikasi
                                      YouKnowBall.

  Precondition                        Aplikasi telah terpasang dan dapat
                                      dijalankan.

  Postcondition sukses                Pertandingan selesai, hasil
                                      ditampilkan dan disimpan; pemain
                                      dapat melanjutkan ke fitur
                                      pendukung atau keluar aplikasi.

  Postcondition alternatif            Jika pertandingan dibatalkan
                                      sebelum selesai, tidak ada catatan
                                      hasil pertandingan yang disimpan.
  -----------------------------------------------------------------------

### 18.3 Skenario narasi

Pemain membuka aplikasi YouKnowBall dan sistem menampilkan halaman utama
yang menyediakan pilihan Mulai Pertandingan, Riwayat Pertandingan,
Pengaturan Aplikasi, Cara Bermain, dan Keluar. Pemain dapat terlebih
dahulu membuka pengaturan aplikasi untuk menyesuaikan volume musik,
volume efek suara, dan sensitivitas mouse. Setelah selesai, pemain
kembali ke halaman utama. Jika belum memahami permainan, pemain dapat
membuka halaman Cara Bermain untuk membaca penjelasan kontrol, aturan
8-Ball dan 9-Ball, foul, scratch, serta ball-in-hand.

Untuk memulai permainan, pemain memilih Mulai Pertandingan, kemudian
menentukan jenis permainan 8-Ball atau 9-Ball. Sistem menampilkan
pengaturan pertandingan agar pemain dapat memilih lawan, yaitu Pemain
Lokal atau Bot Easy, mengisi nama pemain sesuai mode, serta menentukan
batas waktu per giliran berupa tanpa batas, 15, 30, atau 60 detik.
Setelah konfigurasi dikonfirmasi, sistem menyiapkan meja, bola, pemain,
dan giliran awal, kemudian menampilkan halaman permainan.

Pada gilirannya, pemain mengatur arah bidikan menggunakan mouse pada
area meja. Setelah arah ditentukan, pemain mengatur kekuatan pukulan
melalui indikator cue yang terpisah. Ketika power sedang diatur, arah
bidikan dikunci. Jika ingin mengubah arah, pemain dapat menekan Space
sebelum mouse dilepas untuk membatalkan pengaturan power. Jika mouse
dilepas tanpa pembatalan, sistem menjalankan pukulan menggunakan arah
dan kekuatan yang telah ditentukan. Sistem kemudian mensimulasikan
pergerakan bola sampai seluruh bola berhenti dan mengevaluasi hasilnya
berdasarkan aturan mode permainan yang sedang berlangsung.

Jika terjadi foul atau scratch, sistem mengalihkan giliran kepada lawan
dan memberikan ball-in-hand. Jika pukulan sah, sistem menentukan apakah
pemain mempertahankan giliran atau giliran berpindah berdasarkan hasil
pukulan. Pada mode Bot Easy, Bot mengambil giliran secara otomatis dan
melakukan pukulan melalui mekanisme permainan yang sama. Siklus bidik,
pukul, simulasi, dan evaluasi berlangsung bergantian sampai salah satu
pemain memenuhi kondisi kemenangan. Jika waktu habis ketika pemain
sedang menarik indikator power, sistem langsung menjalankan pukulan
dengan power yang telah tercapai saat waktu habis.

Selama pertandingan, pemain dapat menekan Esc untuk membuka Pause.
Sistem menghentikan sementara timer dan simulasi serta membatalkan
tarikan yang belum menjadi pukulan. Pemain dapat melanjutkan permainan,
membuka pengaturan aplikasi, memulai ulang pertandingan, atau kembali ke
menu utama. Aksi restart dan kembali ke menu memerlukan konfirmasi.
Pertandingan yang belum selesai karena restart atau ditinggalkan tidak
disimpan ke riwayat.

Setelah pertandingan selesai, sistem menampilkan halaman hasil yang
berisi nama pemain, pemenang, jenis permainan, jumlah bola masuk, jumlah
foul, dan durasi pertandingan. Sistem menyimpan hasil pertandingan yang
selesai ke riwayat lokal. Pemain dapat memilih Rematch untuk memulai
pertandingan baru dengan konfigurasi sebelumnya atau kembali ke halaman
utama. Dari halaman utama, pemain dapat membuka daftar riwayat dan
melihat detail pertandingan yang telah selesai, mengubah pengaturan
aplikasi, membaca cara bermain, atau memilih Keluar. Ketika Keluar
dipilih, sistem menampilkan konfirmasi sebelum aplikasi ditutup.

### 18.4 Skenario step by step

  ------------------------------------------------------------------------
                           No. Aktor                 Sistem
  ---------------------------- --------------------- ---------------------
                             1 Pemain membuka        Sistem
                               aplikasi YouKnowBall. menginisialisasi
                                                     aplikasi dan
                                                     menampilkan Main
                                                     Menu.

                             2 Pemain memilih        Sistem menampilkan
                               Pengaturan Aplikasi   volume musik, volume
                               jika ingin            SFX, dan sensitivitas
                               menyesuaikan          mouse.
                               pengaturan.           

                             3 Pemain mengubah       Sistem menerapkan
                               pengaturan yang       serta menyimpan
                               diperlukan dan        pengaturan lokal,
                               kembali.              lalu kembali ke
                                                     halaman asal.

                             4 Pemain memilih Cara   Sistem menampilkan
                               Bermain jika ingin    kontrol, aturan
                               membaca panduan.      8-Ball/9-Ball, foul,
                                                     scratch, dan
                                                     ball-in-hand.

                             5 Pemain kembali ke     Sistem menampilkan
                               Main Menu dan memilih pilihan jenis
                               Mulai Pertandingan.   permainan.

                             6 Pemain memilih 8-Ball Sistem menampilkan
                               atau 9-Ball.          Match Setup sesuai
                                                     pilihan.

                             7 Pemain memilih mode   Sistem menyesuaikan
                               lawan Pemain Lokal    isian nama pemain
                               atau Bot Easy.        dengan mode lawan.

                             8 Pemain mengisi nama   Sistem memvalidasi
                               pemain.               dan menampilkan
                                                     konfigurasi nama.

                             9 Pemain memilih timer  Sistem menyimpan
                               tanpa batas, 15, 30,  pilihan waktu untuk
                               atau 60 detik.        pertandingan
                                                     tersebut.

                            10 Pemain memilih Mulai  Sistem menyiapkan
                               Pertandingan.         rack, meja, pemain,
                                                     controller, dan
                                                     giliran awal.

                            11 Pemain mulai          Sistem menampilkan
                               mengamati halaman     meja, bola, cue,
                               permainan.            informasi pemain
                                                     aktif, target, dan
                                                     timer jika digunakan.

                            12 Pemain menggerakkan   Sistem memperbarui
                               mouse/cue pada area   arah bidikan dan
                               meja.                 indikator prediksi
                                                     lintasan.

                            13 Pemain mengatur power Sistem mengunci arah
                               melalui indikator cue bidikan dan
                               yang terpisah.        memperbarui nilai
                                                     power.

                            14 Pemain menekan Space  Sistem membatalkan
                               sebelum mouse dilepas tarikan power dan
                               jika ingin            mengizinkan pemain
                               membatalkan           mengatur arah
                               pengaturan power.     kembali.

                            15 Pemain melepaskan     Sistem menerima
                               mouse tanpa           perintah pukulan dan
                               membatalkan tarikan.  memulai simulasi.

                            16 Pemain menunggu       Sistem menghitung
                               hingga bola berhenti. gerak, gesekan,
                                                     tumbukan, pantulan,
                                                     dan pocket.

                            17 Tidak ada interaksi   Sistem mengevaluasi
                               pemain selama         fakta hasil pukulan
                               simulasi berlangsung. berdasarkan aturan
                                                     permainan.

                            18 Pemain melanjutkan    Sistem mempertahankan
                               permainan sesuai      atau mengalihkan
                               giliran.              giliran sesuai hasil
                                                     evaluasi.

                            19 Jika terjadi          Sistem memberikan
                               foul/scratch, pemain  giliran kepada lawan
                               mengikuti instruksi   dan mengaktifkan
                               ball-in-hand.         penempatan cue ball.

                            20 Pemain menempatkan    Sistem memvalidasi
                               cue ball pada posisi  posisi agar berada di
                               yang diinginkan.      area yang
                                                     diperbolehkan, tidak
                                                     overlap, dan tidak
                                                     berada di pocket.

                            21 Jika mode Bot Easy    Sistem meminta Bot
                               aktif, pemain         memilih target dan
                               menunggu giliran Bot. menghasilkan perintah
                                                     pukulan.

                            22 Pemain dan Bot        Sistem mengulangi
                               melanjutkan giliran   proses bidik, pukul,
                               masing-masing sampai  simulasi, dan
                               pertandingan selesai. evaluasi.

                            23 Jika timer habis saat Sistem langsung
                               pemain sedang menarik mengeksekusi pukulan
                               indikator power,      dengan power yang
                               pemain tidak          telah tercapai.
                               memperoleh tambahan   
                               waktu.                

                            24 Pemain menekan Esc    Sistem menampilkan
                               jika ingin            Pause, menghentikan
                               menghentikan          timer, dan
                               permainan sementara.  membatalkan tarikan
                                                     yang belum menjadi
                                                     pukulan.

                            25 Pemain memilih        Sistem mengembalikan
                               Lanjutkan.            permainan ke state
                                                     sebelumnya dan
                                                     memulihkan sisa
                                                     timer.

                            26 Pemain memilih        Sistem menampilkan
                               Pengaturan Aplikasi   pengaturan dan
                               dari Pause.           kembali ke Pause
                                                     setelah pengaturan
                                                     selesai.

                            27 Pemain memilih Mulai  Sistem meminta
                               Ulang.                konfirmasi; jika
                                                     disetujui,
                                                     pertandingan aktif
                                                     dibatalkan dan rack
                                                     baru disiapkan tanpa
                                                     menyimpan hasil lama.

                            28 Pemain memilih Menu   Sistem meminta
                               Utama dari Pause.     konfirmasi; jika
                                                     disetujui,
                                                     pertandingan aktif
                                                     dibatalkan tanpa
                                                     menyimpan hasil.

                            29 Pemain menyelesaikan  Sistem mengakhiri
                               pertandingan sampai   pertandingan dan
                               kondisi menang        menampilkan Result.
                               terpenuhi.            

                            30 Pemain melihat        Sistem menampilkan
                               ringkasan hasil       nama pemain,
                               pertandingan.         pemenang, jenis
                                                     permainan, statistik
                                                     bola masuk, foul, dan
                                                     durasi.

                            31 Pemain membuka atau   Sistem menyimpan satu
                               kembali ke fitur lain catatan hasil
                               setelah hasil         pertandingan selesai
                               ditampilkan.          ke riwayat lokal.

                            32 Pemain memilih        Sistem memulai
                               Rematch.              pertandingan baru
                                                     dengan konfigurasi
                                                     sebelumnya.

                            33 Pemain kembali ke     Sistem menampilkan
                               Main Menu dan memilih daftar pertandingan
                               Riwayat Pertandingan. yang telah selesai.

                            34 Pemain memilih salah  Sistem menampilkan
                               satu catatan riwayat. detail pertandingan
                                                     yang dipilih.

                            35 Pemain kembali ke     Sistem menampilkan
                               Main Menu dan memilih Exit Confirmation.
                               Keluar.               

                            36 Pemain mengonfirmasi  Sistem menutup
                               keluar.               aplikasi.
  ------------------------------------------------------------------------

### 18.5 Alur alternatif

-   **A1 --- Pengaturan dibatalkan:** pemain kembali tanpa mengubah
    nilai; sistem kembali ke halaman asal.
-   **A2 --- Cara Bermain ditutup:** sistem kembali ke Main Menu.
-   **A3 --- Pengaturan pertandingan belum lengkap:** sistem meminta
    pemain melengkapi data yang diperlukan sebelum pertandingan dimulai.
-   **A4 --- Power dibatalkan:** Space ditekan sebelum mouse dilepas;
    tarikan dibatalkan dan pemain dapat mengatur arah kembali.
-   **A5 --- Timeout ketika power ditarik:** sistem mengeksekusi pukulan
    dengan power yang telah tercapai saat timer habis.
-   **A6 --- Foul atau scratch:** giliran berpindah kepada lawan dan
    lawan memperoleh ball-in-hand.
-   **A7 --- Posisi cue ball tidak valid:** sistem menolak posisi
    tersebut dan meminta pemain memilih posisi lain.
-   **A8 --- Pause:** timer dan simulasi dihentikan; tarikan yang belum
    menjadi pukulan dibatalkan. Resume mengembalikan state sebelumnya
    dan sisa timer.
-   **A9 --- Restart:** setelah konfirmasi, pertandingan aktif
    dibatalkan, rack baru disiapkan, dan pertandingan yang dibatalkan
    tidak disimpan.
-   **A10 --- Kembali ke menu sebelum pertandingan selesai:** setelah
    konfirmasi, sesi dibatalkan dan tidak disimpan sebagai hasil
    pertandingan.
-   **A11 --- 8-Ball break memasukkan bola 8:** rack diulang sesuai
    ketentuan proyek.
-   **A12 --- 9-Ball break memasukkan bola 9:** bola 9 di-respot dan
    permainan dilanjutkan.
-   **A13 --- Rematch:** sistem membuat pertandingan baru menggunakan
    konfigurasi pertandingan sebelumnya.
-   **A14 --- Riwayat kosong:** sistem menampilkan informasi bahwa belum
    ada pertandingan selesai yang tersimpan.
-   **A15 --- Keluar dibatalkan:** sistem menutup dialog konfirmasi dan
    kembali ke aplikasi.

------------------------------------------------------------------------

## 19. Pembagian Peran Anggota

Pembagian tanggung jawab utama anggota:

  -----------------------------------------------------------------------
  Anggota                 Tanggung Jawab          Tugas yang Dikerjakan
  ----------------------- ----------------------- -----------------------
  Rapid Akbar Sinatria    Tampilan dan navigasi   Membuat halaman utama,
                          aplikasi                pengaturan
                                                  pertandingan, menu
                                                  pause, pengaturan
                                                  aplikasi, cara bermain,
                                                  halaman hasil
                                                  pertandingan, serta
                                                  halaman riwayat
                                                  pertandingan.

  Satya Firma Ashari      Tampilan meja dan       Membuat tampilan meja
                          mekanisme fisika        biliar, bola, stik, dan
                          permainan               enam pocket, serta
                                                  menangani pergerakan
                                                  bola, tumbukan antarb
                                                  bola, pantulan
                                                  bantalan, mekanisme
                                                  arah bidikan, dan
                                                  kekuatan pukulan.

  Muhammad Argo Iman      Logika dan sistem       Membuat sistem
                          pertandingan            permainan 8-Ball dan
                                                  9-Ball, pengaturan
                                                  pergantian giliran
                                                  pemain, sistem pemain
                                                  lokal dan Bot Easy,
                                                  pengelolaan timer
                                                  giliran, penerapan
                                                  aturan pertandingan,
                                                  serta penyimpanan
                                                  riwayat pertandingan.

  Semua anggota           Integrasi, pengujian,   Melakukan integrasi
                          dan penyempurnaan       program, pengujian
                                                  aplikasi, memperbaiki
                                                  bug, mengevaluasi hasil
                                                  pengerjaan,
                                                  menyempurnakan
                                                  implementasi, dan
                                                  menyusun laporan
                                                  proyek.
  -----------------------------------------------------------------------

Pembagian di atas merupakan tanggung jawab utama. Pekerjaan teknis dapat
dikerjakan bersama sesuai ketergantungan dan kebutuhan integrasi.

------------------------------------------------------------------------

## 20. Pembagian Kerja dan WBS Minggu 9--15

WBS mempertahankan penomoran dan deskripsi aktivitas yang digunakan
dalam draft kelompok. Kolom tanggal ditambahkan agar aktivitas dapat
diperiksa berdasarkan rentang waktu. Minggu ke-10 menggunakan tanggal
**5--8 November 2026**.

  -----------------------------------------------------------------------------------------------------------------------------
        Minggu Deskripsi Tanggung Jawab       PIC                          Ketergantungan   Target yang     Tanggal   Tanggal
                                                                                            Diperiksa       Mulai     Selesai
  ------------ ------------------------------ ---------------------------- ---------------- --------------- --------- ---------
             9 0.1 Finalisasi rancangan       Seluruh Anggota              Analisis dan     Rancangan       2 Nov     4 Nov
               proyek: deskripsi, fitur, use                               kesepakatan awal proyek dan      2026      2026
               case, skenario, rancangan                                   proyek.          pembagian tugas           
               class, dan pembagian tugas.                                                  disepakati.               

            10 1.1 Desain Wireframe           Seluruh Anggota              0.1              Desain          5 Nov     8 Nov
               YouKnowBall                                                                  keseluruhan     2026      2026
                                                                                            YouKnowBall.              

            11 2.1 Gerak, gesekan,            Rapid                        1.1 → 2.1 → 2.2  Gerak,          9 Nov     15 Nov
               pantulan`<br>`{=html}2.2                                                     tumbukan, dan   2026      2026
               Tumbukan dan lubang                                                          bola masuk                
                                                                                            dapat diamati.            

            12 3.1 HumanController,           Satya; Argo                  Keduanya         Pukulan pemain  16 Nov    22 Nov
               ShotCommand,                                                mengikuti 2.2.   menghasilkan    2026      2026
               Cue`<br>`{=html}3.2 GameRules,                                               catatan yang              
               ShotResult, RuleOutcome                                                      dapat dinilai.            

            13 4.1 Evaluasi 8-Ball/9-Ball di  Argo                         3.2 → 4.1 → 4.2  Giliran dan     23 Nov    29 Nov
               GameRules`<br>`{=html}4.2                                                    konsekuensi     2026      2026
               Sesi, timer, ball-in-hand                                                    aturan                    
                                                                                            terhubung pada            
                                                                                            sesi.                     

            14 5.1 Bot                        Satya:                       5.1 mengikuti    Mode lawan dan  30 Nov    6 Des
               heuristik`<br>`{=html}5.2      5.1--5.2`<br>`{=html}Argo:   3.1 dan 4.2; 5.2 alur antarmuka  2026      2026
               ScreenManager, HUD, jeda,      5.3                          memakai 3.1,     terintegrasi;             
               AudioManager`<br>`{=html}5.3                                4.2, dan         data lokal                
               StorageManager dan struct data                              kejadian fisika; dapat                     
                                                                           5.3 mengikuti    diperiksa.                
                                                                           4.2.                                       

            15 6.1 Uji integrasi dan          Seluruh Anggota              5.1--5.3 → 6.1 → Temuan utama    7 Des     13 Des
               perbaikan`<br>`{=html}6.2                                   6.2              diperbaiki,     2026      2026
               Laporan akhir dan demo                                                       laporan dan               
                                                                                            demo disiapkan.           
  -----------------------------------------------------------------------------------------------------------------------------

### 20.1 Catatan WBS

1.  Aktivitas `0.1` digunakan untuk minggu ke-9 agar penomoran aktivitas
    `1.1` sampai `6.2` pada draft utama tidak perlu diubah.
2.  PIC pada WBS mengikuti draft aktivitas yang diberikan. Pembagian PIC
    aktivitas perlu dicocokkan kembali dengan pembagian tanggung jawab
    utama pada Bagian 19 sebelum dokumen dikumpulkan, terutama aktivitas
    fisika pada minggu ke-11.
3.  Ketergantungan menunjukkan urutan logis pengerjaan. Aktivitas yang
    berjalan pada minggu sama dapat berlangsung paralel jika
    prasyaratnya tersedia.
4.  Tanggal mengikuti penomoran minggu yang telah dikoreksi: minggu
    ke-10 adalah 5--8 November 2026, minggu ke-11 adalah 9--15 November,
    dan seterusnya.
5.  WBS ini adalah rencana pengerjaan, bukan bukti progres atau
    penyelesaian.

------------------------------------------------------------------------

## 21. Kontrak Perilaku dan Ketentuan Integrasi

  -----------------------------------------------------------------------
  Proses                  Prakondisi              Hasil yang diharapkan
  ----------------------- ----------------------- -----------------------
  Menerima pukulan        Giliran valid, state    Snapshot kondisi
                          mengizinkan, seluruh    dibuat, timer giliran
                          bola diam, perintah     berhenti selama
                          valid, dan waktu        simulasi, dan impuls
                          tersedia.               diberikan.

  Menolak pukulan         Salah satu prasyarat    Tidak ada impuls atau
                          pukulan tidak           simulasi baru.
                          terpenuhi.              

  Menyelesaikan simulasi  Seluruh bola berhenti   `GameRules`
                          dan `ShotStartState`    menghasilkan
                          serta `ShotResult`      `RuleOutcome`.
                          tersedia.               

  Foul/scratch            Hasil pukulan memenuhi  Giliran berpindah dan
                          kondisi foul yang telah lawan mendapat
                          ditetapkan.             ball-in-hand.

  Pause                   Pertandingan belum      Timer dan simulasi
                          selesai.                berhenti; state
                                                  sebelumnya disimpan;
                                                  tarikan yang belum
                                                  menjadi pukulan
                                                  dibatalkan.

  Resume                  Sesi sedang paused.     State sebelumnya dan
                                                  sisa timer dipulihkan.

  Restart                 Pemain mengonfirmasi    Sesi aktif dibatalkan
                          restart.                tanpa catatan hasil,
                                                  lalu rack baru
                                                  disiapkan.

  Kembali ke menu         Pemain mengonfirmasi    Sesi dibatalkan dan
                          pembatalan pertandingan tidak dicatat sebagai
                          aktif.                  pertandingan selesai.

  Simpan hasil            Pertandingan selesai    Satu `MatchRecord`
                          dan hasil belum pernah  disimpan.
                          disimpan.               

  Rematch                 Hasil pertandingan      Pertandingan baru
                          sebelumnya tersedia.    dimulai menggunakan
                                                  konfigurasi sebelumnya.

  Penempatan cue ball     Ball-in-hand aktif.     Posisi hanya diterima
                                                  jika memenuhi validasi
                                                  area, overlap, dan
                                                  pocket.
  -----------------------------------------------------------------------

### 21.1 Batas integrasi antarsubsistem

-   Controller menghasilkan `ShotCommand`; controller tidak menjalankan
    fisika.
-   `MatchSession` memvalidasi perintah dan mengatur siklus pukulan.
-   `Cue` mengubah arah dan power menjadi impuls.
-   `PhysicsEngine` menjalankan simulasi dan mencatat fakta.
-   `GameRules` mengevaluasi fakta dan mengembalikan `RuleOutcome`.
-   `MatchSession` menerapkan hasil evaluasi pada pemain, giliran,
    timer, dan status pertandingan.
-   `StorageManager` menyimpan hasil hanya setelah pertandingan selesai.
-   `ScreenManager` menampilkan keadaan sistem kepada pemain.

------------------------------------------------------------------------

## 22. Hal yang Belum Dikunci

Bagian ini mencegah usulan implementasi disalahartikan sebagai keputusan
final.

### 22.1 Aturan permainan

-   Daftar lengkap seluruh kondisi foul selain scratch.
-   Perilaku timeout ketika pemain tidak sedang menarik power.
-   Penentuan kelompok 8-Ball jika dua kelompok masuk pada pukulan yang
    sama.
-   Rincian break selain dua kasus khusus bola 8 dan bola 9.
-   Detail respot di luar kasus yang telah disepakati.
-   Penanganan kontak pertama yang hampir bersamaan.
-   Aturan untuk kondisi permainan macet atau tidak ada kemajuan.

### 22.2 Implementasi teknis

-   Nilai koefisien gesekan, restitusi, stop threshold, ukuran bola,
    skala meja, dan substep simulasi.
-   Rumus sensitivitas mouse dan batas minimum/maksimum power.
-   Algoritma rinci Bot Easy dan fallback.
-   Detail perhitungan prediksi lintasan.
-   Format TXT, delimiter, ID catatan, serta penanganan file hilang atau
    rusak.
-   Definisi pasti statistik pukulan dan bola masuk.
-   Aset visual, audio, font, serta lisensinya.
-   Kecocokan versi SFML dengan compiler dan toolchain yang digunakan.

### 22.3 Konsistensi dokumen dan pembagian kerja

-   PIC aktivitas fisika pada WBS minggu ke-11 perlu diselaraskan dengan
    tabel pembagian peran utama.
-   Signature method dan tipe data final perlu dicocokkan dengan
    implementasi.
-   Relasi dan multiplicity Class Diagram perlu diverifikasi berdasarkan
    kepemilikan objek yang benar-benar diterapkan.
-   Use Case Diagram dapat memisahkan tujuan pengguna seperti bermain,
    melihat riwayat, mengubah pengaturan, membaca panduan, dan keluar,
    walaupun dokumen ini memuat satu skenario penggunaan menyeluruh.

Hal yang belum dikunci tidak membatalkan scope yang sudah ditetapkan.
Jangan menambahkan fitur baru hanya karena rincian teknisnya belum
selesai.

------------------------------------------------------------------------

## 23. Rujukan

Desain dan Pemrograman Berorientasi Objek: Studi Kasus. (t.t.). *Materi
perkuliahan dalam bentuk PowerPoint.*

World Pool-Billiard Association. (2026, 21 Oktober). *WPA Rules*.
https://wpapool.com/wp-content/uploads/2026/10/WPA-Rules-2026-10-21-211.pdf

**Catatan rujukan:** Dokumen WPA digunakan sebagai sumber aturan biliar.
YouKnowBall menerapkan adaptasi aturan untuk ruang lingkup proyek,
sehingga tidak semua ketentuan WPA otomatis diterapkan. Materi
perkuliahan digunakan sebagai acuan pendekatan RDD, CRC, dan rancangan
berorientasi objek.

------------------------------------------------------------------------

## 24. Riwayat Perubahan

### Versi 02 --- 10 November 2026

-   Mengonsolidasikan keputusan produk dan arsitektur dari dokumen acuan
    sebelumnya serta pembahasan lanjutan.
-   Memastikan nama produk YouKnowBall, mode 8-Ball/9-Ball, Pemain
    Lokal/Bot Easy, pilihan timer, kontrol arah dan power terpisah,
    serta penyimpanan TXT tercatat konsisten.
-   Mempertahankan baseline 14 class utama dan 8 struct pendukung.
-   Menyempurnakan uraian CRC, Knowing, Doing, atribut, method utama,
    dan collaborator untuk seluruh class.
-   Menuliskan deskripsi struct sebagai paragraf per objek tanpa
    memaksakan method.
-   Memperluas skenario menjadi skenario penggunaan menyeluruh yang
    mencakup pertandingan dan fitur pendukung aplikasi.
-   Menambahkan pembagian peran anggota serta WBS minggu ke-9 sampai
    minggu ke-15.
-   Menyesuaikan kalender WBS sehingga minggu ke-10 berlangsung pada
    5--8 November 2026.
-   Memisahkan keputusan yang telah ditetapkan dari rincian yang masih
    perlu dikonfirmasi.

### Versi 01 --- 8 November 2026

Dokumen acuan awal yang mengonsolidasikan ruang lingkup, kontrol, aturan
dasar, arsitektur 14 class, 8 struct, alur pukulan, dan skenario
penggunaan.

------------------------------------------------------------------------

**Acuan utama proyek YouKnowBall --- Kelompok 9.**\
Gunakan dokumen ini sebagai referensi bersama. Jika keputusan baru
disepakati, perbarui bagian terkait dan riwayat perubahan agar seluruh
anggota menggunakan acuan versi yang sama.

------------------------------------------------------------------------

# Bagian B --- Penyelarasan Keputusan Terbaru (MD v03)

Bagian ini mempertahankan isi MD v03 sebagai lapisan penyelarasan. Jika
ada ketentuan yang bertentangan dengan Bagian A, keputusan MD v03 yang
berlaku. Ketentuan Bagian A yang tidak bertentangan tetap menjadi bagian
dari acuan final.

## 1. Status dokumen

Dokumen v03 merupakan acuan terbaru untuk ruang lingkup, keputusan
permainan, rancangan OOP, kontrak method, alur penggunaan, pembagian
tanggung jawab, dan jadwal YouKnowBall. Keputusan di dalamnya menjadi
baseline implementasi. Perubahan hanya dilakukan jika ada kendala teknis
nyata atau arahan dosen, dan dampaknya harus diperiksa pada kode,
diagram, skenario, WBS, serta pengujian.

Prinsip rancangan: 1. Mempertahankan **14 class dan 8 struct**. Tidak
menambah class/struct untuk fungsi kecil yang masih wajar digabung. 2.
Setiap class memiliki tanggung jawab utama yang tidak tumpang tindih. 3.
`PhysicsEngine` melaporkan fakta fisika; `GameRules` mengevaluasi
aturan; `MatchSession` menerapkan keputusan dan mengatur siklus
pertandingan. 4. Pemain manusia dan bot menghasilkan `ShotCommand` yang
sama dan menggunakan alur simulasi serta aturan yang sama. 5.
Penyimpanan menggunakan file TXT lokal, tanpa server, akun daring, atau
database. 6. UI memakai koordinat logis 16:9 dan tidak meregang ketika
ukuran window berubah.

## 2. Ringkasan produk dan ruang lingkup

YouKnowBall adalah permainan biliar 2D tampak atas untuk desktop
menggunakan C++ dan SFML. Permainan menyediakan 8-Ball dan 9-Ball dengan
dua mode lawan: dua pemain lokal bergantian pada satu perangkat atau
satu pemain melawan Bot Easy.

### 2.1 Fitur dalam ruang lingkup

-   Menu utama, navigasi halaman, pengaturan pertandingan.
-   Pilihan 8-Ball/9-Ball, Pemain Lokal/Bot Easy, nama pemain.
-   Timer giliran: tanpa batas, 15, 30, atau 60 detik.
-   Meja, bola, cue, indikator arah dan power, prediksi lintasan
    sederhana.
-   Gerak bola, gesekan, tumbukan, cushion, dan deteksi pocket.
-   Aturan dasar 8-Ball/9-Ball, foul, scratch, pergantian giliran,
    ball-in-hand.
-   Pause/resume, hasil pertandingan, riwayat dan detail riwayat.
-   Pengaturan musik, SFX, sensitivitas mouse, Windowed/Fullscreen.
-   Halaman cara bermain dan konfirmasi keluar.
-   Penyimpanan pengaturan dan hasil pertandingan selesai ke TXT.

### 2.2 Di luar ruang lingkup

Multiplayer online, matchmaking, akun/server/database, Bot Normal/Hard,
spin, jump shot, replay, turnamen, Pocket Challenge, dan melanjutkan
pertandingan yang belum selesai setelah aplikasi ditutup.

### 2.3 Halaman aplikasi

  ---------------------------------------------------------------------
  Halaman                            Fungsi
  ---------------------------------- ----------------------------------
  Menu Utama                         Main, Riwayat, Pengaturan, Cara
                                     Bermain, Keluar

  Pengaturan Pertandingan            Jenis permainan, mode lawan, nama,
                                     batas waktu

  Permainan                          Meja, bola, cue, arah/prediksi,
                                     power, giliran, target, timer,
                                     pause

  Pause                              Lanjutkan, restart, kembali ke
                                     menu dengan konfirmasi

  Hasil                              Pemenang dan ringkasan
                                     pertandingan

  Riwayat                            Daftar pertandingan selesai

  Detail Riwayat                     Detail satu pertandingan

  Pengaturan                         Volume musik/SFX, sensitivitas
                                     mouse, mode tampilan

  Cara Bermain                       Kontrol, aturan, foul, scratch,
                                     ball-in-hand

  Konfirmasi Keluar                  Konfirmasi penutupan aplikasi
  ---------------------------------------------------------------------

## 3. Keputusan perilaku permainan

### 3.1 Kontrol pukulan

1.  Mouse mengatur arah cue.
2.  Indikator cue/stik terpisah mengatur power saja, bukan arah.
3.  Saat power diatur, arah dikunci.
4.  Menekan `Space` sebelum mouse dilepas membatalkan pengaturan power
    dan mengembalikan pemain ke tahap mengarahkan pukulan.
5.  Melepas mouse secara normal menjalankan pukulan.
6.  Angka persentase power tidak wajib; indikator visual cukup.
7.  Pause membatalkan input drag yang belum menghasilkan pukulan agar
    tidak terjadi tembakan tak sengaja.

### 3.2 Timer

Pilihan waktu per giliran adalah tanpa batas, 15, 30, atau 60 detik. -
Timer berjalan saat pemain mengarahkan cue dan mengatur power. - Timer
berhenti saat bola bergerak dan saat pause. - Resume meneruskan sisa
waktu. - Timeout bukan foul. - Timeout ketika pemain sedang mengatur
power langsung menjalankan pukulan dengan power saat itu, tanpa tambahan
waktu. - Timeout ketika pemain tidak sedang mengatur power langsung
memindahkan giliran kepada lawan, tanpa foul dan tanpa ball-in-hand. -
Timer giliran baru berjalan ketika pemain berikutnya siap bermain.

### 3.3 Aturan 8-Ball

-   Solid bernomor 1--7; stripe 9--15.
-   Awal permainan meja terbuka, kelompok belum ditentukan.
-   Kelompok ditentukan ketika satu pukulan sah memasukkan bola dari
    satu kelompok saja.
-   Jika solid dan stripe masuk bersamaan saat meja terbuka, kelompok
    tidak ditentukan; meja tetap terbuka.
-   Kelompok ditentukan pada pukulan berikutnya yang secara sah
    memasukkan bola dari satu kelompok saja.
-   Pukulan sah yang memasukkan bola kelompok sendiri mempertahankan
    giliran.
-   Bola 8 masuk sebelum seluruh kelompok sendiri habis berarti kalah.
-   Bola 8 masuk secara sah setelah kelompok sendiri habis berarti
    menang.
-   Bola 8 masuk bersama scratch/foul berarti pemain yang memukul kalah.
-   Bola 8 masuk saat break dikembalikan ke meja dan permainan
    dilanjutkan.

### 3.4 Aturan 9-Ball

-   Bola bernomor terendah yang masih aktif harus terkena pertama.
-   Bola lain boleh masuk selama kontak pertama mengenai bola terendah
    yang masih aktif.
-   Bola 9 masuk secara sah berarti menang.
-   Bola 9 masuk bersama foul tidak menghasilkan kemenangan; bola 9
    dikembalikan ke meja dan foul diproses.
-   Bola 9 masuk saat break dikembalikan ke meja dan permainan
    dilanjutkan.

### 3.5 Foul, scratch, ball-in-hand

-   Scratch adalah cue ball masuk pocket dan dihitung sebagai foul.
-   Foul memberikan giliran kepada lawan dan hak ball-in-hand.
-   Pemain yang mendapat ball-in-hand boleh menempatkan cue ball sebelum
    pukulan berikutnya.
-   Posisi harus berada di area permainan, tidak bertumpuk dengan bola
    aktif lain, dan tidak di dalam pocket.
-   `Table` memvalidasi posisi; `GameRules` menentukan apakah hak
    ball-in-hand diberikan; `MatchSession` mengatur fase penempatannya.
-   Timeout biasa bukan foul dan tidak memberikan ball-in-hand.

Daftar foul selain scratch hanya boleh dinyatakan sebagai fitur final
jika benar-benar disepakati, diimplementasikan, dan diuji. Jangan
mengklaim seluruh aturan resmi pool telah diterapkan jika implementasi
hanya mencakup aturan dasar proyek.

### 3.6 Prediksi lintasan

Prediksi dibatasi pada garis cue ball sampai perkiraan tumbukan pertama
dan arah sederhana bola objek setelah tumbukan. Prediksi hanya visual,
tidak mengubah posisi bola dan tidak memutuskan aturan.

### 3.7 Mode tampilan

-   Mode: Windowed dan Fullscreen.
-   Rasio konten logis: **16:9**.
-   Windowed dapat di-resize tetapi konten tetap 16:9; ukuran minimum
    ditetapkan sebagai konstanta implementasi agar UI terbaca.
-   Fullscreen menggunakan area layar yang tersedia. Jika rasio layar
    bukan 16:9, gunakan letterbox/pillarbox; jangan meregangkan konten.
-   Posisi mouse dikonversi dari koordinat piksel ke koordinat logis
    agar arah cue tetap akurat setelah resize.
-   Mode dan ukuran window disimpan pada pengaturan aplikasi.

## 4. Arsitektur final: 14 class dan 8 struct

### 4.1 Empat belas class

  ---------------------------------------------------------------------
                          No. Class                Tanggung jawab
  --------------------------- -------------------- --------------------
                            1 `GameApp`            Window SFML, event
                                                   loop, siklus
                                                   aplikasi, koordinasi
                                                   tingkat aplikasi

                            2 `ScreenManager`      Halaman aktif,
                                                   navigasi, input
                                                   antarmuka, delegasi
                                                   update/render
                                                   halaman

                            3 `MatchSession`       Siklus pertandingan,
                                                   pemain aktif,
                                                   controller, timer,
                                                   pause, pergantian
                                                   giliran, hasil

                            4 `Player`             Identitas, kelompok
                                                   bola, statistik
                                                   pemain

                            5 `PlayerController`   Kontrak umum sumber
                                                   perintah pukulan

                            6 `HumanController`    Input manusia
                                                   menjadi
                                                   `ShotCommand`

                            7 `BotController`      Strategi Bot Easy
                                                   dan `ShotCommand`

                            8 `Table`              Kumpulan bola,
                                                   pocket, geometri,
                                                   validasi posisi

                            9 `Ball`               Keadaan fisik satu
                                                   bola

                           10 `Cue`                Arah/power, impuls
                                                   pukulan, prediksi
                                                   lintasan sederhana

                           11 `PhysicsEngine`      Gerak, gesekan,
                                                   tumbukan, cushion,
                                                   deteksi pocket

                           12 `GameRules`          Evaluasi aturan
                                                   8-/9-Ball, foul,
                                                   ball-in-hand,
                                                   menang/kalah

                           13 `StorageManager`     Baca/tulis
                                                   pengaturan dan
                                                   riwayat TXT

                           14 `AudioManager`       Musik, SFX, volume
  ---------------------------------------------------------------------

### 4.2 Delapan struct

    No. Struct             Tanggung jawab data
  ----- ------------------ -----------------------------------------------
      1 `MatchConfig`      Konfigurasi pertandingan
      2 `AppSettings`      Audio, sensitivitas mouse, mode/ukuran window
      3 `MatchRecord`      Ringkasan pertandingan selesai
      4 `PocketData`       Posisi dan radius/area pocket
      5 `ShotCommand`      Arah dan power pukulan
      6 `ShotStartState`   Snapshot kondisi penting sebelum pukulan
      7 `ShotResult`       Fakta fisik yang terjadi selama pukulan
      8 `RuleOutcome`      Keputusan aturan setelah evaluasi

### 4.3 Enum pendukung

Enum bukan class/struct tambahan.

``` cpp
enum class GameType { EIGHT_BALL, NINE_BALL };
enum class OpponentType { LOCAL_PLAYER, BOT };
enum class DisplayMode { WINDOWED, FULLSCREEN };
enum class ScreenType {
    MAIN_MENU, MATCH_SETUP, GAME, PAUSE, RESULT,
    HISTORY, SETTINGS, HOW_TO_PLAY, EXIT_CONFIRM
};
enum class MatchState {
    SETUP, WAITING, AIMING, POWER_SETTING, BALL_IN_HAND,
    SIMULATING, PAUSED, FINISHED
};
enum class BallGroup { NONE, SOLID, STRIPE };
enum class FoulType { NONE, SCRATCH };
enum class SoundType {
    BALL_COLLISION, CUSHION_HIT, BALL_POCKETED, CUE_HIT, UI_CLICK
};
```

Jenis foul tambahan hanya dimasukkan bila scope dan implementasinya
telah disepakati.

## 5. Kontrak method dan batas tanggung jawab

Kontrak berikut mengunci pemilik keputusan dan aliran data. Nama teknis
dapat disesuaikan dengan gaya kode tim, tetapi tanggung jawabnya tidak
boleh dipindahkan sembarangan.

Notasi: `const T&` berarti membaca tanpa mengubah; `T&` berarti objek
boleh diubah; `const` di akhir method berarti method tidak mengubah
keadaan objek. Gunakan `std::optional<T>` hanya jika standar compiler
mendukungnya; jika tidak, gunakan `bool` dan parameter output.

### 5.1 `GameApp`

**Batas:** mengelola window dan loop aplikasi. Tidak menggambar detail
setiap halaman, tidak mengatur aturan, giliran, atau fisika.

  -------------------------------------------------------------------------------------
  Method                                                     Kontrak
  ---------------------------------------------------------- --------------------------
  `GameApp()`                                                Menyiapkan keadaan awal.

  `bool initialize()`                                        Memuat `AppSettings`
                                                             melalui `StorageManager`,
                                                             membuat window sesuai
                                                             mode, menginisialisasi
                                                             komponen; mengembalikan
                                                             status berhasil.

  `void run()`                                               Menjalankan loop event,
                                                             update, dan render selama
                                                             aplikasi aktif.

  `void processEvents()`                                     Membaca event window SFML;
                                                             event antarmuka diteruskan
                                                             ke `ScreenManager`.

  `void update(float deltaTime)`                             Meminta komponen aktif
                                                             melakukan update; tidak
                                                             menghitung fisika/aturan
                                                             sendiri.

  `void render()`                                            Membersihkan window,
                                                             memanggil render
                                                             `ScreenManager`, lalu
                                                             menampilkan frame.

  `void applyDisplaySettings(const AppSettings& settings)`   Menerapkan
                                                             Windowed/Fullscreen dan
                                                             ukuran; menjaga viewport
                                                             16:9 serta pemetaan
                                                             koordinat.

  `void shutdown()`                                          Menyimpan pengaturan
                                                             terakhir bila diperlukan
                                                             dan melepas resource.
  -------------------------------------------------------------------------------------

### 5.2 `ScreenManager`

**Batas:** mengelola halaman, navigasi, dan delegasi
input/update/render. Tidak memiliki window, aturan biliar, atau simulasi
fisika.

  --------------------------------------------------------------------------------
  Method                                              Kontrak
  --------------------------------------------------- ----------------------------
  `void setScreen(ScreenType screen)`                 Mengganti halaman aktif dan
                                                      menyiapkan transisi halaman.

  `ScreenType getCurrentScreen() const`               Mengembalikan halaman aktif.

  `void handleEvent(const sf::Event& event)`          Meneruskan event ke halaman
                                                      aktif/controller yang
                                                      relevan.

  `void update(float deltaTime)`                      Memperbarui halaman aktif
                                                      dan sesi jika halaman
                                                      permainan sedang aktif.

  `void render(sf::RenderTarget& target)`             Meminta halaman aktif
                                                      menggambar elemen visual ke
                                                      target.

  `void setViewport(const sf::FloatRect& viewport)`   Memperbarui area render
                                                      logis setelah window berubah
                                                      ukuran.

  `void openMatchSetup()`                             Membuka pengaturan
                                                      pertandingan.

  `void openSettings()`                               Membuka pengaturan aplikasi.

  `void openHistory()`                                Membuka riwayat.

  `void openHowToPlay()`                              Membuka cara bermain.
  --------------------------------------------------------------------------------

`ScreenManager` adalah pengelola antarmuka. Komponen halaman menampilkan
tombol, panel, teks, meja, HUD, dan dekorasi. Tidak perlu satu class
utama baru untuk setiap halaman jika dapat dikelola secara wajar dalam
struktur UI yang sudah ada.

### 5.3 `MatchSession`

**Batas:** koordinator alur pertandingan. Tidak menghitung gerak bola,
membaca mouse mentah, atau memutuskan aturan sendiri.

  --------------------------------------------------------------------------------
  Method                                              Kontrak
  --------------------------------------------------- ----------------------------
  `bool startMatch(const MatchConfig& config)`        Memvalidasi konfigurasi dan
                                                      menyiapkan pemain,
                                                      controller, meja, giliran,
                                                      timer, serta status.

  `void update(float deltaTime)`                      Memperbarui fase
                                                      pertandingan; memanggil
                                                      fisika saat simulasi,
                                                      evaluasi aturan saat bola
                                                      berhenti, dan
                                                      timer/controller saat
                                                      giliran aktif.

  `void submitShot(const ShotCommand& command)`       Menyimpan snapshot awal,
                                                      mengubah status ke simulasi,
                                                      dan memulai pukulan.

  `void beginBallInHand()`                            Mengubah fase agar pemain
                                                      dapat menempatkan cue ball.

  `bool placeCueBall(const sf::Vector2f& position)`   Meminta `Table` memvalidasi
                                                      posisi; menerapkan hanya
                                                      jika valid.

  `void pauseMatch()`                                 Menghentikan timer dan
                                                      membatalkan input controller
                                                      yang belum dikirim.

  `void resumeMatch()`                                Melanjutkan fase sebelumnya
                                                      dan sisa timer.

  `void restartMatch()`                               Mengatur ulang pertandingan
                                                      dengan konfigurasi yang
                                                      sama; tidak menyimpan
                                                      pertandingan yang
                                                      dibatalkan.

  `void switchTurn()`                                 Mengganti pemain aktif dan
                                                      menyiapkan controller/timer
                                                      berikutnya.

  `void handleTimeout()`                              Saat power sedang diatur,
                                                      jalankan pukulan pada power
                                                      saat itu; jika tidak,
                                                      pindahkan giliran tanpa
                                                      foul/ball-in-hand.

  `void finishMatch(int winnerIndex)`                 Mengakhiri pertandingan,
                                                      menghentikan timer,
                                                      membentuk record, meminta
                                                      penyimpanan.

  `int getActivePlayerIndex() const`                  Mengembalikan indeks pemain
                                                      aktif.

  `MatchState getState() const`                       Mengembalikan fase
                                                      pertandingan.

  `const Player& getActivePlayer() const`             Memberikan data pemain aktif
                                                      untuk UI/evaluasi.

  `const MatchConfig& getConfig() const`              Mengembalikan konfigurasi
                                                      aktif.
  --------------------------------------------------------------------------------

Urutan pukulan: controller membuat `ShotCommand` → `MatchSession`
menyimpan `ShotStartState` → `Cue` menghitung impuls → `PhysicsEngine`
menjalankan simulasi dan mengumpulkan `ShotResult` → setelah bola
berhenti, `GameRules` mengembalikan `RuleOutcome` → `MatchSession`
menerapkan hasil dan menyiapkan fase/giliran berikutnya.

### 5.4 `Player`

**Batas:** data pemain dan statistik saja. Tidak membaca input, timer,
atau menentukan pemenang.

  -------------------------------------------------------------------------
  Method                                    Kontrak
  ----------------------------------------- -------------------------------
  `Player(const std::string& name)`         Membuat pemain dengan nama dan
                                            statistik awal.

  `void setName(const std::string& name)`   Mengubah nama.

  `const std::string& getName() const`      Mengambil nama.

  `void setBallGroup(BallGroup group)`      Menetapkan kelompok.

  `BallGroup getBallGroup() const`          Mengambil kelompok.

  `void addPocketedBall(int ballNumber)`    Memperbarui statistik bola
                                            masuk.

  `void addFoul()`                          Menambah jumlah foul.

  `int getPocketedCount() const`            Mengambil jumlah bola masuk.

  `int getFoulCount() const`                Mengambil jumlah foul.

  `void resetStats()`                       Mengatur ulang statistik.
  -------------------------------------------------------------------------

### 5.5 `PlayerController` (abstract)

**Batas:** kontrak umum controller; tidak mengetahui detail input
manusia atau strategi bot.

  ------------------------------------------------------------------------------
  Method                                           Kontrak
  ------------------------------------------------ -----------------------------
  `virtual void update(float deltaTime) = 0`       Memperbarui proses
                                                   pengambilan keputusan.

  `virtual bool hasShotCommand() const = 0`        Memeriksa apakah perintah
                                                   siap dikirim.

  `virtual ShotCommand consumeShotCommand() = 0`   Mengambil satu perintah dan
                                                   mengosongkan status siap.

  `virtual void cancelPendingInput() = 0`          Membatalkan input/perintah
                                                   yang belum dikirim.

  `virtual ~PlayerController() = default`          Destruktor virtual.
  ------------------------------------------------------------------------------

### 5.6 `HumanController`

**Batas:** input manusia menjadi `ShotCommand`. Tidak mengubah bola,
menjalankan fisika, atau memutuskan foul.

  -----------------------------------------------------------------------------------------------------------
  Method                                                                                 Kontrak
  -------------------------------------------------------------------------------------- --------------------
  `void handleEvent(const sf::Event& event, const sf::Vector2f& logicalMousePosition)`   Membaca input
                                                                                         mouse/keyboard dalam
                                                                                         koordinat logis dan
                                                                                         memperbarui
                                                                                         arah/power melalui
                                                                                         `Cue`.

  `void update(float deltaTime)`                                                         Memperbarui status
                                                                                         input dan kesiapan
                                                                                         perintah.

  `bool hasShotCommand() const`                                                          Memeriksa perintah
                                                                                         siap.

  `ShotCommand consumeShotCommand()`                                                     Mengambil satu
                                                                                         perintah pukulan.

  `void cancelPendingInput()`                                                            Membatalkan drag dan
                                                                                         perintah yang belum
                                                                                         dikirim.

  `void setCue(Cue* cue)`                                                                Menghubungkan
                                                                                         controller ke cue
                                                                                         yang digunakan.
  -----------------------------------------------------------------------------------------------------------

Konversi koordinat piksel ke koordinat logis dilakukan lapisan
window/aplikasi sebelum event diteruskan.

### 5.7 `BotController`

**Batas:** memilih pukulan Bot Easy dan mengemasnya menjadi
`ShotCommand`. Tidak mengubah meja atau menerapkan hasil aturan.

  --------------------------------------------------------------------------------------------------------------
  Method                                                                                     Kontrak
  ------------------------------------------------------------------------------------------ -------------------
  `void update(float deltaTime)`                                                             Memeriksa giliran
                                                                                             bot dan menyiapkan
                                                                                             perintah jika belum
                                                                                             ada.

  `ShotCommand chooseShot(const Table& table, const Player& bot, GameType gameType) const`   Memilih target,
                                                                                             arah, dan power
                                                                                             sederhana
                                                                                             berdasarkan keadaan
                                                                                             meja.

  `bool hasShotCommand() const`                                                              Memeriksa perintah
                                                                                             siap.

  `ShotCommand consumeShotCommand()`                                                         Mengambil satu
                                                                                             perintah dan
                                                                                             mengosongkan status
                                                                                             siap.

  `void cancelPendingInput()`                                                                Menghapus perintah
                                                                                             tertunda.

  `void setContext(const Table* table, const Player* bot, GameType gameType)`                Memberikan konteks
                                                                                             baca yang
                                                                                             diperlukan bot.
  --------------------------------------------------------------------------------------------------------------

Bot Easy menggunakan strategi sederhana. Ia tetap mengirim perintah
melalui alur yang sama dengan pemain manusia.

### 5.8 `Table`

**Batas:** penyimpanan bola/pocket, geometri, dan validasi posisi. Tidak
menjalankan fisika atau memutuskan aturan.

  ------------------------------------------------------------------------------------------
  Method                                                            Kontrak
  ----------------------------------------------------------------- ------------------------
  `void initialize(GameType gameType)`                              Menyiapkan geometri,
                                                                    pocket, dan susunan bola
                                                                    awal.

  `Ball* getBall(int ballNumber)`                                   Mengambil bola
                                                                    berdasarkan nomor atau
                                                                    `nullptr`.

  `const Ball* getBall(int ballNumber) const`                       Versi baca-saja.

  `std::vector<Ball>& getBalls()`                                   Akses perubahan internal
                                                                    untuk sistem fisika.

  `const std::vector<Ball>& getBalls() const`                       Akses baca-saja.

  `const std::vector<PocketData>& getPockets() const`               Mengambil data pocket.

  `bool isInsidePlayableArea(const sf::Vector2f& position) const`   Memeriksa titik berada
                                                                    dalam area permainan.

  `bool canPlaceCueBall(const sf::Vector2f& position) const`        Memeriksa batas meja,
                                                                    overlap bola aktif, dan
                                                                    pocket.

  `void setCueBallPosition(const sf::Vector2f& position)`           Mengubah posisi cue ball
                                                                    setelah validasi.

  `void resetBalls(GameType gameType)`                              Mengatur ulang susunan
                                                                    bola.

  `void respotBall(int ballNumber)`                                 Mengembalikan bola ke
                                                                    spot yang ditentukan.

  `bool areAllBallsStopped() const`                                 Memeriksa apakah seluruh
                                                                    bola telah berhenti.
  ------------------------------------------------------------------------------------------

### 5.9 `Ball`

**Batas:** keadaan satu bola. Tidak mendeteksi tumbukan atau pocket.

  -----------------------------------------------------------------------------------------
  Method                                                           Kontrak
  ---------------------------------------------------------------- ------------------------
  `Ball(int number, const sf::Vector2f& position, float radius)`   Membuat bola.

  `void setPosition(const sf::Vector2f& position)` /               Mengubah/mengambil
  `const sf::Vector2f& getPosition() const`                        posisi.

  `void setVelocity(const sf::Vector2f& velocity)` /               Mengubah/mengambil
  `const sf::Vector2f& getVelocity() const`                        kecepatan.

  `void applyImpulse(const sf::Vector2f& impulse)`                 Menambahkan impuls pada
                                                                   kecepatan sesuai
                                                                   parameter fisika.

  `void updatePosition(float deltaTime)`                           Memperbarui posisi;
                                                                   dipanggil
                                                                   `PhysicsEngine`.

  `void stop()`                                                    Mengatur kecepatan
                                                                   menjadi nol.

  `bool isMoving() const`                                          Memeriksa kecepatan
                                                                   terhadap ambang
                                                                   berhenti.

  `void setPocketed(bool pocketed)` / `bool isPocketed() const`    Mengatur/mengambil
                                                                   status pocket.

  `int getNumber() const` / `float getRadius() const`              Mengambil nomor/radius.
  -----------------------------------------------------------------------------------------

### 5.10 `Cue`

**Batas:** arah, power, impuls, dan prediksi visual. Tidak membaca event
langsung atau memutuskan kapan pemain boleh memukul.

  ------------------------------------------------------------------------------------------------
  Method                                                                    Kontrak
  ------------------------------------------------------------------------- ----------------------
  `void setAimDirection(const sf::Vector2f& direction)`                     Menyimpan arah bidikan
                                                                            ternormalisasi.

  `const sf::Vector2f& getAimDirection() const`                             Mengambil arah.

  `void setPower(float power)` / `float getPower() const`                   Mengatur/mengambil
                                                                            power dalam rentang
                                                                            valid.

  `sf::Vector2f calculateImpulse() const`                                   Menghitung vektor
                                                                            impuls dari arah dan
                                                                            power.

  `std::vector<sf::Vector2f> predictTrajectory(const Table& table) const`   Menghasilkan garis
                                                                            prediksi tumbukan
                                                                            pertama dan arah awal
                                                                            bola objek tanpa
                                                                            mengubah meja.

  `void reset()`                                                            Mengatur ulang status
                                                                            arah/power setelah
                                                                            pukulan atau
                                                                            pembatalan.
  ------------------------------------------------------------------------------------------------

### 5.11 `PhysicsEngine`

**Batas:** fakta fisika saja. Tidak menyimpulkan foul, kemenangan, atau
pergantian giliran.

  --------------------------------------------------------------------------------------------
  Method                                                               Kontrak
  -------------------------------------------------------------------- -----------------------
  `void beginShot()`                                                   Mengosongkan catatan
                                                                       kejadian untuk pukulan
                                                                       baru.

  `void applyCueImpulse(Ball& cueBall, const sf::Vector2f& impulse)`   Memberikan impuls awal
                                                                       ke cue ball.

  `void update(Table& table, float deltaTime)`                         Memperbarui gerak,
                                                                       gesekan, tumbukan,
                                                                       cushion, dan deteksi
                                                                       pocket untuk satu
                                                                       langkah simulasi.

  `void resolveBallCollisions(Table& table)`                           Menyelesaikan tumbukan
                                                                       antarb bola dan
                                                                       mencatat kontak.

  `void resolveCushionCollisions(Table& table)`                        Menyelesaikan pantulan
                                                                       cushion dan mencatat
                                                                       kontak.

  `void detectPocketedBalls(Table& table)`                             Menandai bola yang
                                                                       masuk pocket dan
                                                                       mencatat nomornya.

  `bool areAllBallsStopped(const Table& table) const`                  Memeriksa akhir
                                                                       simulasi.

  `ShotResult getShotResult() const`                                   Mengembalikan fakta
                                                                       yang tercatat selama
                                                                       pukulan.
  --------------------------------------------------------------------------------------------

Fakta yang dicatat meliputi bola pertama yang terkena, bola yang masuk,
cue ball masuk/tidak, dan kontak cushion yang relevan.

### 5.12 `GameRules`

**Batas:** evaluasi aturan dari fakta dan keadaan meja. Tidak
menjalankan simulasi, mengganti giliran, menyimpan file, atau
memindahkan cue ball.

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Method                                                                                                                                                                               Kontrak
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ---------------------
  `RuleOutcome evaluateShot(GameType gameType, const ShotStartState& startState, const ShotResult& result, const Table& table, const Player& shooter, const Player& opponent) const`   Mengevaluasi satu
                                                                                                                                                                                       pukulan dan
                                                                                                                                                                                       mengembalikan
                                                                                                                                                                                       keputusan aturan.

  `bool isLegalFirstContact(GameType gameType, const ShotStartState& startState, const ShotResult& result, const Player& shooter) const`                                               Memeriksa kontak
                                                                                                                                                                                       pertama sesuai jenis
                                                                                                                                                                                       permainan/kelompok.

  `bool isFoul(const ShotResult& result, const ShotStartState& startState, GameType gameType, const Player& shooter) const`                                                            Menilai foul yang
                                                                                                                                                                                       benar-benar masuk
                                                                                                                                                                                       implementasi.

  `BallGroup determineGroup(const ShotResult& result) const`                                                                                                                           Mengembalikan
                                                                                                                                                                                       SOLID/STRIPE hanya
                                                                                                                                                                                       jika satu kelompok
                                                                                                                                                                                       tunggal dapat
                                                                                                                                                                                       ditentukan; selain
                                                                                                                                                                                       itu NONE.

  `int getLowestActiveBall(const Table& table) const`                                                                                                                                  Mengambil nomor bola
                                                                                                                                                                                       aktif terendah untuk
                                                                                                                                                                                       9-Ball.

  `bool isEightBallWin(const ShotResult& result, const Player& shooter, const Table& table) const`                                                                                     Memeriksa kondisi
                                                                                                                                                                                       menang/kalah 8-Ball
                                                                                                                                                                                       berdasarkan status
                                                                                                                                                                                       kelompok dan bola 8.

  `bool isNineBallWin(const ShotResult& result, const Table& table) const`                                                                                                             Memeriksa kemenangan
                                                                                                                                                                                       9-Ball yang sah.

  `bool requiresBallInHand(const RuleOutcome& outcome) const`                                                                                                                          Memeriksa apakah
                                                                                                                                                                                       hasil memberi hak
                                                                                                                                                                                       ball-in-hand.
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

`RuleOutcome` membawa hasil evaluasi; `MatchSession` menerapkannya pada
pemain, giliran, fase, penempatan ulang bola, dan akhir pertandingan.

### 5.13 `StorageManager`

**Batas:** baca/tulis data lokal. Tidak mengatur UI atau aturan
permainan.

  ---------------------------------------------------------------------------------
  Method                                                Kontrak
  ----------------------------------------------------- ---------------------------
  `bool loadSettings(AppSettings& settings)`            Membaca pengaturan; jika
                                                        file tidak ada/rusak,
                                                        mengisi default.

  `bool saveSettings(const AppSettings& settings)`      Menulis pengaturan ke TXT.

  `bool saveMatchRecord(const MatchRecord& record)`     Menambahkan hasil
                                                        pertandingan selesai ke
                                                        riwayat.

  `std::vector<MatchRecord> loadMatchHistory() const`   Membaca record riwayat yang
                                                        valid.

  `bool deleteMatchRecord(int recordId)`                Opsional; hanya dibuat jika
                                                        fitur hapus satu record
                                                        disediakan di UI.

  `bool clearMatchHistory()`                            Opsional; hanya dibuat jika
                                                        fitur hapus semua riwayat
                                                        disediakan dan
                                                        dikonfirmasi.
  ---------------------------------------------------------------------------------

Format TXT harus konsisten. File tidak tersedia/rusak tidak boleh
membuat aplikasi langsung crash.

### 5.14 `AudioManager`

**Batas:** pemutaran dan volume audio. Tidak menentukan kapan kejadian
permainan berlangsung.

  --------------------------------------------------------------------------------
  Method                                              Kontrak
  --------------------------------------------------- ----------------------------
  `bool initialize()`                                 Memuat resource audio.

  `void playMusic()` / `void stopMusic()`             Memulai/menghentikan musik.

  `void setMusicVolume(float volume)`                 Mengatur volume musik.

  `void setSfxVolume(float volume)`                   Mengatur volume efek suara.

  `void playSfx(SoundType sound)`                     Memutar efek suara yang
                                                      diminta.

  `void applySettings(const AppSettings& settings)`   Menerapkan volume dari
                                                      pengaturan.
  --------------------------------------------------------------------------------

### 5.15 Kontrak struct

``` cpp
struct MatchConfig {
    GameType gameType;
    OpponentType opponentType;
    std::string player1Name;
    std::string player2Name;
    int turnTimeLimitSeconds; // 0 = tanpa batas
};

struct AppSettings {
    float musicVolume;
    float sfxVolume;
    float mouseSensitivity;
    DisplayMode displayMode;
    unsigned int windowWidth;
    unsigned int windowHeight;
};

struct MatchRecord {
    int recordId;
    std::string dateTime;
    GameType gameType;
    OpponentType opponentType;
    std::string player1Name;
    std::string player2Name;
    std::string winnerName;
    int player1PocketedCount;
    int player2PocketedCount;
    int player1FoulCount;
    int player2FoulCount;
    int durationSeconds;
};

struct PocketData {
    sf::Vector2f position;
    float radius;
};

struct ShotCommand {
    sf::Vector2f aimDirection;
    float power;
};

struct ShotStartState {
    int shooterIndex;
    BallGroup shooterGroup;
    int lowestActiveBallAtStart;
    bool tableOpen;
    bool shooterGroupClearedAtStart;
};

struct ShotResult {
    int firstBallHit;
    std::vector<int> pocketedBalls;
    bool cueBallPocketed;
    bool anyBallHitCushionAfterContact;
    bool eightBallPocketed;
    bool nineBallPocketed;
};

struct RuleOutcome {
    bool isFoul;
    FoulType foulType;
    bool retainTurn;
    bool ballInHand;
    bool matchFinished;
    int winnerIndex; // -1 jika belum ada pemenang
    BallGroup assignedGroup; // NONE jika belum ditetapkan
    int groupOwnerIndex; // -1 jika tidak ada penetapan
    std::vector<int> ballsToRespot;
};
```

Field dapat ditambah hanya bila dibutuhkan oleh alur yang disepakati.
`ShotResult` menyimpan fakta, bukan kesimpulan; `RuleOutcome` menyimpan
kesimpulan aturan, bukan fakta mentah.

## 6. Relasi dan alur kolaborasi

### 6.1 Relasi

-   `GameApp` menginisialisasi dan mengoordinasikan `ScreenManager`,
    `StorageManager`, dan `AudioManager`.
-   `ScreenManager` menampilkan halaman dan menghubungkan UI ke
    `MatchSession`.
-   `MatchSession` menggunakan `Table`, `Cue`, `PhysicsEngine`,
    `GameRules`, `Player`, dan controller.
-   `HumanController` dan `BotController` merupakan turunan
    `PlayerController`.
-   `HumanController` memperbarui `Cue`; `BotController` membaca `Table`
    dan `Player`.
-   `Table` menyimpan `Ball` dan `PocketData`.
-   `PhysicsEngine` mengubah keadaan bola melalui `Table`.
-   `GameRules` membaca snapshot, hasil fisika, meja, dan pemain lalu
    menghasilkan `RuleOutcome`.
-   `StorageManager` mengelola `AppSettings` dan `MatchRecord`.
-   `AudioManager` dipanggil oleh komponen yang mengetahui kejadian yang
    harus diberi suara.

### 6.2 Alur aplikasi

1.  `GameApp::initialize()` meminta `StorageManager` memuat pengaturan.
2.  Window dibuat sesuai mode tampilan; audio dan halaman awal
    disiapkan.
3.  `GameApp::run()` menjalankan event, update, dan render.
4.  Event UI diteruskan ke `ScreenManager`; event permainan diteruskan
    ke controller melalui halaman permainan.
5.  `ScreenManager` menampilkan halaman aktif.

### 6.3 Alur satu pukulan

1.  Controller menghasilkan `ShotCommand`.
2.  `MatchSession` menyimpan `ShotStartState`.
3.  `Cue` menghitung impuls dari arah dan power.
4.  `PhysicsEngine` menjalankan simulasi dan mengumpulkan `ShotResult`.
5.  Saat semua bola berhenti, `MatchSession` meminta
    `GameRules::evaluateShot`.
6.  `GameRules` mengembalikan `RuleOutcome`.
7.  `MatchSession` memperbarui statistik/pemain, giliran, timer,
    ball-in-hand, respot, atau status selesai.
8.  Jika selesai, `MatchSession` membentuk `MatchRecord` dan meminta
    `StorageManager` menyimpan.

### 6.4 Alur ball-in-hand

`GameRules` mengembalikan `ballInHand = true` → `MatchSession` masuk
`BALL_IN_HAND` → pemain memilih posisi → `Table::canPlaceCueBall`
memvalidasi → jika valid `MatchSession` menerapkan posisi, jika tidak
pemain tetap pada tahap penempatan.

### 6.5 Alur mode tampilan

Pengguna memilih mode → nilai `AppSettings` diperbarui →
`GameApp::applyDisplaySettings` mengubah window → viewport 16:9 dihitung
→ `ScreenManager::setViewport` memperbarui layout → input mouse
dipetakan ke koordinat logis → `StorageManager` menyimpan pengaturan.

## 7. Skenario penggunaan

### 7.1 Skenario utama: Menggunakan YouKnowBall dan memainkan pertandingan hingga selesai

**Aktor:** Pemain. **Aktor pendukung:** Bot Easy jika dipilih.\
**Tujuan:** Mengatur pertandingan, bermain, melihat hasil, dan menyimpan
hasil ke riwayat.

**Prasyarat:** Aplikasi berjalan dan menu utama tampil.

**Alur utama:** 1. Pemain memilih Main. 2. Sistem menampilkan pengaturan
pertandingan. 3. Pemain memilih 8-Ball atau 9-Ball. 4. Pemain memilih
Pemain Lokal atau Bot Easy. 5. Pemain mengisi nama pemain sesuai mode.
6. Pemain memilih tanpa batas, 15, 30, atau 60 detik. 7. Pemain menekan
Mulai. 8. Sistem menyiapkan meja, bola, pemain, controller, timer, dan
aturan. 9. Sistem menampilkan halaman permainan. 10. Pemain mengarahkan
cue dengan mouse. 11. Pemain mengatur power dengan indikator terpisah.
12. Pemain dapat menekan Space untuk membatalkan pengaturan power. 13.
Pemain melepas mouse untuk menjalankan pukulan. 14. Sistem menjalankan
simulasi sampai seluruh bola berhenti. 15. Sistem mengevaluasi pukulan
sesuai aturan permainan. 16. Jika foul, sistem memberikan giliran kepada
lawan dan ball-in-hand sesuai hasil aturan. 17. Jika belum selesai,
sistem menyiapkan giliran berikutnya. 18. Jika melawan bot, Bot Easy
memilih pukulan dan mengirim `ShotCommand` melalui alur yang sama. 19.
Giliran bergantian sampai kondisi akhir tercapai. 20. Sistem menampilkan
pemenang, nama pemain, jenis permainan, bola masuk, foul, dan durasi.
21. Sistem menyimpan hasil pertandingan ke riwayat TXT. 22. Pemain dapat
kembali ke menu atau bermain lagi dengan konfigurasi sebelumnya.

**Alur alternatif:** - Timeout saat tidak mengatur power: giliran
berpindah tanpa foul dan tanpa ball-in-hand. - Timeout saat mengatur
power: pukulan dijalankan dengan power saat itu. - Pause: timer berhenti
dan input yang belum dikirim dibatalkan; resume melanjutkan sisa
waktu. - Ball-in-hand: cue ball hanya dapat diletakkan di posisi
valid. - Dua kelompok masuk bersamaan pada 8-Ball ketika meja terbuka:
kelompok tetap belum ditentukan. - Bola 8 masuk sebelum kelompok sendiri
habis: pemain yang memukul kalah. - Bola 8 masuk bersama scratch/foul:
pemain yang memukul kalah. - Bola 8 masuk saat break: bola 8
dikembalikan ke meja dan permainan dilanjutkan. - Bola 9 masuk secara
sah: pemain yang memukul menang. - Bola 9 masuk saat break: bola 9
dikembalikan ke meja dan permainan dilanjutkan. - Bola 9 masuk bersama
foul: tidak menang; bola 9 dikembalikan dan foul diproses. -
Restart/batal: pertandingan aktif tidak disimpan sebagai hasil
selesai. - Window di-resize: konten tetap 16:9 dan koordinat mouse tetap
tepat. - File TXT tidak tersedia/rusak: gunakan default atau riwayat
kosong tanpa crash.

### 7.2 Melihat riwayat

1.  Pemain memilih Riwayat.
2.  Sistem membaca data melalui `StorageManager`.
3.  Sistem menampilkan daftar pertandingan selesai.
4.  Pemain memilih satu record.
5.  Sistem menampilkan detail pemain, jenis permainan, pemenang, bola
    masuk, foul, dan durasi.
6.  Pemain kembali ke daftar atau menu.

### 7.3 Mengubah pengaturan

1.  Pemain membuka Pengaturan.
2.  Sistem menampilkan nilai saat ini.
3.  Pemain mengubah volume musik/SFX, sensitivitas mouse, atau mode
    tampilan.
4.  Sistem menerapkan perubahan.
5.  `StorageManager` menyimpan pengaturan.
6.  Pemain kembali ke menu.

### 7.4 Cara bermain

1.  Pemain membuka Cara Bermain.
2.  Sistem menjelaskan arah, power, pembatalan power, dan pause.
3.  Sistem menjelaskan aturan dasar 8-Ball/9-Ball.
4.  Sistem menjelaskan foul, scratch, dan ball-in-hand.
5.  Pemain kembali ke menu.

### 7.5 Keluar aplikasi

1.  Pemain memilih Keluar.
2.  Sistem menampilkan konfirmasi.
3.  Jika batal, sistem kembali ke halaman sebelumnya.
4.  Jika Ya, aplikasi menutup dan menyimpan pengaturan terakhir.

## 8. Rancangan halaman minimum

  ---------------------------------------------------------------------
  Halaman                            Informasi/komponen
  ---------------------------------- ----------------------------------
  Menu Utama                         Judul/logo, Main, Riwayat,
                                     Pengaturan, Cara Bermain, Keluar

  Pengaturan Pertandingan            8-/9-Ball, Pemain Lokal/Bot Easy,
                                     nama, timer, Mulai/Kembali

  Permainan                          Meja, pocket, bola, cue, prediksi,
                                     power, nama, giliran, target,
                                     timer, pause

  Pause                              Lanjutkan, Restart, Menu dengan
                                     konfirmasi

  Hasil                              Pemenang, pemain, jenis permainan,
                                     bola masuk, foul, durasi, Main
                                     Lagi/Menu

  Riwayat                            Daftar record selesai

  Detail Riwayat                     Rincian satu pertandingan

  Pengaturan                         Musik, SFX, sensitivitas,
                                     Windowed/Fullscreen

  Cara Bermain                       Kontrol, aturan, foul, scratch,
                                     ball-in-hand

  Konfirmasi Keluar                  Ya/Kembali
  ---------------------------------------------------------------------

Prioritas tampilan adalah keterbacaan dan fungsi. Dekorasi/animasi tidak
boleh menghambat penyelesaian mekanik inti.

## 9. Pembagian pekerjaan

**Anggota:** Rapid Akbar Sinatria, Muhammad Argo Iman, Satya Firma
Ashari.

PIC adalah penanggung jawab koordinasi dan memastikan hasil area kerja
selesai. PIC bukan satu-satunya orang yang boleh mengerjakan bagian
tersebut; anggota lain dapat membantu coding, pengujian, debugging, dan
integrasi dengan koordinasi.

  -----------------------------------------------------------------------
  Area                    PIC                     Kolaborasi
  ----------------------- ----------------------- -----------------------
  Antarmuka, layout,      Rapid Akbar Sinatria    Satya menghubungkan
  halaman, navigasi, HUD,                         data permainan; Argo
  konsistensi visual                              menghubungkan status
  (`ScreenManager`)                               aturan/hasil ke UI

  Window SFML, loop       Rapid Akbar Sinatria    Satya membantu uji
  aplikasi,                                       SFML; Argo membantu
  Windowed/Fullscreen,                            integrasi pengaturan
  viewport (`GameApp`)                            

  Bola, meja, pocket,     Satya Firma Ashari      Rapid membantu
  geometri (`Ball`,                               kebutuhan visual; Argo
  `Table`, `PocketData`)                          membantu uji validasi
                                                  posisi

  Gerak, gesekan,         Satya Firma Ashari      Argo menguji dampak ke
  tumbukan, cushion,                              aturan; Rapid membantu
  pocket                                          visualisasi/debug
  (`PhysicsEngine`)                               

  Cue, input manusia,     Satya Firma Ashari      Rapid membantu
  arah/power, prediksi                            interaksi/indikator;
  (`Cue`,                                         Argo memeriksa alur
  `HumanController`)                              pukulan

  Data pemain dan         Muhammad Argo Iman      Rapid menghubungkan
  konfigurasi (`Player`,                          form; Satya integrasi
  `MatchConfig`,                                  controller
  `AppSettings`)                                  

  Aturan 8-/9-Ball, foul, Muhammad Argo Iman      Satya menyediakan fakta
  ball-in-hand                                    fisika; Rapid
  (`GameRules`,                                   menampilkan status
  `RuleOutcome`)                                  

  Siklus pertandingan,    Muhammad Argo Iman      Satya integrasi
  giliran, timer, pause,                          fisika/controller;
  hasil (`MatchSession`)                          Rapid integrasi halaman

  Bot Easy                Satya Firma Ashari      Argo memvalidasi
  (`BotController`)                               keputusan; Rapid
                                                  menampilkan status bot

  TXT pengaturan/riwayat  Muhammad Argo Iman      Rapid menghubungkan
  (`StorageManager`,                              halaman; Satya menguji
  `MatchRecord`)                                  data hasil

  Musik dan efek suara    Rapid Akbar Sinatria    Satya membantu pemicu
  (`AudioManager`)                                dari fisika; Argo
                                                  menghubungkan
                                                  volume/pengaturan

  Pengujian integrasi dan Ketiganya               Semua anggota menguji
  perbaikan lintas modul                          modul di luar bagiannya

  Laporan akhir dan       Ketiganya               Argo mengoordinasikan
  persiapan demo                                  konsistensi dokumen;
                                                  PIC melengkapi
                                                  dokumentasi area
  -----------------------------------------------------------------------

## 10. WBS dan jadwal

**Semua pekerjaan, termasuk laporan akhir, harus selesai paling lambat
13 Desember 2026.**

  -------------------------------------------------------------------------
  Minggu/tanggal   Kegiatan           Target keluaran  PIC
  ---------------- ------------------ ---------------- --------------------
  Minggu 9 --- 26  Finalisasi         Dasar kebutuhan  Argo
  Okt--1 Nov       kebutuhan, scope,  dan rancangan    
                   skenario, use      awal             
                   case,                               
                   class/struct,                       
                   pembagian awal                      

  Minggu 10 ---    Finalisasi relasi  Acuan desain     Argo
  5--8 Nov         class, kontrak     siap             
                   method, struktur   implementasi     
                   proyek                              

  Minggu 11 ---    Ball, Table,       Meja dan         Satya
  9--15 Nov        pocket, geometri,  simulasi dasar   
                   gerak dasar,       dapat diuji      
                   gesekan, tumbukan,                  
                   cushion, pocket                     
                   detection                           

  Minggu 12 ---    Cue,               Input pukulan    Satya
  16--22 Nov       HumanController,   dan evaluasi     (Cue/controller),
                   ShotCommand,       aturan awal      Argo (aturan)
                   aturan dasar dan                    
                   hasil pukulan                       

  Minggu 13 ---    MatchSession,      Siklus           Argo
  23--29 Nov       giliran, timer,    pertandingan     
                   pause/resume,      berjalan         
                   foul,                               
                   ball-in-hand,                       
                   hasil                               

  Minggu 14 --- 30 Bot Easy,          Fitur pendukung  Rapid
  Nov--6 Des       halaman/HUD, mode  terintegrasi     (UI/window/audio),
                   tampilan,                           Satya (bot), Argo
                   StorageManager,                     (storage)
                   riwayat,                            
                   AudioManager, cara                  
                   bermain                             

  Minggu 15 ---    Integrasi final,   Build dan        Ketiganya
  7--13 Des        uji skenario,      laporan final    
                   perbaikan bug,     selesai          
                   laporan akhir,                      
                   pemeriksaan, demo                   
  -------------------------------------------------------------------------

### 10.1 Rincian target

**Minggu 11 (9--15 November)** - Menetapkan ukuran meja, radius bola,
posisi pocket, batas area. - Membuat `Ball` dan `Table`, serta susunan
awal 8-/9-Ball. - Membuat gerak, gesekan, ambang berhenti, tumbukan,
cushion, pocket. - Menguji bola tunggal, tumbukan dua bola, pantulan,
dan pocket.

**Minggu 12 (16--22 November)** - Membuat arah cue, power, input mouse,
indikator power terpisah. - Mengimplementasikan Space untuk membatalkan
power. - Menghasilkan `ShotCommand`, snapshot awal, dan hasil fisika. -
Mengimplementasikan evaluasi aturan dasar. - Menguji dua jenis timeout.

**Minggu 13 (23--29 November)** - Mengintegrasikan controller, cue,
fisika, dan aturan melalui `MatchSession`. - Membuat giliran, timer,
pause/resume, foul, scratch, ball-in-hand. - Mengimplementasikan kondisi
akhir 8-/9-Ball. - Menguji kondisi khusus break, dua kelompok masuk
bersamaan, dan bola 8/9 bersama foul.

**Minggu 14 (30 November--6 Desember)** - Menyelesaikan seluruh halaman
yang masuk scope dan menghubungkan HUD. - Mengimplementasikan Bot Easy
melalui `ShotCommand`. - Mengimplementasikan Windowed/Fullscreen 16:9. -
Menyimpan/membaca pengaturan dan riwayat TXT. - Mengintegrasikan
musik/SFX dan menguji navigasi.

**Minggu 15 (7--13 Desember)** - Mengintegrasikan seluruh modul ke build
final. - Menjalankan pengujian utama dan alternatif. - Memperbaiki bug
crash, mekanik, aturan, dan integrasi. - Memeriksa source, aset, dan
struktur folder. - Menyelesaikan laporan, diagram, kontrak method, WBS,
dan hasil pengujian. - Pemeriksaan akhir oleh semua anggota. - Tidak
menjadwalkan pekerjaan wajib setelah 13 Desember 2026.

## 11. Pengujian minimum

  -----------------------------------------------------------------------
  ID                      Skenario                Hasil yang diharapkan
  ----------------------- ----------------------- -----------------------
  T01                     Membuka aplikasi dengan Menu tampil tanpa error
                          pengaturan default      

  T02                     Memulai 8-Ball Pemain   Susunan 8-Ball tampil
                          Lokal                   

  T03                     Memulai 9-Ball Bot Easy Susunan 9-Ball tampil

  T04                     Menggerakkan mouse      Arah cue berubah sesuai
                          untuk membidik          input

  T05                     Mengatur power          Power berubah, arah
                                                  tetap terkunci

  T06                     Menekan Space saat      Power dibatalkan, belum
                          mengatur power          ada tembakan

  T07                     Melepas mouse normal    Satu pukulan dijalankan

  T08                     Pause saat drag belum   Input dibatalkan, tidak
                          selesai                 ada tembakan tak
                                                  sengaja

  T09                     Timeout tanpa mengatur  Giliran pindah tanpa
                          power                   foul/ball-in-hand

  T10                     Timeout saat mengatur   Pukulan dijalankan pada
                          power                   power saat itu

  T11                     Semua bola berhenti     Simulasi berakhir

  T12                     Cue ball masuk pocket   Scratch/foul tercatat

  T13                     Terjadi foul            Lawan mendapat giliran
                                                  dan ball-in-hand

  T14                     Penempatan cue ball     Posisi ditolak
                          tidak valid             

  T15                     Solid dan stripe masuk  Kelompok belum
                          bersamaan saat meja     ditetapkan
                          terbuka                 

  T16                     Bola 8 masuk sebelum    Pemain yang memukul
                          kelompok sendiri habis  kalah

  T17                     Bola 8 masuk bersama    Pemain yang memukul
                          scratch                 kalah

  T18                     Bola 8 masuk saat break Bola 8 di-spot kembali

  T19                     Bola 9 masuk sah        Pemain yang memukul
                                                  menang

  T20                     Bola 9 masuk saat break Bola 9 di-spot kembali

  T21                     Bola 9 masuk bersama    Tidak menang; foul
                          foul                    diproses, bola 9
                                                  di-spot

  T22                     Bot mendapat giliran    Bot mengirim satu
                                                  perintah lewat alur
                                                  normal

  T23                     Pertandingan selesai    Halaman hasil
                                                  menampilkan data benar

  T24                     Membuka riwayat setelah Record muncul
                          pertandingan            

  T25                     Mengubah                Nilai diterapkan dan
                          audio/sensitivitas      tersimpan

  T26                     Resize Windowed         Rasio tetap 16:9, mouse
                                                  tetap akurat

  T27                     Fullscreen pada layar   Letterbox/pillarbox,
                          non-16:9                tidak meregang

  T28                     File TXT tidak          Default/riwayat kosong,
                          tersedia/rusak          tidak crash

  T29                     Restart/batal           Tidak disimpan sebagai
                          pertandingan            hasil selesai

  T30                     Keluar melalui          Aplikasi hanya tertutup
                          konfirmasi              setelah Ya
  -----------------------------------------------------------------------

### Prioritas jika waktu terbatas

1.  Aplikasi berjalan tanpa crash.
2.  Pukulan, gerak, tumbukan, dan pocket bekerja.
3.  Aturan inti dan pemenang benar.
4.  Giliran, timer, pause, ball-in-hand benar.
5.  Bot Easy berfungsi melalui alur yang sama.
6.  Navigasi dan halaman utama dapat digunakan.
7.  Riwayat dan pengaturan tersimpan.
8.  Audio, dekorasi, animasi, dan penyempurnaan visual.

## 12. Risiko dan mitigasi

  ---------------------------------------------------------------------
  Risiko                             Mitigasi
  ---------------------------------- ----------------------------------
  Fisika tidak stabil                Uji per kasus, kendalikan delta
                                     time, tetapkan ambang berhenti

  Method tumpang tindih              Ikuti batas: PhysicsEngine=fakta,
                                     GameRules=keputusan,
                                     MatchSession=orkestrasi

  Input salah setelah resize         Gunakan viewport dan koordinat
                                     logis

  Bot terlalu kompleks               Batasi strategi pada target, arah,
                                     dan power sederhana

  TXT gagal dibaca                   Tetapkan format awal dan uji
                                     baca/tulis; sediakan fallback

  Integrasi terlambat                Integrasi bertahap tiap minggu dan
                                     kontrak antarmodul disepakati

  Dekorasi menyita waktu             Dahulukan mekanik dan aturan inti
  ---------------------------------------------------------------------

## 13. Kriteria selesai

Proyek siap diserahkan jika: - Aplikasi berjalan pada lingkungan yang
disepakati. - 8-Ball dan 9-Ball dapat dimulai. - Pemain Lokal dan Bot
Easy dapat dimainkan. - Kontrol arah/power sesuai ketentuan. - Simulasi
bola dan pocket berjalan. - Aturan inti, foul, scratch, giliran,
ball-in-hand, timeout, pause/resume bekerja. - Hasil pertandingan
ditampilkan dan disimpan ke TXT. - Pengaturan dapat disimpan dan
dimuat. - Windowed/Fullscreen mempertahankan 16:9 dan input tetap
akurat. - Halaman dan navigasi dalam scope dapat digunakan. - Pengujian
minimum dicatat. - Laporan akhir dan seluruh dokumentasi selesai paling
lambat **13 Desember 2026**.

## 14. Nilai teknis yang ditetapkan saat implementasi

Nilai yang perlu ditentukan melalui uji coba, bukan ditebak dalam
dokumen: - Ukuran logis meja dan posisi bola awal. - Radius bola dan
pocket. - Massa, gesekan, kekuatan cushion, dan power
minimum/maksimum. - Ambang kecepatan untuk menyatakan bola berhenti. -
Ukuran minimum window 16:9. - Format TXT dan perilaku ketika file
rusak. - Spot untuk bola 8/9 yang dikembalikan. - Daftar foul rinci yang
benar-benar akan dibuat.

Catat nilai tersebut dalam konstanta/konfigurasi internal. Jangan
menjadikannya semua sebagai pengaturan pengguna tanpa kebutuhan.

## 15. Konsistensi dokumen lanjutan

Gunakan secara konsisten: - Nama: **YouKnowBall**. - Teknologi: **C++
dan SFML**. - Permainan: **8-Ball dan 9-Ball**. - Lawan: **Pemain Lokal
dan Bot Easy**. - Rancangan: **14 class dan 8 struct**. - Tampilan:
**Windowed/Fullscreen, rasio 16:9**. - Penyimpanan: **TXT lokal**. -
Batas akhir: **13 Desember 2026**. - PIC adalah penanggung jawab
koordinasi/penyelesaian area, bukan satu-satunya pelaksana. - `GameApp`
mengelola window/loop; `ScreenManager` mengelola halaman. -
`PhysicsEngine` menghasilkan fakta; `GameRules` mengevaluasi;
`MatchSession` menerapkan hasil dan mengelola siklus. - Bot dan manusia
memakai `ShotCommand` dan alur permainan yang sama.

**Dokumen v03 ini menjadi acuan utama terbaru.** Jika berbeda dengan
catatan rancangan lama, gunakan keputusan v03 kecuali tim/dosen
menyepakati revisi berikutnya.

------------------------------------------------------------------------

# Bagian C --- Aturan Pemeliharaan Dokumen

1.  Seluruh anggota menggunakan v04 sebagai satu acuan kerja bersama.
2.  Penambahan fitur, class, struct, mode, atau aturan tidak boleh
    dilakukan sepihak.
3.  Baseline arsitektur tetap 14 class utama dan 8 struct pendukung.
4.  Perubahan harus ditelusuri dampaknya pada class diagram, sequence
    diagram, use case, WBS, pembagian tugas, implementasi, dan
    pengujian.
5.  PIC adalah penanggung jawab utama koordinasi dan penyelesaian area,
    bukan satu-satunya anggota yang boleh mengerjakan.
6.  Bedakan keputusan final, nilai teknis yang harus ditentukan melalui
    pengujian, dan hal yang masih terbuka.
7.  Setiap revisi mencatat versi, tanggal, perubahan, alasan, dan
    artefak yang terdampak.

## Riwayat Finalisasi v04

-   Mempertahankan keseluruhan 24 bagian MD v02.
-   Menyertakan keseluruhan 15 bagian MD v03 sebagai penyelarasan
    terbaru.
-   Menetapkan urutan prioritas jika ditemukan perbedaan.
-   Menjadikan v04 acuan bersama untuk implementasi, diagram, pengujian,
    dan laporan akhir.

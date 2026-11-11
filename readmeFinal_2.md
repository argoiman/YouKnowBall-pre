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

/*
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
*/

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
| Pemain | Pengguna yang menjalankan aplikasi, mengatur pertandingan, memainkan permainan, dan mengakses fitur aplikasi. Dalam Local Multiplayer, peran pemain dijalankan oleh Player 1 dan Player 2 secara bergantian pada satu perangkat. |

Bot Easy bukan aktor eksternal karena merupakan perilaku otomatis di dalam sistem. Bot tetap dijelaskan pada alur penggunaan ketika mode Human vs Bot dipilih.

Pada mode Local Multiplayer, Player 1 dan Player 2 bermain secara bergantian menggunakan perangkat yang sama. Pada mode Human vs Bot, pengguna bermain melawan Bot Easy yang mengambil keputusan pukulan secara otomatis berdasarkan kondisi permainan dan strategi sederhana.

### 18.2 Identitas Skenario

| Elemen | Keterangan |
|---|---|
| Nama Skenario | Menggunakan YouKnowBall dan Memainkan Pertandingan hingga Selesai |
| Goal | Pemain dapat mengatur dan memainkan pertandingan 8-Ball atau 9-Ball, melihat hasil dan riwayat, mengatur aplikasi, membaca panduan, serta mengakhiri penggunaan aplikasi. |
| Level | User-Goal |
| Primary Actor | Pemain |
| Supporting Actor | Tidak ada. Bot Easy merupakan perilaku internal sistem, bukan aktor eksternal. |
| Trigger | Pemain menjalankan aplikasi YouKnowBall. |
| Precondition | Aplikasi telah terpasang dan dapat dijalankan. |
| Kondisi Akhir Sukses | Pertandingan selesai, hasil ditampilkan dan disimpan, serta pemain dapat melanjutkan ke menu lain atau keluar. |
| Kondisi Akhir Alternatif | Jika pertandingan dibatalkan sebelum selesai, pertandingan tidak disimpan sebagai hasil pertandingan. |

### 18.3 Narasi Skenario Penggunaan

Ketika aplikasi YouKnowBall dijalankan, sistem menampilkan halaman Main Menu sebagai halaman utama. Pada halaman ini, pengguna dapat memilih permainan 8-Ball melalui tombol **Main 8-Ball** atau permainan 9-Ball melalui tombol **Main 9-Ball**. Kedua tombol tersebut tersedia secara langsung pada Main Menu sehingga pengguna tidak perlu memilih mode permainan melalui tombol Start Match terlebih dahulu.

Selain pilihan permainan, Main Menu menyediakan akses menuju Match History, Application Settings, How to Play, dan Exit.

Jika pengguna memilih Main 8-Ball atau Main 9-Ball, sistem menampilkan halaman pengaturan pertandingan. Pada halaman tersebut, pengguna dapat menentukan jenis lawan yang akan dihadapi, yaitu Local Multiplayer atau Human vs Bot. Pengguna juga dapat mengisi nama pemain dan menentukan batas waktu setiap giliran. Pilihan waktu yang tersedia adalah Unlimited, 15 Seconds, 30 Seconds, dan 60 Seconds.

Setelah pengaturan pertandingan selesai, pengguna memulai pertandingan. Sistem menyiapkan meja, susunan bola, pemain, dan giliran awal, kemudian menampilkan halaman permainan.

Pada saat giliran pemain aktif, pemain dapat mengarahkan cue stick untuk menentukan arah tembakan. Setelah arah ditentukan, pemain mengatur kekuatan tembakan melalui indikator power yang terpisah dari cue stick pada area meja. Indikator ini hanya mengatur kekuatan, bukan arah; bentuk visualnya boleh menyerupai cue stick, sedangkan bentuk dan posisi akhirnya ditentukan saat implementasi.

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
5. Pemain mengatur kekuatan tembakan melalui indikator power yang terpisah dari cue stick pada area meja; bentuk dan posisi indikator ditentukan saat implementasi.
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

### 18.6 Postcondition

- Jika pertandingan selesai secara normal, sistem menampilkan hasil dan menyimpan satu catatan pertandingan ke Match History.
- Jika pertandingan dibatalkan melalui Restart atau Main Menu sebelum selesai, sistem tidak menyimpan pertandingan tersebut sebagai hasil selesai.
- Pengaturan yang telah diterapkan melalui Apply/Save tersimpan dan dimuat kembali ketika aplikasi dijalankan pada sesi berikutnya.
- Pemain dapat kembali ke Main Menu, memulai pertandingan baru, membuka riwayat, mengubah pengaturan, membaca panduan, atau menutup aplikasi.

**Catatan metodologis:** bagian ini sengaja menyajikan satu skenario penggunaan menyeluruh sesuai kebutuhan dokumentasi kelompok. Narasi dan urutan langkah tetap berfokus pada interaksi aktor dengan sistem serta respons fungsionalnya; nama class, method, dan mekanisme internal tidak digunakan sebagai isi skenario. Dalam pemodelan UML yang lebih terperinci, tujuan seperti melihat riwayat atau mengubah pengaturan dapat dipisahkan menjadi use case tersendiri.

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
3. Memfinalisasi kontrak seluruh method pada 14 class, termasuk method publik, method override, accessor, dan operasi internal yang menjadi bagian antarmuka antarmodul.
4. Menyepakati aliran data antarmodul.
5. Menyiapkan struktur folder dan file proyek.
6. Memastikan kebutuhan implementasi sesuai dengan rancangan.

**Target akhir Minggu 10:**

- Wireframe selesai dan telah dipresentasikan.
- Relasi class dan tanggung jawab disepakati.
- Kontrak seluruh method baseline 14 class tersedia dan batas tanggung jawab antarmodul telah diperiksa.
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
4. Membuat indikator power yang terpisah dari cue stick pada meja dan dari kontrol arah; bentuk serta posisi visual ditentukan saat implementasi.
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

README ini menjadi acuan mandiri proyek YouKnowBall. Dokumen mencakup identitas dan ruang lingkup produk, rancangan halaman, konfigurasi, kontrol, timer, aturan 8-Ball/9-Ball, prediksi lintasan, Bot Easy, hasil dan penyimpanan, arsitektur 14 class dan 8 struct, seluruh kontrak method baseline, relasi antarkomponen, skenario penggunaan, pembagian peran, WBS minggu 9–15, ketentuan integrasi, pengujian, risiko, kriteria penyelesaian, serta keputusan yang masih perlu ditentukan saat implementasi.

Perubahan dan penegasan yang menjadi acuan:

- Menggunakan C++ dan SFML 2.4.2 untuk platform PC/Desktop.
- Main Menu menyediakan tombol langsung Main 8-Ball dan Main 9-Ball.
- Mode lawan adalah Local Multiplayer atau Human vs Bot Easy.
- Pilihan timer adalah Unlimited, 15, 30, dan 60 detik.
- Cue stick pada meja mengatur arah; indikator power terpisah hanya mengatur kekuatan. Bentuk dan posisi indikator power ditentukan saat implementasi.
- Space membatalkan pengaturan power sebelum mouse dilepas; pemain kemudian dapat mengatur arah kembali.
- Timeout saat power sedang ditarik langsung menjalankan pukulan dengan power saat itu; timeout di luar kondisi tersebut langsung memindahkan giliran tanpa foul dan tanpa ball-in-hand.
- Pause menyediakan Continue, Settings, Restart, dan Main Menu. Settings memiliki Apply/Save dan Back.
- Rematch langsung memulai pertandingan baru dengan konfigurasi sebelumnya; perubahan konfigurasi dilakukan melalui Main Menu.
- Windowed dan Fullscreen menggunakan konten logis 16:9 tanpa distorsi.
- Penyimpanan lokal menggunakan file TXT untuk pengaturan dan hasil pertandingan selesai.
- Arsitektur mempertahankan tepat 14 class utama dan 8 struct pendukung.
- Target seluruh implementasi, pengujian, dokumentasi, dan laporan akhir adalah 13 Desember 2026.

---

**Acuan utama proyek YouKnowBall — Kelompok 9.**

Gunakan dokumen ini sebagai referensi bersama selama pengembangan. Jika terdapat keputusan baru yang disepakati, perbarui bagian terkait dan riwayat perubahan agar seluruh anggota menggunakan acuan versi yang sama.

## Dokumentasi untuk CIDRAM v3 (Bahasa Indonesia).

### Isi
- 1. [SEPATAH KATA](#user-content-SECTION1)
- 2. [BAGAIMANA CARA MENGINSTAL](#user-content-SECTION2)
- 3. [BAGAIMANA CARA MENGGUNAKAN](#user-content-SECTION3)
- 4. [MANAJEMEN BAGIAN DEPAN](#user-content-SECTION4)
- 5. [OPSI KONFIGURASI](#user-content-SECTION5)
- 6. [FORMAT TANDA TANGAN](#user-content-SECTION6)
- 7. [MASALAH KOMPATIBILITAS DIKETAHUI](#user-content-SECTION7)
- 8. [PERTANYAAN YANG SERING DIAJUKAN (FAQ)](#user-content-SECTION8)
- 9. [INFORMASI HUKUM](#user-content-SECTION9)
- 10. [MEMUTAKHIRKAN DARI VERSI UTAMA SEBELUMNYA](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>SEPATAH KATA

CIDRAM (Classless Inter-Domain Routing Access Manager) adalah skrip PHP dirancang untuk melindungi situs oleh memblokir permintaan yang berasal dari alamat IP yang dianggap sumber lalu lintas yang tidak diinginkan, termasuk (tapi tidak terbatas pada) lalu lintas dari jalur akses yang tidak manusia, layanan cloud, robot spam, pencakar, dll. Hal ini dilakukan melalui menghitung kisaran CIDR dari alamat IP dipasok dari permintaan dan mencoba untuk mencocokkan CIDR tersebut terhadap file tanda tangan (file tanda tangan berisi daftar CIDR dari alamat IP dianggap sumber lalu lintas yang tidak diinginkan); Jika dicocokkan, permintaan yang diblokir.

*(Lihat: [Apa yang "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) HAK CIPTA 2016 dan di atas GNU/GPLv2 oleh [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Skrip ini adalah perangkat lunak gratis; Anda dapat mendistribusikan kembali dan/atau memodifikasinya dalam batasan dari GNU General Public License, seperti di publikasikan dari Free Software Foundation; baik versi 2 dari License, atau (dalam opsi Anda) versi selanjutnya apapun. Skrip ini didistribusikan untuk harapan dapat digunakan tapi TANPA JAMINAN; tanpa walaupun garansi dari DIPERJUALBELIKAN atau KECOCOKAN UNTUK TUJUAN TERTENTU. Mohon Lihat GNU General Public Licence untuk lebih detail, terletak di file `LICENSE.txt` dan tersedia juga dari:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Dokumen ini dan paket terhubung di dalamnya dapat di unduh secara gratis dari:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

---


### 2. <a name="SECTION2"></a>BAGAIMANA CARA MENGINSTAL

#### 2.0 MENGINSTAL SECARA MANUAL

Pertama, Anda memerlukan salinan CIDRAM baru. Anda dapat mengunduh arsip yang barisi CIDRAM versi terbaru dari repositori [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM). Lebih spesifik, Anda memerlukan salinan direktori "vault" (semuanya dari arsip selain direktori "vault" dan isinya dapat dihapus atau diabaikan dengan aman).

Sebelum v3, Anda perlu menginstal CIDRAM di suatu tempat di dalam root publik Anda agar dapat mengakses front-end CIDRAM. Namun, dari v3 dan seterusnya, ini tidak perlu, dan untuk memaksimalkan keamanan dan untuk mencegah akses yang tidak diotorisasi ke CIDRAM dan filenya, disarankan untuk menginstal CIDRAM *di luar* root publik Anda. Tidak masalah persis dimana Anda memilih untuk menginstal CIDRAM, selama PHP dapat mengaksesnya, dan selama itu di suatu tempat yang cukup aman dan Anda puas dengan. Juga tidak perlu mempertahankan nama direktori "vault", jadi Anda dapat mengganti nama "vault" menjadi nama apapun yang Anda inginkan (tetapi demi kenyamanan, dokumentasi akan terus merujuknya sebagai direktori "vault").

Saat Anda siap, upload direktori "vault" ke lokasi yang Anda pilih, dan pastikan direktori tersebut memiliki izin yang diperlukan agar PHP dapat menulis ke direktori (tergantung pada sistem yang dimaksud, terkadang Anda tidak perlu melakukan apapun, atau terkadang Anda perlu menyetel CHMOD 755 ke direktori, atau jika ada masalah dengan 755, Anda dapat mencoba 777, tetapi 777 tidak disarankan karena kurang aman).

Selanjutnya, agar CIDRAM dapat melindungi basis kode atau CMS Anda, Anda harus membuat "titik masuk". Titik masuk ini terdiri dari tiga hal:

1. Menyertakan file "loader.php" pada titik yang sesuai dalam basis kode atau CMS Anda.
2. Menginstansiasi CIDRAM core.
3. Memanggil metode "protect".

Contoh sederhana:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Jika Anda menggunakan server web Apache dan memiliki akses ke `php.ini`, Anda dapat menggunakan direktif `auto_prepend_file` untuk menjalankan CIDRAM setiap kali permintaan PHP dibuat. Dalam kasus ini, tempat yang paling tepat untuk membuat titik masuk Anda adalah di filenya sendiri, dan Anda kemudian akan mengutip file ini di direktif `auto_prepend_file`.

Contoh:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

Atau ini di file `.htaccess`:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

Dalam kasus lain, tempat yang paling tepat untuk membuat titik masuk Anda adalah pada titik sedini mungkin dalam basis kode atau CMS Anda untuk selalu dimuat setiap kali seseorang mengakses halaman manapun di seluruh situs web Anda. Jika basis kode Anda menggunakan "bootstrap", contoh bagus adalah di awal file "bootstrap" Anda. Jika basis kode Anda memiliki file pusat yang bertanggung jawab untuk menghubungkan ke database Anda, contoh bagus lainnya adalah di awal file pusat ini.

#### 2.1 MENGINSTAL DENGAN COMPOSER

[CIDRAM terdaftar dengan Packagist](https://packagist.org/packages/cidram/cidram). Jika Anda akrab dengan Composer, Anda dapat menggunakan Composer untuk menginstal CIDRAM.

`composer require cidram/cidram`

#### 2.2 MENGINSTAL UNTUK WORDPRESS

[CIDRAM terdaftar sebagai plugin dengan database plugin WordPress](https://wordpress.org/plugins/cidram/), dan Anda dapat menginstal CIDRAM langsung dari plugin dashboard. Anda dapat menginstalnya dengan cara yang sama seperti plugin lainnya, dan tidak ada langkah-langkah selain diperlukan.

*Peringatan: Memperbarui CIDRAM melalui dashboard plugin menghasilkan instalasi yang bersih! Jika Anda telah menyesuaikan instalasi Anda (mengubah konfigurasi, modul terinstal, dll), kustomisasi ini akan hilang saat memperbarui melalui dashboard plugin! File log juga akan hilang saat memperbarui melalui dashboard plugin! Untuk menyimpan file log dan kustomisasi, perbarui melalui halaman pembaruan bagian depan CIDRAM.*

#### 2.3 KONFIGURASI DAN KUSTOMISASI

Sangat disarankan bagi Anda untuk meninjau konfigurasi instalasi baru Anda agar Anda dapat menyesuaikannya sesuai dengan kebutuhan Anda. Anda mungkin juga ingin menginstal modul tambahan, file tanda tangan, membuat aturan tambahan, atau menerapkan penyesuaian lain agar instalasi Anda dapat paling sesuai dengan kebutuhan Anda. Saya sarankan menggunakan front-end untuk melakukan hal-hal ini.

---


### 3. <a name="SECTION3"></a>BAGAIMANA CARA MENGGUNAKAN

CIDRAM harus secara otomatis memblokir permintaan yang tidak diinginkan ke website Anda tanpa memerlukan bantuan manual, selain dari instalasi.

Anda dapat menyesuaikan konfigurasi Anda dan menyesuaikan apa CIDRs diblokir oleh memodifikasi file konfigurasi Anda dan/atau file tanda tangan Anda.

Jika Anda menemukan positif palsu, tolong hubungi saya untuk membiarkan saya tahu tentang hal itu. *(Lihat: [Apa yang dimaksud dengan "positif palsu"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM dapat diperbarui secara manual atau melalui bagian depan. CIDRAM juga bisa diperbarui via Composer atau WordPress, jika sudah diinstal dengan cara ini.

---


### 4. <a name="SECTION4"></a>MANAJEMEN BAGIAN DEPAN

#### 4.0 APA YANG MANAJEMEN BAGIAN DEPAN.

Manajemen bagian depan menyediakan cara yang nyaman dan mudah untuk mempertahankan, mengelola, dan memperbarui instalasi CIDRAM Anda. Anda dapat melihat, berbagi, dan download file log melalui halaman log, Anda dapat mengubah konfigurasi melalui halaman konfigurasi, Anda dapat instal dan uninstal/hapus komponen melalui halaman pembaruan, dan Anda dapat upload, download, dan memodifikasi file dalam vault Anda melalui file manager.

#### 4.1 BAGAIMANA CARA MENGAKSESKAN MANAJEMEN BAGIAN DEPAN.

Mirip dengan bagaimana Anda perlu membuat titik masuk agar CIDRAM melindungi situs web Anda, Anda juga harus membuat titik masuk untuk mengakses front-end. Titik masuk ini terdiri dari tiga hal:

1. Menyertakan file "loader.php" pada titik yang sesuai dalam basis kode atau CMS Anda.
2. Menginstansiasi CIDRAM front-end.
3. Memanggil metode "view".

Contoh sederhana:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

Kelas "FrontEnd" memperluas kelas "Core", yang berarti bahwa jika Anda mau, Anda dapat memanggil metode "protect" sebelum memanggil metode "view" untuk memblokir lalu lintas yang mungkin tidak diinginkan dari mengakses front-end. Melakukannya sepenuhnya opsional.

Contoh sederhana:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

Tempat paling tepat untuk membuat titik masuk untuk front-end adalah di file miliknya sendiri. Tidak seperti titik masuk yang Anda dibuat sebelumnya, Anda ingin titik masuk front-end Anda menjadi hanya dapat diakses melalui permintaan langsung untuk file tertentu dimana titik masuk ada, jadi dalam kasus ini, Anda tidak ingin menggunakan `auto_prepend_file` atau `.htaccess`.

Setelah membuat titik masuk front-end Anda, gunakan browser Anda untuk mengaksesnya. Anda harus disajikan dengan halaman login. Pada halaman login, masukkan nama pengguna dan kata sandi default (admin/password) dan tekan tombol login.

Catat: Setelah Anda dimasukkan untuk pertama kalinya, untuk mencegah akses tidak sah ke manajemen bagian depan, Anda harus segera mengubah nama pengguna dan kata sandi Anda! Ini sangat penting, karena itu mungkin untuk meng-upload kode PHP sewenang-wenang untuk situs web Anda melalui bagian depan.

Juga, untuk keamanan yang optimal, memungkinkan "otentikasi dua faktor" untuk semua akun bagian depan sangat disarankan (petunjuk disediakan dibawah).

#### 4.2 BAGAIMANA CARA MENGGUNAKAN MANAJEMEN BAGIAN DEPAN.

Instruksi disediakan pada setiap halaman dari manajemen bagian depan, untuk menjelaskan cara yang benar untuk menggunakannya dan tujuan yang telah ditetapkan. Jika Anda membutuhkan penjelasan lebih lanjut atau bantuan khusus, silakan hubungi dukungan, atau sebagai pilihan lain, ada beberapa video yang tersedia di YouTube yang dapat membantu dengan cara demonstrasi.

#### 4.3 OTENTIKASI DUA FAKTOR

Mungkin untuk membuat bagian depan lebih aman dengan mengaktifkan otentikasi dua faktor ("2FA"). Saat masuk ke akun berkemampuan 2FA, email dikirim ke alamat email yang terkait dengan akun tersebut. Email ini berisi "kode 2FA", yang kemudian harus dimasukkan oleh pengguna, selain nama pengguna dan kata sandi, agar dapat masuk menggunakan akun tersebut. Ini berarti bahwa mendapatkan kata sandi akun tidak akan cukup bagi peretas atau penyerang potensial untuk dapat masuk ke akun tersebut, karena mereka juga harus sudah memiliki akses ke alamat email yang terkait dengan akun tersebut agar dapat menerima dan memanfaatkan kode 2FA yang terkait dengan sesi, sehingga membuat bagian depan lebih aman.

Pertama, untuk mengaktifkan otentikasi dua faktor, menggunakan halaman pembaruan bagian depan, instal komponen PHPMailer. CIDRAM menggunakan PHPMailer untuk mengirim email.

Setelah Anda menginstal PHPMailer, Anda harus mengisi direktif konfigurasi untuk PHPMailer melalui halaman konfigurasi CIDRAM atau file konfigurasi. Informasi lebih lanjut tentang direktif konfigurasi ini termasuk dalam bagian konfigurasi dokumen ini. Setelah Anda mengisi direktif konfigurasi PHPMailer, atur `enable_two_factor` ke `true`. Otentikasi dua faktor sekarang harus diaktifkan.

Selanjutnya, Anda harus mengaitkan alamat email dengan akun, sehingga CIDRAM tahu ke mana harus mengirim 2FA kode ketika masuk dengan akun tersebut. Untuk melakukan ini, gunakan alamat email sebagai nama pengguna untuk akun tersebut (seperti `foo@bar.tld`), atau sertakan alamat email sebagai bagian dari nama pengguna dengan cara yang sama seperti ketika mengirim email secara normal (seperti `Foo Bar <foo@bar.tld>`).

Catat: Melindungi vault Anda terhadap akses yang tidak sah (misalnya, dengan memperketat keamanan server Anda dan izin akses publik), sangat penting disini, karena akses tidak sah ke file konfigurasi Anda (yang disimpan dalam vault Anda), dapat berisiko mengekspos konfigurasi SMTP Anda (termasuk nama pengguna dan kata sandi SMTP). Anda harus memastikan bahwa vault Anda diamankan dengan benar sebelum mengaktifkan otentikasi dua faktor. Jika Anda tidak dapat melakukan ini, setidaknya Anda harus membuat akun email baru, yang didedikasikan untuk tujuan ini, untuk mengurangi risiko yang terkait dengan konfigurasi SMTP yang diekspos.

---


### 5. <a name="SECTION5"></a>OPSI KONFIGURASI

Berikut list variabel yang ditemukan pada file konfigurasi CIDRAM `config.yml`, dengan deskripsi dari tujuan dan fungsi.

```
Konfigurasi (v3)
│
├───general
│       stages [string]
│       fields [string]
│       timezone [string]
│       time_offset [int]
│       time_format [string]
│       ipaddr [string]
│       http_response_header_code [int]
│       silent_mode [string]
│       silent_mode_response_header_code [int]
│       lang [string]
│       lang_override [bool]
│       numbers [string]
│       emailaddr [string]
│       emailaddr_display_style [string]
│       ban_override [int]
│       default_dns [string]
│       default_algo [string]
│       statistics [string]
│       force_hostname_lookup [bool]
│       allow_gethostbyaddr_lookup [bool]
│       disabled_channels [string]
│       request_proxy [string]
│       request_proxyauth [string]
│       default_timeout [int]
│       sensitive [string]
│       email_notification_address [string]
│       email_notification_name [string]
│       email_notification_when [string]
├───components
│       ipv4 [string]
│       ipv6 [string]
│       modules [string]
│       imports [string]
│       events [string]
├───logging
│       standard_log [string]
│       apache_style_log [string]
│       serialised_log [string]
│       error_log [string]
│       outbound_request_log [string]
│       report_log [string]
│       truncate [string]
│       log_rotation_limit [int]
│       log_rotation_action [string]
│       log_banned_ips [bool]
│       log_sanitisation [bool]
├───frontend
│       frontend_log [string]
│       signatures_update_event_log [string]
│       max_login_attempts [int]
│       theme [string]
│       theme_mode [string]
│       magnification [float]
│       custom_header [string]
│       custom_footer [string]
│       remotes [string]
│       enable_two_factor [bool]
├───signatures
│       shorthand [string]
│       default_tracktime [string]
│       infraction_limit [int]
│       tracking_override [bool]
│       conflict_response [int]
├───verification
│       search_engines [string]
│       social_media [string]
│       other [string]
│       adjust [string]
├───recaptcha
│       usemode [int]
│       lockip [bool]
│       lockuser [bool]
│       sitekey [string]
│       secret [string]
│       expiry [float]
│       recaptcha_log [string]
│       signature_limit [int]
│       api [string]
│       show_cookie_warning [bool]
│       show_api_message [bool]
│       nonblocked_status_code [int]
├───hcaptcha
│       usemode [int]
│       lockip [bool]
│       lockuser [bool]
│       sitekey [string]
│       secret [string]
│       expiry [float]
│       hcaptcha_log [string]
│       signature_limit [int]
│       api [string]
│       show_cookie_warning [bool]
│       show_api_message [bool]
│       nonblocked_status_code [int]
├───legal
│       pseudonymise_ip_addresses [bool]
│       privacy_policy [string]
├───template_data
│       theme [string]
│       theme_mode [string]
│       magnification [float]
│       css_url [string]
│       block_event_title [string]
│       captcha_title [string]
│       custom_header [string]
│       custom_footer [string]
├───rate_limiting
│       max_bandwidth [string]
│       max_requests [int]
│       precision_ipv4 [int]
│       precision_ipv6 [int]
│       allowance_period [string]
│       exceptions [string]
│       segregate [bool]
├───supplementary_cache_options
│       prefix [string]
│       enable_apcu [bool]
│       enable_memcached [bool]
│       enable_redis [bool]
│       enable_pdo [bool]
│       memcached_host [string]
│       memcached_port [int]
│       redis_host [string]
│       redis_port [int]
│       redis_timeout [float]
│       redis_database_number [int]
│       pdo_dsn [string]
│       pdo_username [string]
│       pdo_password [string]
└───bypasses
        used [string]
```

#### "general" (Kategori)
Konfigurasi umum (konfigurasi inti apapun yang bukan milik kategori lain).

##### "stages" `[string]`
- Kontrol untuk tahapan rantai eksekusi (apakah diaktifkan, apakah kesalahan dicatat, dll).

```
stages
├─Tests ("Jalankan tes untuk file tanda tangan")
├─Modules ("Jalankan modul")
├─SearchEngineVerification ("Jalankan verifikasi mesin pencari")
├─SocialMediaVerification ("Jalankan verifikasi media sosial")
├─OtherVerification ("Jalankan verifikasi lainnya")
├─Aux ("Jalankan aturan tambahan")
├─Tracking ("Jalankan pelacakan IP")
├─RL ("Jalankan pembatasan laju")
├─CAPTCHA ("Terapkan CAPTCHA (permintaan yang diblokir)")
├─Reporting ("Jalankan pelaporan")
├─Statistics ("Memperbarui statistik")
├─Webhooks ("Jalankan webhook")
├─PrepareFields ("Siapkan bidang untuk keluaran dan log")
├─Output ("Menghasilkan keluaran (permintaan yang diblokir)")
├─WriteLogs ("Mencatat ke log (permintaan yang diblokir)")
├─Terminate ("Hentikan permintaan (permintaan yang diblokir)")
├─AuxRedirect ("Arahkan ulang sesuai dengan aturan tambahan")
└─NonBlockedCAPTCHA ("Terapkan CAPTCHA (permintaan yang tidak diblokir)")
```

##### "fields" `[string]`
- Kontrol untuk bidang selama acara blokir (ketika permintaan diblokir).

```
fields
├─ID ("ID")
├─ScriptIdent ("Versi skrip")
├─DateTime ("Tanggal/Waktu")
├─IPAddr ("Alamat IP")
├─IPAddrResolved ("Alamat IP (terselesaikan)")
├─Query ("Kueri")
├─Referrer ("Halaman mengacu")
├─UA ("Agen pengguna")
├─UALC ("Agen pengguna (huruf kecil)")
├─SignatureCount ("Penghitungan tanda tangan")
├─Signatures ("Referensi tanda tangan")
├─WhyReason ("Mengapa diblokir")
├─ReasonMessage ("Mengapa diblokir (terperinci)")
├─rURI ("Direkonstruksi URI")
├─Infractions ("Pelanggaran")
├─ASNLookup ("** Pencarian ASN")
├─CCLookup ("** Pencarian kode negara")
├─Verified ("Identitas terverifikasi")
├─Expired ("Kedaluwarsa")
├─Ignored ("Diabaikan")
├─Request_Method ("Metode permintaan")
├─Protocol ("Protokol")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Nama host")
├─CAPTCHA ("Status CAPTCHA")
├─Inspection ("* Pemeriksaan kondisi")
└─ClientL10NAccepted ("Resolusi bahasa")
```

* Dimaksudkan hanya untuk men-debug aturan tambahan. Tidak ditampilkan kepada pengguna yang diblokir.

** Memerlukan fungsionalitas pencarian ASN (misalnya, melalui modul IP-API atau BGPView).

!! Ini adalah petunjuk klien dengan entropi rendah. Petunjuk klien adalah teknologi web eksperimental baru yang belum didukung secara luas di semua browser dan klien utama. *Melihat: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Meskipun petunjuk klien dapat berguna untuk sidik jari, karena petunjuk tersebut tidak didukung secara luas, kehadiran petunjuk klien tersebut dalam permintaan tidak boleh diasumsikan atau diandalkan (yaitu, memblokir berdasarkan ketidakhadiran mereka adalah ide yang buruk).

##### "timezone" `[string]`
- Ini digunakan untuk menentukan zona waktu yang akan digunakan (misalnya, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, dll). Menentukan "SYSTEM" untuk membiarkan PHP menangani ini untuk Anda secara otomatis.

```
timezone
├─SYSTEM ("Gunakan zona waktu default sistem.")
├─UTC ("UTC")
└─…Lain
```

##### "time_offset" `[int]`
- Offset zona waktu dalam hitungan menit.

##### "time_format" `[string]`
- Format notasi tanggal/waktu yang digunakan oleh CIDRAM. Opsi tambahan dapat ditambahkan atas permintaan.

```
time_format
├─{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz} ("{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}")
├─{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} ("{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss}")
├─{Day}, {dd} {Mon} {yyyy} ("{Day}, {dd} {Mon} {yyyy}")
├─{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} ("{yyyy}.{mm}.{dd} {hh}:{ii}:{ss}")
├─{yyyy}.{mm}.{dd} ("{yyyy}.{mm}.{dd}")
├─{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} ("{yyyy}-{mm}-{dd} {hh}:{ii}:{ss}")
├─{yyyy}-{mm}-{dd} ("{yyyy}-{mm}-{dd}")
├─{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} ("{yyyy}/{mm}/{dd} {hh}:{ii}:{ss}")
├─{yyyy}/{mm}/{dd} ("{yyyy}/{mm}/{dd}")
├─{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} ("{dd}.{mm}.{yyyy} {hh}:{ii}:{ss}")
├─{dd}.{mm}.{yyyy} ("{dd}.{mm}.{yyyy}")
├─{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} ("{dd}-{mm}-{yyyy} {hh}:{ii}:{ss}")
├─{dd}-{mm}-{yyyy} ("{dd}-{mm}-{yyyy}")
├─{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} ("{dd}/{mm}/{yyyy} {hh}:{ii}:{ss}")
├─{dd}/{mm}/{yyyy} ("{dd}/{mm}/{yyyy}")
├─{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} ("{mm}.{dd}.{yyyy} {hh}:{ii}:{ss}")
├─{mm}.{dd}.{yyyy} ("{mm}.{dd}.{yyyy}")
├─{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} ("{mm}-{dd}-{yyyy} {hh}:{ii}:{ss}")
├─{mm}-{dd}-{yyyy} ("{mm}-{dd}-{yyyy}")
├─{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} ("{mm}/{dd}/{yyyy} {hh}:{ii}:{ss}")
├─{mm}/{dd}/{yyyy} ("{mm}/{dd}/{yyyy}")
├─{yy}.{mm}.{dd} {hh}:{ii}:{ss} {tz} ("{yy}.{mm}.{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}.{mm}.{dd} {hh}:{ii}:{ss} ("{yy}.{mm}.{dd} {hh}:{ii}:{ss}")
├─{yy}.{mm}.{dd} ("{yy}.{mm}.{dd}")
├─{yy}-{mm}-{dd} {hh}:{ii}:{ss} {tz} ("{yy}-{mm}-{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}-{mm}-{dd} {hh}:{ii}:{ss} ("{yy}-{mm}-{dd} {hh}:{ii}:{ss}")
├─{yy}-{mm}-{dd} ("{yy}-{mm}-{dd}")
├─{yy}/{mm}/{dd} {hh}:{ii}:{ss} {tz} ("{yy}/{mm}/{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}/{mm}/{dd} {hh}:{ii}:{ss} ("{yy}/{mm}/{dd} {hh}:{ii}:{ss}")
├─{yy}/{mm}/{dd} ("{yy}/{mm}/{dd}")
├─{dd}.{mm}.{yy} {hh}:{ii}:{ss} {tz} ("{dd}.{mm}.{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}.{mm}.{yy} {hh}:{ii}:{ss} ("{dd}.{mm}.{yy} {hh}:{ii}:{ss}")
├─{dd}.{mm}.{yy} ("{dd}.{mm}.{yy}")
├─{dd}-{mm}-{yy} {hh}:{ii}:{ss} {tz} ("{dd}-{mm}-{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}-{mm}-{yy} {hh}:{ii}:{ss} ("{dd}-{mm}-{yy} {hh}:{ii}:{ss}")
├─{dd}-{mm}-{yy} ("{dd}-{mm}-{yy}")
├─{dd}/{mm}/{yy} {hh}:{ii}:{ss} {tz} ("{dd}/{mm}/{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}/{mm}/{yy} {hh}:{ii}:{ss} ("{dd}/{mm}/{yy} {hh}:{ii}:{ss}")
├─{dd}/{mm}/{yy} ("{dd}/{mm}/{yy}")
├─{mm}.{dd}.{yy} {hh}:{ii}:{ss} {tz} ("{mm}.{dd}.{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}.{dd}.{yy} {hh}:{ii}:{ss} ("{mm}.{dd}.{yy} {hh}:{ii}:{ss}")
├─{mm}.{dd}.{yy} ("{mm}.{dd}.{yy}")
├─{mm}-{dd}-{yy} {hh}:{ii}:{ss} {tz} ("{mm}-{dd}-{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}-{dd}-{yy} {hh}:{ii}:{ss} ("{mm}-{dd}-{yy} {hh}:{ii}:{ss}")
├─{mm}-{dd}-{yy} ("{mm}-{dd}-{yy}")
├─{mm}/{dd}/{yy} {hh}:{ii}:{ss} {tz} ("{mm}/{dd}/{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}/{dd}/{yy} {hh}:{ii}:{ss} ("{mm}/{dd}/{yy} {hh}:{ii}:{ss}")
├─{mm}/{dd}/{yy} ("{mm}/{dd}/{yy}")
├─{yyyy}年{m}月{d}日 {hh}時{ii}分{ss}秒 ("{yyyy}年{m}月{d}日 {hh}時{ii}分{ss}秒")
├─{yyyy}年{m}月{d}日 {hh}:{ii}:{ss} {tz} ("{yyyy}年{m}月{d}日 {hh}:{ii}:{ss} {tz}")
├─{yyyy}年{m}月{d}日 ("{yyyy}年{m}月{d}日")
├─{yy}年{m}月{d}日 {hh}時{ii}分{ss}秒 ("{yy}年{m}月{d}日 {hh}時{ii}分{ss}秒")
├─{yy}年{m}月{d}日 {hh}:{ii}:{ss} {tz} ("{yy}年{m}月{d}日 {hh}:{ii}:{ss} {tz}")
├─{yy}年{m}月{d}日 ("{yy}年{m}月{d}日")
├─{yyyy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초 ("{yyyy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초")
├─{yyyy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz} ("{yyyy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz}")
├─{yyyy}년 {m}월 {d}일 ("{yyyy}년 {m}월 {d}일")
├─{yy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초 ("{yy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초")
├─{yy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz} ("{yy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz}")
├─{yy}년 {m}월 {d}일 ("{yy}년 {m}월 {d}일")
├─{yyyy}-{mm}-{dd}T{hh}:{ii}:{ss}{t:z} ("{yyyy}-{mm}-{dd}T{hh}:{ii}:{ss}{t:z}")
├─{d}. {m}. {yyyy} ("{d}. {m}. {yyyy}")
└─…Lain
```

__*Placeholder – Penjelasan – Contoh berdasarkan 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – Tahun – Misalnya, 2024.<br />
`{yy}` – Tahun yang disingkat – Misalnya, 24.<br />
`{Mon}` – Nama bulan yang disingkat (dalam bahasa Inggris) – Misalnya, Apr.<br />
`{mm}` – Bulan dengan angka nol di depannya – Misalnya, 04.<br />
`{m}` – Bulan – Misalnya, 4.<br />
`{Day}` – Nama hari yang disingkat (dalam bahasa Inggris) – Misalnya, Tue.<br />
`{dd}` – Hari dengan angka nol di depannya – Misalnya, 30.<br />
`{d}` – Hari – Misalnya, 30.<br />
`{hh}` – Jam dengan angka nol di depannya (menggunakan waktu 24 jam) – Misalnya, 18.<br />
`{h}` – Jam (menggunakan waktu 24 jam) – Misalnya, 18.<br />
`{ii}` – Menit dengan angka nol di depannya – Misalnya, 27.<br />
`{i}` – Menit – Misalnya, 27.<br />
`{ss}` – Detik dengan angka nol di depannya – Misalnya, 49.<br />
`{s}` – Detik – Misalnya, 49.<br />
`{tz}` – Zona waktu (tanpa titik dua) – Misalnya, +0800.<br />
`{t:z}` – Zona waktu (dengan titik dua) – Misalnya, +08:00.

##### "ipaddr" `[string]`
- Dimana menemukan alamat IP dari menghubungkan permintaan? (Berguna untuk layanan seperti Cloudflare). Default = REMOTE_ADDR. PERINGATAN: Jangan ganti ini kecuali Anda tahu apa yang Anda lakukan!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Default)")
└─…Lain
```

Lihat juga:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Pesan status HTTP mana yang harus dikirim oleh CIDRAM ketika memblokir permintaan?

```
http_response_header_code
├─200 (200 OK): Paling tidak kuat, tetapi paling ramah-pengguna. Permintaan otomatis
│ kemungkinan besar akan menafsirkan respons ini sebagai indikasi bahwa
│ permintaan berhasil.
├─403 (403 Forbidden (Terlarang)): Lebih kuat, tetapi kurang ramah-pengguna. Direkomendasikan untuk kebanyakan
│ keadaan umum.
├─410 (410 Gone (Dipergi)): Dapat menyebabkan masalah saat menyelesaikan kesalahan positif, karena
│ beberapa browser akan menyimpan pesan status ini di cache dan tidak mengirim
│ permintaan berikutnya, bahkan setelah tidak diblokir lagi. Mungkin yang
│ paling disukai dalam beberapa konteks, untuk jenis lalu lintas tertentu.
├─418 (418 I'm a teapot (Saya adalah teko)): Referensi pada lelucon April Mop (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Probabilitas rendah bahwa
│ akan dipahami oleh klien, bot, browser, atau lainnya. Disediakan untuk
│ hiburan dan kenyamanan, tetapi umumnya tidak direkomendasikan.
├─451 (451 Unavailable For Legal Reasons (Tidak tersedia karena alasan hukum)): Direkomendasikan saat memblokir terutama karena alasan hukum. Tidak
│ direkomendasikan dalam konteks lain.
└─503 (503 Service Unavailable (Layanan tidak tersedia)): Paling kuat, tetapi paling tidak ramah-pengguna. Direkomendasikan untuk saat
  diserang, atau saat berhadapan dengan lalu lintas yang tidak diinginkan yang
  sangat persisten.
```

##### "silent_mode" `[string]`
- Seharusnya CIDRAM diam-diam mengarahkan diblokir upaya akses bukannya menampilkan halaman "akses ditolak"? Jika ya, menentukan lokasi untuk mengarahkan diblokir upaya akses. Jika tidak, kosongkan variabel ini.

##### "silent_mode_response_header_code" `[int]`
- Pesan status HTTP mana yang harus dikirim oleh CIDRAM saat secara diam-diam mengarahkan upaya akses yang diblokir?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Dipindahkan Secara Permanen)): Menginstruksikan klien bahwa pengalihan adalah PERMANEN, dan bahwa metode
│ permintaan yang digunakan untuk pengalihan MUNGKIN berbeda dari metode
│ permintaan yang digunakan untuk permintaan awal.
├─302 (302 Found (Ditemukan)): Menginstruksikan klien bahwa pengalihan adalah SEMENTARA, dan bahwa metode
│ permintaan yang digunakan untuk pengalihan MUNGKIN berbeda dari metode
│ permintaan yang digunakan untuk permintaan awal.
├─307 (307 Temporary Redirect (Pengalihan Sementara)): Menginstruksikan klien bahwa pengalihan adalah SEMENTARA, dan bahwa metode
│ permintaan yang digunakan untuk pengalihan TIDAK mungkin berbeda dari metode
│ permintaan yang digunakan untuk permintaan awal.
└─308 (308 Permanent Redirect (Pengalihan Permanen)): Menginstruksikan klien bahwa pengalihan adalah PERMANEN, dan bahwa metode
  permintaan yang digunakan untuk pengalihan TIDAK mungkin berbeda dari metode
  permintaan yang digunakan untuk permintaan awal.
```

Terlepas dari bagaimana kami menginstruksikan klien, penting untuk diingat bahwa pada akhirnya kami tidak memiliki kendali atas apa yang klien pilih untuk dilakukan, dan tidak ada jaminan bahwa klien akan menghormati instruksi kami.

##### "lang" `[string]`
- Tentukan bahasa default untuk CIDRAM.

```
lang
├─af ("Afrikaans")
├─ar ("العربية")
├─bg ("Български")
├─bn ("বাংলা")
├─bs ("Bosanski")
├─ca ("Català")
├─cs ("Čeština")
├─de ("Deutsch")
├─en ("English (AU/GB/NZ)")
├─en-CA ("English (CA)")
├─en-US ("English (US)")
├─es ("Español")
├─fa ("فارسی")
├─fr ("Français (FR)")
├─fr-CA ("Français (CA)")
├─gl ("Galego")
├─gu ("ગુજરાતી")
├─he ("עברית")
├─hi ("हिंदी")
├─hr ("Hrvatski")
├─id ("Bahasa Indonesia")
├─it ("Italiano")
├─ja ("日本語")
├─ko ("한국어")
├─lv ("Latviešu")
├─ml ("മലയാളം")
├─mr ("मराठी")
├─ms ("Bahasa Melayu")
├─nl ("Nederlandse")
├─no ("Norsk")
├─pa ("ਪੰਜਾਬੀ")
├─pl ("Polski")
├─pt-BR ("Português (Brasil)")
├─pt-PT ("Português (Europeu)")
├─ro ("Română")
├─ru ("Русский")
├─sv ("Svenska")
├─sr ("Српски")
├─ta ("தமிழ்")
├─th ("ภาษาไทย")
├─tr ("Türkçe")
├─uk ("Українська")
├─ur ("اردو")
├─vi ("Tiếng Việt")
├─zh-Hans ("中文（简体）")
└─zh-Hant ("中文（傳統）")
```

##### "lang_override" `[bool]`
- Melokalisasikan sesuai dengan HTTP_ACCEPT_LANGUAGE jika/bila memungkinkan? True = Ya [Default]; False = Tidak.

##### "numbers" `[string]`
- Cara apa yang kamu suka nomor menjadi ditampilkan? Pilih contoh yang paling sesuai untuk Anda.

```
numbers
├─Arabic-1 ("١٢٣٤٥٦٧٫٨٩")
├─Arabic-2 ("١٬٢٣٤٬٥٦٧٫٨٩")
├─Arabic-3 ("۱٬۲۳۴٬۵۶۷٫۸۹")
├─Arabic-4 ("۱۲٬۳۴٬۵۶۷٫۸۹")
├─Armenian ("Ճ̅Ի̅Գ̅ՏՇԿԷ")
├─Base-12 ("4b6547.a8")
├─Base-16 ("12d687.e3")
├─Bengali-1 ("১২,৩৪,৫৬৭.৮৯")
├─Burmese-1 ("၁၂၃၄၅၆၇.၈၉")
├─China-1 ("123,4567.89")
├─Chinese-Simplified ("一百二十三万四千五百六十七点八九")
├─Chinese-Simplified-Financial ("壹佰贰拾叁萬肆仟伍佰陆拾柒点捌玖")
├─Chinese-Traditional ("一百二十三萬四千五百六十七點八九")
├─Chinese-Traditional-Financial ("壹佰貳拾叄萬肆仟伍佰陸拾柒點捌玖")
├─Fullwidth ("１２３４５６７.８９")
├─Geez ("፻፳፫፼፵፭፻፷፯")
├─Hebrew ("א׳׳ב׳קג׳יד׳ךסז")
├─India-1 ("12,34,567.89")
├─India-2 ("१२,३४,५६७.८९")
├─India-3 ("૧૨,૩૪,૫૬૭.૮૯")
├─India-4 ("੧੨,੩੪,੫੬੭.੮੯")
├─India-5 ("೧೨,೩೪,೫೬೭.೮೯")
├─India-6 ("౧౨,౩౪,౫౬౭.౮౯")
├─Japanese ("百万二十万三万四千五百六十七・八九分")
├─Javanese ("꧑꧒꧓꧔꧕꧖꧗.꧘꧙")
├─Khmer-1 ("១.២៣៤.៥៦៧,៨៩")
├─Lao-1 ("໑໒໓໔໕໖໗.໘໙")
├─Latin-1 ("1,234,567.89")
├─Latin-2 ("1 234 567.89")
├─Latin-3 ("1.234.567,89")
├─Latin-4 ("1 234 567,89")
├─Latin-5 ("1,234,567·89")
├─Mayan ("𝋧𝋮𝋦𝋨𝋧.𝋱𝋰")
├─Mongolian ("᠑᠒᠓᠔᠕᠖᠗.᠘᠙")
├─NoSep-1 ("1234567.89")
├─NoSep-2 ("1234567,89")
├─Odia ("୧୨୩୪୫୬୭.୮୯")
├─Roman ("M̅C̅C̅X̅X̅X̅I̅V̅DLXVII")
├─SDN-Dwiggins ("4E6,547;X8")
├─SDN-Pitman ("4↋6,547;↊8")
├─Tamil ("௲௲௨௱௲௩௰௲௪௲௫௱௬௰௭")
├─Thai-1 ("๑,๒๓๔,๕๖๗.๘๙")
├─Thai-2 ("๑๒๓๔๕๖๗.๘๙")
└─Tibetan ("༡༢༣༤༥༦༧.༨༩")
```

##### "emailaddr" `[string]`
- Jika Anda ingin, Anda dapat menyediakan alamat email sini untuk diberikan kepada pengguna ketika diblokir, bagi mereka untuk menggunakan sebagai metode kontak untuk dukungan dan/atau bantuan untuk dalam hal mereka menjadi diblokir keliru atau diblokir oleh kesalahan. PERINGATAN: Apapun alamat email Anda menyediakan sini akan pasti diperoleh oleh spambots dan pencakar/scrapers ketika digunakan disini, dan karena itu, jika Anda ingin memberikan alamat email disini, itu sangat direkomendasikan Anda memastikan bahwa alamat email yang Anda berikan disini adalah alamat yang dapat dibuang dan/atau adalah alamat Anda tidak keberatan menjadi di-spam (dengan kata lain, Anda mungkin tidak ingin untuk menggunakan Anda alamat email yang personal primer atau bisnis primer).

##### "emailaddr_display_style" `[string]`
- Bagaimana Anda lebih suka alamat email yang akan disajikan kepada pengguna?

```
emailaddr_display_style
├─default ("Link yang dapat diklik")
└─noclick ("Teks yang tidak dapat diklik")
```

##### "ban_override" `[int]`
- Mengesampingkan "http_response_header_code" ketika "infraction_limit" adalah melampaui? 200 = Jangan mengesampingkan [Default]. Nilai lainnya sama dengan nilai yang tersedia untuk "http_response_header_code".

```
ban_override
├─200 (200 OK): Paling tidak kuat, tetapi paling ramah-pengguna. Permintaan otomatis
│ kemungkinan besar akan menafsirkan respons ini sebagai indikasi bahwa
│ permintaan berhasil.
├─403 (403 Forbidden (Terlarang)): Lebih kuat, tetapi kurang ramah-pengguna. Direkomendasikan untuk kebanyakan
│ keadaan umum.
├─410 (410 Gone (Dipergi)): Dapat menyebabkan masalah saat menyelesaikan kesalahan positif, karena
│ beberapa browser akan menyimpan pesan status ini di cache dan tidak mengirim
│ permintaan berikutnya, bahkan setelah tidak diblokir lagi. Mungkin yang
│ paling disukai dalam beberapa konteks, untuk jenis lalu lintas tertentu.
├─418 (418 I'm a teapot (Saya adalah teko)): Referensi pada lelucon April Mop (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Probabilitas rendah bahwa
│ akan dipahami oleh klien, bot, browser, atau lainnya. Disediakan untuk
│ hiburan dan kenyamanan, tetapi umumnya tidak direkomendasikan.
├─451 (451 Unavailable For Legal Reasons (Tidak tersedia karena alasan hukum)): Direkomendasikan saat memblokir terutama karena alasan hukum. Tidak
│ direkomendasikan dalam konteks lain.
└─503 (503 Service Unavailable (Layanan tidak tersedia)): Paling kuat, tetapi paling tidak ramah-pengguna. Direkomendasikan untuk saat
  diserang, atau saat berhadapan dengan lalu lintas yang tidak diinginkan yang
  sangat persisten.
```

##### "default_dns" `[string]`
- Daftar server DNS yang digunakan untuk pencarian nama host. PERINGATAN: Jangan ganti ini kecuali Anda tahu apa yang Anda lakukan!

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.id.md#apa-yang-bisa-saya-gunakan-untuk-default_dns" hreflang="id-ID">Apa yang bisa saya gunakan untuk "default_dns"?</a>*

##### "default_algo" `[string]`
- Mendefinisikan algoritma mana yang akan digunakan untuk semua kata sandi dan sesi di masa depan.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Mengontrol informasi statistik mana yang akan dilacak.

```
statistics
├─Blocked-IPv4 ("Permintaan diblokir – IPv4")
├─Blocked-IPv6 ("Permintaan diblokir – IPv6")
├─Blocked-Other ("Permintaan diblokir – Lain")
├─Banned-IPv4 ("Permintaan dilarang – IPv4")
├─Banned-IPv6 ("Permintaan dilarang – IPv6")
├─Passed-IPv4 ("Permintaan berlalu – IPv4")
├─Passed-IPv6 ("Permintaan berlalu – IPv6")
├─Passed-Other ("Permintaan berlalu – Lain")
├─CAPTCHAs-Failed ("Upaya CAPTCHA – Gagal!")
├─CAPTCHAs-Passed ("Upaya CAPTCHA – Lulus!")
├─Reported-IPv4-OK ("Permintaan dilaporkan ke API eksternal – IPv4 – OK")
├─Reported-IPv4-Failed ("Permintaan dilaporkan ke API eksternal – IPv4 – Gagal")
├─Reported-IPv6-OK ("Permintaan dilaporkan ke API eksternal – IPv6 – OK")
└─Reported-IPv6-Failed ("Permintaan dilaporkan ke API eksternal – IPv6 – Gagal")
```

Catat: Apakah akan melacak statistik untuk aturan tambahan dapat dikontrol dari halaman aturan tambahan.

##### "force_hostname_lookup" `[bool]`
- Memaksa periksa untuk nama host? True = Ya; False = Tidak [Default]. Periksa untuk nama host biasanya dilakukan pada dasar "sesuai kebutuhan", tapi bisa dipaksakan untuk semua permintaan. Melakukan hal tersebut mungkin berguna sebagai sarana untuk memberikan informasi lebih rinci di log, tapi mungkin juga memiliki sedikit efek negatif pada kinerja.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Izinkan menggunakan gethostbyaddr saat UDP tidak tersedia? True = Ya [Default]; False = Tidak.

Catat: Pencarian IPv6 mungkin tidak bekerja dengan benar pada beberapa sistem 32-bit.

##### "disabled_channels" `[string]`
- Ini dapat digunakan untuk mencegah CIDRAM dari menggunakan saluran tertentu saat mengirim permintaan (misalnya, saat memperbarui, saat mengambil metadata komponen, dll).

```
disabled_channels
├─GitHub ("<span class="origin us">US</span> GitHub")
├─BitBucket ("<span class="origin us">US</span> BitBucket")
├─Codeberg ("<span class="origin de">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin us">US</span> GoogleDNS")
```

##### "request_proxy" `[string]`
- Jika Anda ingin permintaan keluar dikirim melalui proxy, tentukan proxy tersebut disini. Jika tidak, biarkan ini kosong.

##### "request_proxyauth" `[string]`
- Jika mengirim permintaan keluar melalui proxy dan jika proxy tersebut memerlukan nama pengguna dan kata sandi, tentukan nama pengguna dan kata sandi tersebut disini (misalnya, `user:pass`). Jika tidak, biarkan ini kosong.

##### "default_timeout" `[int]`
- Batas waktu default yang digunakan untuk permintaan eksternal? Default = 12 detik.

##### "sensitive" `[string]`
- Daftar jalur yang dianggap sebagai halaman sensitif. Setiap jalur yang terdaftar akan diperiksa terhadap URI yang direkonstruksi bila diperlukan. Jalur yang dimulai dengan garis miring ke depan akan diperlakukan sebagai literal, dan dicocokkan dari komponen jalur permintaan selanjutnya. Jika tidak, jalur yang dimulai dengan karakter non-alfanumerik, dan diakhiri dengan karakter yang sama (atau karakter yang sama ditambah tanda "i" opsional) akan diperlakukan sebagai ekspresi reguler. Jenis jalur lain apapun akan diperlakukan sebagai literal, dan dapat dicocokkan dari bagian manapun dari URI. Apakah jalur dianggap sebagai halaman sensitif dapat memengaruhi perilaku beberapa modul, tetapi sebaliknya tidak berpengaruh apapun.

##### "email_notification_address" `[string]`
- Jika Anda memilih untuk menerima notifikasi dari CIDRAM melalui email, misalnya, ketika aturan tambahan tertentu dipicu, Anda dapat menentukan alamat penerima untuk notifikasi tersebut disini.

##### "email_notification_name" `[string]`
- Jika Anda memilih untuk menerima notifikasi dari CIDRAM melalui email, misalnya, ketika aturan tambahan tertentu dipicu, Anda dapat menentukan nama penerima untuk notifikasi tersebut disini.

##### "email_notification_when" `[string]`
- Kapan harus mengirim notifikasi setelah mereka dibuat.

```
email_notification_when
├─Immediately ("Segera.")
├─After24Hours ("Setelah 24 jam, digabungkan bersama (atau ketika dipicu secara manual, misalnya, melalui cron).")
└─ManuallyOnly ("Hanya bila dipicu secara manual (misalnya, melalui cron).")
```

#### "components" (Kategori)
Konfigurasi untuk pengaktifan dan penonaktifan komponen yang digunakan oleh CIDRAM. Biasanya diisi oleh halaman pembaruan, tetapi juga dapat dikelola dari sini untuk kontrol yang lebih baik dan untuk komponen dipersonalisasi yang tidak dikenali oleh halaman pembaruan.

##### "ipv4" `[string]`
- File tanda tangan IPv4.

##### "ipv6" `[string]`
- File tanda tangan IPv6.

##### "modules" `[string]`
- Modul.

##### "imports" `[string]`
- Impor. Biasanya digunakan untuk memasok informasi konfigurasi komponen ke CIDRAM.

##### "events" `[string]`
- Penangan acara. Biasanya digunakan untuk memodifikasi cara CIDRAM berperilaku secara internal atau untuk menyediakan fungsionalitas tambahan.

#### "logging" (Kategori)
Konfigurasi yang terkait dengan pencatatan (tidak termasuk yang berlaku untuk kategori lain).

##### "standard_log" `[string]`
- File yang dapat dibaca oleh manusia untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- File yang dalam gaya Apache untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- File serial untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- File untuk mencatat kesalahan tidak fatal yang terdeteksi. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- File untuk mencatat hasil permintaan keluar apapun. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- File untuk mencatat setiap laporan yang dikirim ke API eksternal. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- Memotong file log ketika mereka mencapai ukuran tertentu? Nilai adalah ukuran maksimum dalam B/KB/MB/GB/TB yang bisa ditambahkan untuk file log sebelum dipotong. Nilai default 0KB menonaktifkan pemotongan (file log dapat tumbuh tanpa batas waktu). Catat: Berlaku untuk file log individu! Ukuran file log tidak dianggap secara kolektif.

##### "log_rotation_limit" `[int]`
- Rotasi log membatasi jumlah file log yang seharusnya ada pada satu waktu. Ketika file log baru dibuat, jika jumlah total file log melebihi batas yang ditentukan, tindakan yang ditentukan akan dilakukan. Anda dapat menentukan batas yang diinginkan disini. Nilai 0 akan menonaktifkan rotasi log.

##### "log_rotation_action" `[string]`
- Rotasi log membatasi jumlah file log yang seharusnya ada pada satu waktu. Ketika file log baru dibuat, jika jumlah total file log melebihi batas yang ditentukan, tindakan yang ditentukan akan dilakukan. Anda dapat menentukan tindakan yang diinginkan disini.

```
log_rotation_action
├─Delete ("Hapus file log tertua, hingga batasnya tidak lagi terlampaui.")
└─Archive ("Pertama arsipkan, lalu hapus file log tertua, hingga batasnya tidak lagi terlampaui.")
```

##### "log_banned_ips" `[bool]`
- Termasuk permintaan diblokir dari IP dilarang dalam file log? True = Ya [Default]; False = Tidak.

##### "log_sanitisation" `[bool]`
- Saat menggunakan halaman log untuk melihat data log, CIDRAM mensanitasikan data log sebelum menampilkannya, untuk melindungi pengguna dari serangan XSS dan potensi ancaman lain yang bisa terkandung dalam data tersebut. Namun, secara default, data tidak disanitasikan selama pencatatan. Ini untuk memastikan bahwa data log dicatat secara akurat, untuk membantu analisis heuristik atau forensik yang mungkin diperlukan di masa depan. Namun, jika pengguna mencoba membaca data log menggunakan alat eksternal, dan jika alat eksternal itu tidak melakukan proses sanitasi sendiri, pengguna bisa terkena serangan XSS. Jika perlu, Anda dapat mengubah perilaku default menggunakan direktif konfigurasi ini. True = Mensanitasikan data saat mencatatnya (data disimpan kurang akurat, tetapi risiko XSS lebih rendah). False = Jangan mensanitasikan data saat mencatatnya (data disimpan lebih akurat, tetapi risiko XSS lebih tinggi) [Default].

#### "frontend" (Kategori)
Konfigurasi untuk front-end.

##### "frontend_log" `[string]`
- File untuk mencatat upaya masuk bagian depan. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- File untuk mencatat ketika tanda tangan diperbarui melalui bagian depan. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Jumlah maksimum upaya memasukkan ke bagian depan. Default = 5.

##### "theme" `[string]`
- Tema yang akan digunakan untuk front-end.

```
theme
├─default ("Default")
├─bluemetal ("Blue Metal")
├─fullmoon ("Full Moon")
├─moss ("Moss")
├─primer ("Primer")
├─primerdark ("Primer Dark")
├─rbi ("Red-Blue Inverted")
├─slate ("Slate")
└─…Lain
```

##### "theme_mode" `[string]`
- Mode untuk tema yang akan digunakan untuk front-end.

```
theme_mode
├─normal ("Normal")
└─inverted ("Terbalik")
```

##### "magnification" `[float]`
- Perbesaran font. Default = 1.

##### "custom_header" `[string]`
- Disisipkan sebagai HTML di awal semua halaman front-end. Ini dapat berguna jika Anda ingin menyertakan logo situs web, header yang dipersonalisasi, skrip, atau sejenisnya di semua halaman tersebut.

##### "custom_footer" `[string]`
- Disisipkan sebagai HTML di akhir semua halaman front-end. Ini dapat berguna jika Anda ingin menyertakan pemberitahuan hukum, tautan kontak, informasi bisnis, atau sejenisnya di semua halaman tersebut.

##### "remotes" `[string]`
- Daftar alamat yang digunakan oleh pembaru untuk mengambil metadata komponen. Ini mungkin perlu disesuaikan saat memutakhirkan ke versi utama baru, atau saat memperoleh sumber baru untuk pembaruan, tetapi dalam keadaan normal harus dibiarkan saja.

##### "enable_two_factor" `[bool]`
- Direktif ini menentukan apakah akan menggunakan 2FA untuk akun depan.

#### "signatures" (Kategori)
Konfigurasi untuk tanda tangan, file tanda tangan, modul, dll.

##### "shorthand" `[string]`
- Kontrol untuk apa yang harus dilakukan dengan permintaan jika/ketika ada kecocokan yang positif dengan tanda tangan yang menggunakan kata-kata singkat yang diberikan.

```
shorthand
├─Attacks ("Serangan")
├─Bogon ("⁰ IP yang bogon")
├─Cloud ("Layanan komputasi awan")
├─Generic ("Umum")
├─Legal ("¹ Hukum")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Spam")
├─Banned ("³ Dilarang")
├─BadIP ("³ IP tidak valid")
├─RL ("³ Laju terbatas")
├─Conflict ("³ Konflik")
└─Other ("⁴ Lain")
```

__0.__ Jika situs web Anda memerlukan akses melalui LAN atau localhost, jangan blokir ini. Jika tidak memerlukannya, Anda dapat memblokir ini.

__1.__ Tidak ada file tanda tangan default yang menggunakan ini, tapi tetap didukung dalam kasus mungkin berguna untuk beberapa pengguna.

__2.__ Jika Anda memerlukan pengguna untuk dapat mengakses situs web Anda melalui proxy, jangan blokir ini. Jika tidak memerlukannya, Anda dapat memblokir ini.

__3.__ Penggunaan langsung dalam tanda tangan tidak didukung, tetapi mungkin dipanggil dengan cara lain dalam keadaan tertentu.

__4.__ Mengacu pada kasus dimana kata-kata singkat tidak digunakan sama sekali, atau tidak dikenali oleh CIDRAM.

__Satu per tanda tangan.__ Tanda tangan dapat memanggil beberapa profil, tetapi hanya dapat menggunakan satu kata singkat. Ada kemungkinan bahwa beberapa kata singkat mungkin cocok, tetapi karena hanya satu dapat digunakan, kami bertujuan untuk selalu menggunakan hanya yang paling cocok.

__Prioritas.__ Opsi yang dipilih selalu diprioritaskan daripada opsi yang tidak dipilih. Misalnya, jika beberapa kata-kata singkat sedang di tangan, tetapi hanya satu yang disetel sebagai diblokir, permintaan akan tetap diblokir.

__Titik akhir manusia dan layanan komputasi awan.__ Layanan komputasi awan dapat merujuk ke penyedia hosting web, server farm, pusat data, atau sejumlah hal lainnya. Titik akhir manusia mengacu pada cara manusia mengakses internet, seperti melalui penyedia layanan internet. Jaringan biasanya menyediakan hanya satu atau lain, tetapi kadang-kadang dapat menyediakan keduanya. Kami bertujuan untuk tidak pernah mengidentifikasi titik akhir manusia potensial sebagai layanan komputasi awan. Demikian, layanan komputasi awan dapat diidentifikasi sebagai sesuatu lain jika rentangnya dibagi oleh titik akhir manusia yang dikenal. Dengan cara yang sama, kami bertujuan untuk selalu mengidentifikasi layanan cloud, yang rentangnya tidak dibagikan oleh titik akhir manusia yang dikenal, sebagai layanan komputasi awan. Akibatnya, permintaan yang diidentifikasi eksplisit sebagai layanan komputasi awan paling mungkin tidak berbagi rentangnya dengan titik akhir manusia yang diketahui. Demikian juga, permintaan yang diidentifikasi eksplisit oleh serangan atau oleh risiko spam paling mungkin membagikannya. Namun, internet selalu berubah, tujuan jaringan berubah dari waktu ke waktu, dan rentang-rentang selalu dibeli atau dijual, jadi tetaplah sadar dan waspada dalam hal positif palsu.

##### "default_tracktime" `[string]`
- Durasi yang alamat IP harus dilacak. Default = 7d0°0′0″ (1 seminggu).

##### "infraction_limit" `[int]`
- Jumlah maksimum pelanggaran IP diperbolehkan untuk dikenakan sebelum dilarang oleh pelacakan IP. Default = 10.

##### "tracking_override" `[bool]`
- Izinkan modul untuk mengganti opsi pelacakan? True = Ya [Default]; False = Tidak.

##### "conflict_response" `[int]`
- Bila terdapat terlalu banyak upaya simultan untuk mengakses sumber daya yang sama (misalnya, permintaan simultan ke beberapa proses PHP pada mesin yang sama untuk sumber daya yang sama), beberapa upaya tersebut mungkin gagal. Jika hal ini memengaruhi file tanda tangan atau modul, CIDRAM mungkin tidak dapat membuat penentuan efektif mengenai permintaan tersebut. Jika ini terjadi, haruskah permintaan diblokir, dan mana pesan status HTTP harus CIDRAM kirim?

```
conflict_response
├─0 (Jangan blokir permintaan tersebut.): Jika Anda lebih suka permintaan diblokir hanya bila Anda yakin permintaan
│ tersebut jahat, atau Anda lebih suka berhati-hati terhadap positif palsu
│ (dengan risiko lalu lintas yang tidak diinginkan terkadang masuk), pilih
│ ini. Jika Anda lebih suka permintaan diblokir bila Anda tidak yakin
│ permintaan tersebut tidak berbahaya, atau Anda lebih suka bersikap waspada
│ (dengan risiko positif palsu sesekali), pilih dari opsi lain yang tersedia.
├─409 (409 Konflik): Direkomendasikan untuk konflik sumber daya (misalnya, konflik penggabungan,
│ konflik akses berkas, dll). Tidak direkomendasikan dalam konteks lain.
└─429 (429 Too Many Requests (Terlalu Banyak Permintaan)): Direkomendasikan untuk pembatasan laju, saat menangani serangan DDoS, dan
  untuk pencegahan banjir. Tidak direkomendasikan dalam konteks lain.
```

#### "verification" (Kategori)
Konfigurasi untuk memverifikasi dari mana permintaan berasal.

##### "search_engines" `[string]`
- Kontrol untuk memverifikasi permintaan dari mesin pencari.

```
search_engines
├─Amazonbot ("Amazonbot")
├─Applebot ("Applebot")
├─Baidu ("* Baiduspider/百度")
├─Bingbot ("* Bingbot")
├─DuckDuckBot ("* DuckDuckBot")
├─Googlebot ("* Googlebot")
├─MojeekBot ("MojeekBot")
├─PetalBot ("* PetalBot")
├─Qwantify ("Qwantify/Bleriot")
├─SeznamBot ("SeznamBot")
├─Sogou ("* Sogou/搜狗")
├─Yahoo ("Yahoo/Slurp")
├─Yandex ("* Yandex/Яндекс")
└─YoudaoBot ("YoudaoBot")
```

__Apa itu "positif" dan "negatif"?__ Saat memverifikasi identitas yang disajikan oleh permintaan, hasil yang berhasil dapat digambarkan sebagai "positif" atau "negatif". Ketika identitas yang disajikan dikonfirmasi sebagai identitas sebenarnya, itu akan digambarkan sebagai "positif". Ketika identitas yang disajikan dikonfirmasi sebagai dipalsukan, itu akan digambarkan sebagai "negatif". Namun, hasil yang tidak berhasil (misalnya, verifikasi gagal, atau kebenaran identitas yang disajikan tidak dapat ditentukan) tidak akan digambarkan sebagai "positif" atau "negatif". Sebaliknya, hasil yang tidak berhasil akan digambarkan sebagai tidak diverifikasi. Ketika tidak ada upaya untuk memverifikasi identitas yang disajikan oleh permintaan, permintaan tersebut juga akan digambarkan sebagai tidak diverifikasi. Istilah tersebut masuk akal hanya dalam konteks dimana identitas yang disajikan oleh permintaan dikenali, dan jadi, dimana verifikasi dimungkinkan. Jika identitas yang disajikan tidak sesuai dengan opsi yang diberikan di atas, atau jika tidak ada identitas yang disajikan, opsi yang diberikan di atas menjadi tidak relevan.

__Apa itu "bypass satu pelanggaran"?__ Dalam beberapa kasus, permintaan diverifikasi secara positif mungkin masih diblokir sebagai akibat dari file tanda tangan, modul, atau kondisi permintaan lainnya, dan bypass mungkin diperlukan untuk menghindari positif palsu. Dalam kasus dimana bypass dimaksudkan untuk menangani tepat satu pelanggaran, tidak lebih dan tidak kurang, bypass seperti itu dapat digambarkan sebagai "bypass satu pelanggaran".

* Opsi ini memiliki bypass terkait dibawah `bypasses➡used`. Direkomendasikan untuk memastikan bahwa kotak centang untuk bypass terkait ditandai dengan cara yang sama seperti kotak centang untuk mencoba memverifikasi opsi ini.

##### "social_media" `[string]`
- Kontrol untuk memverifikasi permintaan dari platform media sosial.

```
social_media
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__Apa itu "positif" dan "negatif"?__ Saat memverifikasi identitas yang disajikan oleh permintaan, hasil yang berhasil dapat digambarkan sebagai "positif" atau "negatif". Ketika identitas yang disajikan dikonfirmasi sebagai identitas sebenarnya, itu akan digambarkan sebagai "positif". Ketika identitas yang disajikan dikonfirmasi sebagai dipalsukan, itu akan digambarkan sebagai "negatif". Namun, hasil yang tidak berhasil (misalnya, verifikasi gagal, atau kebenaran identitas yang disajikan tidak dapat ditentukan) tidak akan digambarkan sebagai "positif" atau "negatif". Sebaliknya, hasil yang tidak berhasil akan digambarkan sebagai tidak diverifikasi. Ketika tidak ada upaya untuk memverifikasi identitas yang disajikan oleh permintaan, permintaan tersebut juga akan digambarkan sebagai tidak diverifikasi. Istilah tersebut masuk akal hanya dalam konteks dimana identitas yang disajikan oleh permintaan dikenali, dan jadi, dimana verifikasi dimungkinkan. Jika identitas yang disajikan tidak sesuai dengan opsi yang diberikan di atas, atau jika tidak ada identitas yang disajikan, opsi yang diberikan di atas menjadi tidak relevan.

__Apa itu "bypass satu pelanggaran"?__ Dalam beberapa kasus, permintaan diverifikasi secara positif mungkin masih diblokir sebagai akibat dari file tanda tangan, modul, atau kondisi permintaan lainnya, dan bypass mungkin diperlukan untuk menghindari positif palsu. Dalam kasus dimana bypass dimaksudkan untuk menangani tepat satu pelanggaran, tidak lebih dan tidak kurang, bypass seperti itu dapat digambarkan sebagai "bypass satu pelanggaran".

* Opsi ini memiliki bypass terkait dibawah `bypasses➡used`. Direkomendasikan untuk memastikan bahwa kotak centang untuk bypass terkait ditandai dengan cara yang sama seperti kotak centang untuk mencoba memverifikasi opsi ini.

** Memerlukan fungsionalitas pencarian ASN (misalnya, melalui modul IP-API atau BGPView).

*!! Kemungkinan tinggi menyebabkan positif palsu karena iMessage.

##### "other" `[string]`
- Kontrol untuk memverifikasi jenis permintaan lain jika/bila memungkinkan.

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
└─GPTBot ("!! GPTBot")
```

__Apa itu "positif" dan "negatif"?__ Saat memverifikasi identitas yang disajikan oleh permintaan, hasil yang berhasil dapat digambarkan sebagai "positif" atau "negatif". Ketika identitas yang disajikan dikonfirmasi sebagai identitas sebenarnya, itu akan digambarkan sebagai "positif". Ketika identitas yang disajikan dikonfirmasi sebagai dipalsukan, itu akan digambarkan sebagai "negatif". Namun, hasil yang tidak berhasil (misalnya, verifikasi gagal, atau kebenaran identitas yang disajikan tidak dapat ditentukan) tidak akan digambarkan sebagai "positif" atau "negatif". Sebaliknya, hasil yang tidak berhasil akan digambarkan sebagai tidak diverifikasi. Ketika tidak ada upaya untuk memverifikasi identitas yang disajikan oleh permintaan, permintaan tersebut juga akan digambarkan sebagai tidak diverifikasi. Istilah tersebut masuk akal hanya dalam konteks dimana identitas yang disajikan oleh permintaan dikenali, dan jadi, dimana verifikasi dimungkinkan. Jika identitas yang disajikan tidak sesuai dengan opsi yang diberikan di atas, atau jika tidak ada identitas yang disajikan, opsi yang diberikan di atas menjadi tidak relevan.

__Apa itu "bypass satu pelanggaran"?__ Dalam beberapa kasus, permintaan diverifikasi secara positif mungkin masih diblokir sebagai akibat dari file tanda tangan, modul, atau kondisi permintaan lainnya, dan bypass mungkin diperlukan untuk menghindari positif palsu. Dalam kasus dimana bypass dimaksudkan untuk menangani tepat satu pelanggaran, tidak lebih dan tidak kurang, bypass seperti itu dapat digambarkan sebagai "bypass satu pelanggaran".

* Opsi ini memiliki bypass terkait dibawah `bypasses➡used`. Direkomendasikan untuk memastikan bahwa kotak centang untuk bypass terkait ditandai dengan cara yang sama seperti kotak centang untuk mencoba memverifikasi opsi ini.

!! Mayoritas pengguna mungkin ingin ini diblokir, terlepas dari apakah itu asli atau dipalsukan. Ini dapat dicapai dengan tidak memilih "mencoba memverifikasi" dan pilih "blokir permintaan yang tidak diverifikasi". Namun, karena beberapa pengguna mungkin ingin dapat memverifikasi permintaan semacam ini (untuk memblokir permintaan negatif sambil mengizinkan permintaan positif), alih-alih memblokir permintaan tersebut melalui modul, opsi untuk menangani permintaan tersebut disediakan disini.

##### "adjust" `[string]`
- Kontrol untuk menyesuaikan fitur lain saat dalam konteks verifikasi.

```
adjust
├─Negatives ("Negatif yang diblokir")
└─NonVerified ("Tidak diverifikasi yang diblokir")
```

#### "recaptcha" (Kategori)
Konfigurasi untuk reCAPTCHA (menyediakan cara bagi manusia untuk mendapatkan kembali akses ketika diblokir).

##### "usemode" `[int]`
- Kapan CAPTCHA harus ditawarkan? Catat: Permintaan yang masuk daftar putih atau diverifikasi dan tidak diblokir tidak perlu menyelesaikan CAPTCHA. Juga mencatat: CAPTCHA dapat memberikan lapisan perlindungan tambahan yang berguna terhadap bot dan berbagai jenis permintaan yang otomatis dan berbahaya, tetapi tidak akan memberikan perlindungan apapun terhadap manusia yang berbahaya.

```
usemode
├─0 (Tak pernah !!!)
├─1 (Hanya jika diblokir, dalam batas tanda tangan, dan tidak dilarang.)
├─2 (Hanya jika diblokir, ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.)
├─3 (Hanya jika dalam batas tanda tangan, dan tidak dilarang (terlepas dari apakah diblokir).)
├─4 (Hanya jika tidak diblokir.)
├─5 (Hanya jika tidak diblokir, atau jika ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.)
└─6 (Hanya jika tidak diblokir, pada permintaan halaman sensitif.)
```

##### "lockip" `[bool]`
- Kunci CAPTCHA ke IP?

##### "lockuser" `[bool]`
- Kunci CAPTCHA ke pengguna?

##### "sitekey" `[string]`
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

Lihat juga:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)

##### "secret" `[string]`
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

Lihat juga:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)

##### "expiry" `[float]`
- Jumlah jam untuk mengingat instansi CAPTCHA. Default = 720 (1 bulan).

##### "recaptcha_log" `[string]`
- Mencatat hasil semua instansi CAPTCHA? Jika ya, tentukan nama untuk menggunakan untuk file pencatatan. Jika tidak, variabel ini harus kosong.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- Jumlah maksimum tanda tangan yang diperbolehkan sebelum penawaran CAPTCHA ditarik. Default = 1.

##### "api" `[string]`
- API mana yang akan digunakan?

```
api
├─v2 ("v2 (Kotak centang)")
└─Invisible ("v2 (Tak terlihat)")
```

##### "show_cookie_warning" `[bool]`
- Tampilkan peringatan cookie? True = Ya [Default]; False = Tidak.

##### "show_api_message" `[bool]`
- Tampilkan pesan API? True = Ya [Default]; False = Tidak.

##### "nonblocked_status_code" `[int]`
- Kode status mana yang harus digunakan saat menampilkan CAPTCHA ke permintaan yang tidak diblokir?

```
nonblocked_status_code
├─200 (200 OK): Paling tidak kuat, tetapi paling ramah-pengguna. Permintaan otomatis
│ kemungkinan besar akan menafsirkan respons ini sebagai indikasi bahwa
│ permintaan berhasil.
├─403 (403 Forbidden (Terlarang)): Lebih kuat, tetapi kurang ramah-pengguna. Direkomendasikan untuk kebanyakan
│ keadaan umum.
├─418 (418 I'm a teapot (Saya adalah teko)): Referensi pada lelucon April Mop (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Probabilitas rendah bahwa
│ akan dipahami oleh klien, bot, browser, atau lainnya. Disediakan untuk
│ hiburan dan kenyamanan, tetapi umumnya tidak direkomendasikan.
├─429 (429 Too Many Requests (Terlalu Banyak Permintaan)): Direkomendasikan untuk pembatasan laju, saat menangani serangan DDoS, dan
│ untuk pencegahan banjir. Tidak direkomendasikan dalam konteks lain.
└─451 (451 Unavailable For Legal Reasons (Tidak tersedia karena alasan hukum)): Direkomendasikan saat memblokir terutama karena alasan hukum. Tidak
  direkomendasikan dalam konteks lain.
```

#### "hcaptcha" (Kategori)
Konfigurasi untuk hCaptcha (menyediakan cara bagi manusia untuk mendapatkan kembali akses ketika diblokir).

##### "usemode" `[int]`
- Kapan CAPTCHA harus ditawarkan? Catat: Permintaan yang masuk daftar putih atau diverifikasi dan tidak diblokir tidak perlu menyelesaikan CAPTCHA. Juga mencatat: CAPTCHA dapat memberikan lapisan perlindungan tambahan yang berguna terhadap bot dan berbagai jenis permintaan yang otomatis dan berbahaya, tetapi tidak akan memberikan perlindungan apapun terhadap manusia yang berbahaya.

```
usemode
├─0 (Tak pernah !!!)
├─1 (Hanya jika diblokir, dalam batas tanda tangan, dan tidak dilarang.)
├─2 (Hanya jika diblokir, ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.)
├─3 (Hanya jika dalam batas tanda tangan, dan tidak dilarang (terlepas dari apakah diblokir).)
├─4 (Hanya jika tidak diblokir.)
├─5 (Hanya jika tidak diblokir, atau jika ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.)
└─6 (Hanya jika tidak diblokir, pada permintaan halaman sensitif.)
```

##### "lockip" `[bool]`
- Kunci CAPTCHA ke IP?

##### "lockuser" `[bool]`
- Kunci CAPTCHA ke pengguna?

##### "sitekey" `[string]`
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

Lihat juga:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

Lihat juga:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Jumlah jam untuk mengingat instansi CAPTCHA. Default = 720 (1 bulan).

##### "hcaptcha_log" `[string]`
- Mencatat hasil semua instansi CAPTCHA? Jika ya, tentukan nama untuk menggunakan untuk file pencatatan. Jika tidak, variabel ini harus kosong.

Kiat yang berguna: Anda dapat melampirkan informasi tanggal/waktu ke nama file log dengan menggunakan placeholder format waktu. Placeholder format waktu yang tersedia ditampilkan di <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- Jumlah maksimum tanda tangan yang diperbolehkan sebelum penawaran CAPTCHA ditarik. Default = 1.

##### "api" `[string]`
- API mana yang akan digunakan?

```
api
├─v1 ("v1")
└─Invisible ("v1 (Tak terlihat)")
```

##### "show_cookie_warning" `[bool]`
- Tampilkan peringatan cookie? True = Ya [Default]; False = Tidak.

##### "show_api_message" `[bool]`
- Tampilkan pesan API? True = Ya [Default]; False = Tidak.

##### "nonblocked_status_code" `[int]`
- Kode status mana yang harus digunakan saat menampilkan CAPTCHA ke permintaan yang tidak diblokir?

```
nonblocked_status_code
├─200 (200 OK): Paling tidak kuat, tetapi paling ramah-pengguna. Permintaan otomatis
│ kemungkinan besar akan menafsirkan respons ini sebagai indikasi bahwa
│ permintaan berhasil.
├─403 (403 Forbidden (Terlarang)): Lebih kuat, tetapi kurang ramah-pengguna. Direkomendasikan untuk kebanyakan
│ keadaan umum.
├─418 (418 I'm a teapot (Saya adalah teko)): Referensi pada lelucon April Mop (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Probabilitas rendah bahwa
│ akan dipahami oleh klien, bot, browser, atau lainnya. Disediakan untuk
│ hiburan dan kenyamanan, tetapi umumnya tidak direkomendasikan.
├─429 (429 Too Many Requests (Terlalu Banyak Permintaan)): Direkomendasikan untuk pembatasan laju, saat menangani serangan DDoS, dan
│ untuk pencegahan banjir. Tidak direkomendasikan dalam konteks lain.
└─451 (451 Unavailable For Legal Reasons (Tidak tersedia karena alasan hukum)): Direkomendasikan saat memblokir terutama karena alasan hukum. Tidak
  direkomendasikan dalam konteks lain.
```

#### "legal" (Kategori)
Konfigurasi untuk persyaratan hukum.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonimisasikan alamat IP saat menulis file log? True = Ya [Default]; False = Tidak.

##### "privacy_policy" `[string]`
- Alamat dari kebijakan privasi yang relevan untuk ditampilkan di footer dari setiap halaman yang dihasilkan. Spesifikasikan URL, atau biarkan kosong untuk menonaktifkan.

#### "template_data" (Kategori)
Konfigurasi untuk template dan tema.

##### "theme" `[string]`
- Tema yang akan digunakan untuk acara blokir dan permintaan CAPTCHA.

```
theme
├─default ("Default")
├─bluemetal ("Blue Metal")
├─fullmoon ("Full Moon")
├─moss ("Moss")
├─primer ("Primer")
├─primerdark ("Primer Dark")
├─rbi ("Red-Blue Inverted")
├─slate ("Slate")
└─…Lain
```

##### "theme_mode" `[string]`
- Mode untuk tema yang akan digunakan untuk acara blokir dan permintaan CAPTCHA.

```
theme_mode
├─normal ("Normal")
└─inverted ("Terbalik")
```

##### "magnification" `[float]`
- Perbesaran font. Default = 1.

##### "css_url" `[string]`
- URL file CSS untuk tema kustom.

##### "block_event_title" `[string]`
- Judul halaman yang akan ditampilkan untuk acara blokir.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Akses ditolak!")
└─…Lain
```

##### "captcha_title" `[string]`
- Judul halaman yang akan ditampilkan untuk permintaan CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Lain
```

##### "custom_header" `[string]`
- Disisipkan sebagai HTML di awal semua halaman "akses ditolak". Ini dapat berguna jika Anda ingin menyertakan logo situs web, header yang dipersonalisasi, skrip, atau sejenisnya di semua halaman tersebut.

##### "custom_footer" `[string]`
- Disisipkan sebagai HTML di akhir semua halaman "akses ditolak". Ini dapat berguna jika Anda ingin menyertakan pemberitahuan hukum, tautan kontak, informasi bisnis, atau sejenisnya di semua halaman tersebut.

#### "rate_limiting" (Kategori)
Konfigurasi untuk pembatasan laju (tidak direkomendasikan untuk penggunaan umum).

Perlu diingat bahwa seperti halnya semua fitur CIDRAM lainnya, fitur pembatasan laju CIDRAM hanya dapat diterapkan untuk halaman dan sumber daya yang terhubung dengan CIDRAM. Ini biasanya berarti bahwa sumber daya yang bukan PHP tidak akan dicakup kecuali jika secara eksplisit dilayani oleh sumber daya PHP yang terhubung. Jika Anda dapat menggunakan modul server, cPanel, atau alat jaringan lain untuk menerapkan pembatasan laju, akan lebih baik menggunakannya daripada fitur pembatasan laju CIDRAM. Perlu diingat juga bahwa pengguna yang sangat bertekad dapat dengan mudah menghindari pembatasan laju dengan memutar alamat IP mereka, atau dengan beralih ke penyedia proxy atau VPN yang belum diketahui oleh CIDRAM, dan perlu diingat bahwa pembatasan laju bisa sangat mengganggu bagi pengguna akhir. Kadang-kadang hal itu mungkin diperlukan, tetapi jarang diinginkan.

##### "max_bandwidth" `[string]`
- Jumlah maksimum bandwidth yang diizinkan dalam periode tunjangan sebelum mengaktifkan pembatasan laju untuk permintaan di masa mendatang. Nilai 0 menonaktifkan jenis pembatasan laju ini. Default = 0KB.

##### "max_requests" `[int]`
- Jumlah maksimum permintaan yang diizinkan dalam periode tunjangan sebelum mengaktifkan pembatasan laju untuk permintaan di masa mendatang. Nilai 0 menonaktifkan jenis pembatasan laju ini. Default = 0.

##### "precision_ipv4" `[int]`
- Presisi yang akan digunakan saat melacak penggunaan IPv4. Nilai mencerminkan ukuran blok CIDR. Atur ke 32 untuk presisi terbaik. Default = 32.

##### "precision_ipv6" `[int]`
- Presisi yang akan digunakan saat melacak penggunaan IPv6. Nilai mencerminkan ukuran blok CIDR. Atur ke 128 untuk presisi terbaik. Default = 128.

##### "allowance_period" `[string]`
- Durasi untuk melacak penggunaan. Default = 0°0′0″.

##### "exceptions" `[string]`
- Pengecualian (yaitu, permintaan yang seharusnya tidak dibatasi). Hanya relevan ketika pembatasan laju diaktifkan.

```
exceptions
├─Whitelisted ("Permintaan yang masuk daftar putih")
├─Verified ("Permintaan yang diverifikasi dari mesin pencari dan media sosial")
└─FE ("Permintaan ke bagian depan CIDRAM")
```

##### "segregate" `[bool]`
- Haruskah kuota untuk domain dan host yang berbeda dipisahkan atau dibagikan? True = Kuota akan dipisahkan. False = Kuota akan dibagikan [Default].

#### "supplementary_cache_options" (Kategori)
Opsi cache tambahan. Catat: Mengubah nilai ini berpotensi membuat Anda keluar.

##### "prefix" `[string]`
- Nilai yang ditentukan disini akan ditambahkan ke awal kunci untuk semua entri di cache. Default = "CIDRAM_". Ketika beberapa instalasi ada di server, ini dapat berguna untuk menjaga cache mereka terpisah.

##### "enable_apcu" `[bool]`
- Menentukan apakah akan mencoba menggunakan APCu untuk cache. Default = True.

##### "enable_memcached" `[bool]`
- Menentukan apakah akan mencoba menggunakan Memcached untuk cache. Default = False.

##### "enable_redis" `[bool]`
- Menentukan apakah akan mencoba menggunakan Redis untuk cache. Default = False.

##### "enable_pdo" `[bool]`
- Menentukan apakah akan mencoba menggunakan PDO untuk cache. Default = False.

##### "memcached_host" `[string]`
- Nilai host Memcached. Default = localhost.

##### "memcached_port" `[int]`
- Nilai port Memcached. Default = "11211".

##### "redis_host" `[string]`
- Nilai host Redis. Default = localhost.

##### "redis_port" `[int]`
- Nilai port Redis. Default = "6379".

##### "redis_timeout" `[float]`
- Nilai batas waktu Redis. Default = "2.5".

##### "redis_database_number" `[int]`
- Nomor basis data Redis. Default = 0. Catat: Tidak dapat menggunakan nilai selain 0 dengan Redis Cluster.

##### "pdo_dsn" `[string]`
- Nilai DSN PDO. Default = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.id.md#user-content-HOW_TO_USE_PDO" hreflang="id-ID">Apa itu "PDO DSN"? Bagaimana saya bisa menggunakan PDO dengan CIDRAM?</a>*

##### "pdo_username" `[string]`
- Nama pengguna PDO.

##### "pdo_password" `[string]`
- Kata sandi PDO.

#### "bypasses" (Kategori)
Konfigurasi untuk bypass tanda tangan default.

##### "used" `[string]`
- Bypass mana yang harus digunakan?

```
used
├─AbuseIPDB ("AbuseIPDB")
├─AmazonAdBot ("AmazonAdBot")
├─Baidu ("Baiduspider/百度")
├─Bingbot ("Bingbot")
├─DuckDuckBot ("DuckDuckBot")
├─Embedly ("Embedly")
├─Feedbot ("Feedbot")
├─Feedspot ("Feedspot")
├─GoogleFiber ("Google Fiber")
├─Googlebot ("Googlebot")
├─Jetpack ("Jetpack")
├─PetalBot ("PetalBot")
├─Pinterest ("Pinterest")
├─Redditbot ("Redditbot")
├─Snapchat ("Snapchat")
├─Sogou ("Sogou/搜狗")
└─Yandex ("Yandex/Яндекс")
```

---


### 6. <a name="SECTION6"></a>FORMAT TANDA TANGAN

*Lihat juga:*
- *[Apa yang "tanda tangan"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 DASAR-DASAR (UNTUK FILE TANDA TANGAN)

Semua tanda tangan IPv4 mengikuti format: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` merupakan awal dari blok CIDR (oktet dari alamat IP pertama dalam blok).
- `yy` merupakan ukuran dari blok CIDR [1-32].
- `[Function]` menginstruksikan skrip apa yang harus dilakukan dengan tanda tangan (bagaimana tanda tangan harus dianggap).
- `[Param]` merupakan apapun informasi tambahan mungkin diperlukan oleh `[Function]`.

Semua tanda tangan IPv6 mengikuti format: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` merupakan awal dari blok CIDR (oktet dari alamat IP pertama dalam blok). Notasi lengkap dan notasi disingkat keduanya diterima (dan masing-masing HARUS mengikuti standar tepat dan relevan dari notasi IPv6, tapi dengan satu pengecualian: alamat IPv6 tidak pernah dapat dimulai dengan singkatan bila digunakan dalam tanda tangan untuk skrip ini, karena cara dimana CIDR-CIDR direkonstruksi oleh skrip ini; Sebagai contoh, `::1/128` harus diungkapkan, bila digunakan dalam tanda tangan, sebagai `0::1/128`, dan `::0/128` diungkapkan sebagai `0::/128`).
- `yy` merupakan ukuran dari blok CIDR [1-128].
- `[Function]` menginstruksikan skrip apa yang harus dilakukan dengan tanda tangan (bagaimana tanda tangan harus dianggap).
- `[Param]` merupakan apapun informasi tambahan mungkin diperlukan oleh `[Function]`.

Jeda baris yang gaya Unix (`%0A`, or `\n`) DIREKOMENDASIKAN untuk file tanda tangan dalam CIDRAM. Jenis/Gaya lain (misalnya, jeda baris yang gaya Windows `%0D%0A` atau `\r\n`, jeda baris yang gaya Mac `%0D` atau `\r`, dll) MUNGKIN digunakan, tapi TIDAK disukai. Setiap jeda baris yang tidak gaya Unix akan dinormalisasi untuk jeda baris yang gaya unix oleh skrip ini.

Notasi CIDR tepat dan benar diperlukan; Jika tidak digunakan, skrip TIDAK akan mengenali tanda tangan. Selain itu, semua tanda tangan CIDR dari skrip ini HARUS dimulai dengan alamat IP yang nomor IP dapat membagi secara merata ke divisi blok diwakili oleh ukuran dari blok CIDR-nya (misalnya, jika Anda ingin memblokir semua IP dari `10.128.0.0` ke `11.127.255.255`, `10.128.0.0/8` akan TIDAK diakui oleh skrip ini, tapi `10.128.0.0/9` dan `11.0.0.0/9` digunakan bersama, AKAN diakui oleh skrip ini).

Apapun dalam file tanda tangan tidak diakui sebagai tanda tangan atau sebagai sintaks terkait tanda tangan oleh skrip ini akan DIABAIKAN, oleh karena itu berarti Anda dapat dengan aman menempatkan setiap data lain yang Anda inginkan ke dalam file tanda tangan tanpa melanggar mereka dan tanpa melanggar skrip. Komentar yang diterima dalam file tanda tangan, dan tidak ada format khusus diperlukan untuk mereka. Hash yang gaya Shell untuk komentar lebih disukai, tapi tidak ditegakkan; Fungsional, tidak ada bedanya untuk skrip apakah Anda memilih menggunakan hash gaya Shell untuk komentar, tapi menggunakan hash yang gaya Shell membantu IDE dan editor teks biasa untuk benar menyoroti berbagai bagian dari file tanda tangan (dan sebagainya, hash yang gaya Shell dapat membantu sebagai bantuan visual saat mengedit).

Kemungkinan nilai-nilai `[Function]` adalah sebagai berikut:
- Run
- Whitelist
- Greylist
- Deny

Jika "Run" digunakan, ketika tanda tangan dipicu, skrip akan mencoba untuk mengeksekusi (menggunakan `require_once` pernyataan) eksternal skrip PHP, ditentukan oleh nilai dari `[Param]` (direktori kerja harus direktori "/vault/" skrip ini).

Contoh: `127.0.0.0/8 Run example.php`

Hal ini dapat berguna jika Anda ingin mengeksekusi beberapa kode PHP yang spesifik untuk beberapa IP dan/atau CIDR tertentu.

Jika "Whitelist" digunakan, ketika tanda tangan dipicu, skrip akan mengatur ulang semua pendeteksian (jika sudah ada setiap pendeteksian) dan istirahat fungsi tes. `[Param]` diabaikan. Fungsi ini setara dengan membolehkan akses untuk IP tertentu atau CIDR.

Contoh: `127.0.0.1/32 Whitelist`

Jika "Greylist" digunakan, ketika tanda tangan dipicu, skrip akan mengatur ulang semua pendeteksian (jika sudah ada setiap pendeteksian) dan melompat ke file tanda tangan berikutnya untuk melanjutkan proses. `[Param]` diabaikan.

Contoh: `127.0.0.1/32 Greylist`

Jika "Deny" digunakan, ketika tanda tangan dipicu, dengan asumsi tidak ada tanda tangan daftar putih telah memicu untuk alamat IP yang diberikan dan/atau CIDR yang diberikan, akses ke halaman dilindungi akan ditolak. "Deny" adalah apa yang akan Anda ingin menggunakan untuk benar-benar memblokir alamat IP dan/atau CIDR. Ketika setiap tanda tangan dipicu yang memanfaatkan "Deny", halaman skrip "Akses Ditolak" akan dihasilkan dan permintaan untuk halaman dilindungi akan dihentikan.

Nilai `[Param]` diterima oleh "Deny" akan diurai ke output halaman "Akses Ditolak", dipasok ke klien/pengguna sebagai alasan dikutip untuk akses mereka ke halaman yang diminta ditolak. Ini bisa menjadi kalimat pendek dan sederhana, menjelaskan mengapa Anda memilih untuk memblokir mereka (apapun harus cukup, bahkan pesan sederhana "Saya tidak ingin Anda di website saya"), atau satu dari segelintir kecil kata-kata pendek disediakan oleh skrip, bahwa jika digunakan, akan digantikan oleh skrip dengan penjelasan pra-siap mengapa klien/pengguna diblokir.

Penjelasan pra-siap memiliki dukungan L10N dan dapat diterjemahkan oleh skrip berdasarkan bahasa yang Anda tentukan untuk direktif `lang` dari konfigurasi skrip. Selain itu, Anda dapat menginstruksikan skrip untuk mengabaikan tanda tangan "Deny" berdasarkan mereka nilai dari `[Param]` (jika mereka menggunakan kata-kata singkat) melalui direktif-direktif yang ditentukan oleh konfigurasi skrip (setiap kata singkat memiliki direktif yang sesuai untuk memproses sesuai tanda tangan atau mengabaikannya). Nilai dari `[Param]` yang tidak menggunakan kata-kata singkat, namun, tidak memiliki dukungan L10N dan karena itu TIDAK akan diterjemahkan oleh skrip ini, dan tambahan, tidak bisa langsung dikontrol oleh konfigurasi skrip.

Kata-kata singkat yang tersedia adalah:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 TAG

##### 6.1.0 TAG BAGIAN

Jika Anda ingin membagi tanda tangan kustom Anda ke bagian individual, Anda dapat mengidentifikasi bagian individual untuk skrip dengan menambahkan "tag bagian" segera setelah tanda tangan dari setiap bagian, bersama dengan nama bagian tanda tangan Anda (lihat contoh dibawah ini).

```
# Bagian 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Bagian 1
```

Untuk mematahkan tag bagian dan untuk memastikan bahwa tag tidak salah mengidentifikasi untuk bagian tanda tangan dari sebelumnya dalam file tanda tangan, hanya memastikan bahwa setidaknya ada dua jeda baris berturut-turut antara tag Anda dan bagian tanda tangan sebelumnya Anda. Apapun tanda tangan tidak di-tag akan default untuk "IPv4" atau "IPv6" (tergantung pada jenis tanda tangan yang dipicu).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Bagian 1
```

Dalam contoh di atas `1.2.3.4/32` dan `2.3.4.5/32` akan di-tag sebagai "IPv4", sedangkan `4.5.6.7/32` dan `5.6.7.8/32` akan di-tag sebagai "Bagian 1".

Logika sama ini dapat diterapkan untuk memisahkan jenis tag lainnya juga.

Secara khusus, tag bagian bisa sangat berguna untuk debugging bila terjadi positif palsu, dengan menyediakan sarana mudah untuk menemukan sumber masalah yang tepat, dan bisa sangat berguna untuk menyaring entri file log saat melihat file log melalui halaman log depan (nama bagian dapat diklik melalui halaman log depan dan dapat digunakan sebagai kriteria penyaringan). Jika tag bagian diabaikan untuk beberapa tanda tangan tertentu, saat tanda tangan dipicu, CIDRAM menggunakan nama file tanda tangan beserta jenis alamat IP yang diblokir (IPv4 atau IPv6) sebagai fallback, dan demikian, tag bagian sepenuhnya opsional. Mereka mungkin akan merekomendasikan dalam beberapa kasus meskipun, seperti ketika file tanda tangan diberi nama samar-samar atau bila mungkin sulit untuk secara jelas mengidentifikasi sumber tanda tangan yang menyebabkan permintaan diblokir.

##### 6.1.1 TAG KADALUARSA

Jika Anda ingin tanda tangan untuk berakhir setelah beberapa waktu, dengan cara yang sama untuk tag bagian, Anda dapat menggunakan "tag kadaluarsa" untuk menentukan kapan tanda tangan harus berhenti menjadi valid. Tag kadaluarsa menggunakan format "TTTT.BB.HH" (lihat contoh dibawah ini).

```
# Bagian 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Tanda tangan kadaluarsa tidak akan pernah dipicu pada permintaan apapun, tidak masalah apa.

##### 6.1.2 TAG ASAL

Jika Anda ingin menentukan negara asal untuk beberapa tanda tangan tertentu, Anda dapat melakukannya dengan menggunakan "tag asal". Tag asal menerima kode "[ISO 3166-1 Alpha-2](https://id.wikipedia.org/wiki/ISO_3166-1)" yang sesuai dengan negara asal untuk tanda tangan yang berlaku. Kode ini harus ditulis dalam huruf besar (huruf kecil atau huruf campuran tidak akan ditampilkan dengan benar). Saat tag asal digunakan, ditambahkan ke entri lapangan log "Mengapa Diblokir" untuk setiap permintaan yang diblokir akibat tanda tangan yang diterapkan tag.

Jika komponen "flags CSS" opsional diinstal, saat melihat logfile melalui halaman log depan, informasi yang ditambahkan oleh tag asal akan diganti dengan bendera negara yang sesuai dengan informasi tersebut. Informasi ini, apakah dalam bentuk mentah atau sebagai bendera negara, dapat diklik, dan saat diklik, akan menyaring entri log dengan cara entri serupa lainnya (secara efektif membiarkan mereka mengakses halaman log untuk menyaring dengan cara negara asal).

Catat: Secara teknis, ini bukan geolokasi, karena ini tidak melibatkan pencarian informasi spesifik terkait dengan IP, namun hanya memungkinkan kita untuk secara eksplisit menyatakan negara asal untuk setiap permintaan yang diblokir oleh tanda tangan tertentu. Lebih dari satu tag asal diperbolehkan di bagian tanda tangan sama.

Contoh hipotetis:

```
1.2.3.4/32 Deny Generic
Origin: CN
2.3.4.5/32 Deny Generic
Origin: FR
4.5.6.7/32 Deny Generic
Origin: DE
6.7.8.9/32 Deny Generic
Origin: US
Tag: Foobar
```

Tag apapun dapat digunakan bersamaan, dan semua tag bersifat opsional (lihat contoh dibawah ini).

```
# Contoh Bagian.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Contoh Bagian
Expires: 2016.12.31
```

##### 6.1.3 TAG PENANGGUH

Ketika sejumlah besar file tanda tangan diinstal dan aktif digunakan, instalasi bisa menjadi sangat kompleks, dan mungkin ada beberapa tanda tangan yang tumpang tindih. Dalam kasus ini, untuk mencegah banyak tanda tangan tumpang tindih dipicu selama kejadian blokir, tag penangguh dapat digunakan untuk menangguhkan bagian tanda tangan tertentu dalam kasus dimana beberapa file tanda tangan khusus lainnya diinstal dan aktif digunakan. Ini mungkin berguna jika beberapa tanda tangan diperbarui lebih sering daripada yang lain, untuk menangguhkan tanda tangan yang kurang sering diperbarui untuk mendukung tanda tangan yang lebih sering diperbarui.

Tag penangguh digunakan serupa dengan jenis tag lainnya. Nilai tag harus cocok dengan file tanda tangan yang diinstal dan aktif digunakan untuk ditangguhkan.

Contoh:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 TAG PROFIL

Tag profil menyediakan sarana untuk menampilkan informasi tambahan di halaman pengujian IP, dan dapat dimanfaatkan oleh modul dan aturan tambahan untuk perilaku yang lebih kompleks dan pengambilan keputusan yang lebih baik.

Tag profil digunakan serupa dengan jenis tag lainnya. Nilai untuk tag profil dapat digunakan sebagai kondisi untuk modul dan aturan tambahan. Tag profil dapat memberikan beberapa nilai dengan memisahkan nilai tersebut dengan titik koma. Pengguna tidak pernah melihat nilai untuk tag profil.

Contoh:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 DASAR-DASAR YAML

Sebuah bentuk sederhana YAML markup dapat digunakan dalam file tanda tangan untuk tujuan perilaku mendefinisikan dan direktif spesifik untuk bagian tanda tangan individu. Ini mungkin berguna jika Anda ingin nilai direktif konfigurasi berbeda atas dasar tanda tangan individu dan bagian tanda tangan (sebagai contoh; jika Anda ingin memberikan alamat email untuk tiket dukungan untuk setiap pengguna diblokir oleh satu tanda tangan tertentu, tapi tidak ingin memberikan alamat email untuk tiket dukungan untuk pengguna diblokir oleh tanda tangan lain; jika Anda ingin beberapa tanda tangan spesifik untuk memicu halaman redireksi; jika Anda ingin menandai bagian tanda tangan untuk digunakan dengan reCAPTCHA/hCaptcha; jika Anda ingin merekam diblokir upaya akses untuk memisahkan file berdasarkan tanda tangan individu dan/atau bagian tanda tangan).

Penggunaan YAML markup dalam file tanda tangan sepenuhnya opsional (yaitu, Anda dapat menggunakannya jika Anda ingin melakukannya, tapi Anda tidak diharuskan untuk melakukannya), dan mampu memanfaatkan kebanyakan (tapi tidak semua) direktif konfigurasi.

Catat: Implementasi markup YAML di CIDRAM sangat sederhana dan sangat terbatas; Hal ini dimaksudkan untuk memenuhi kebutuhan spesifik untuk CIDRAM dengan cara yang memiliki keakraban dari YAML markup, tapi tidak mengikuti dengan spesifikasi resmi (dan karena itu tidak akan berperilaku dalam cara sama seperti implementasi yang lebih menyeluruh di tempat lain, dan mungkin tidak sesuai untuk proyek-proyek lain di tempat lain).

Dalam CIDRAM, segmen markup YAML diidentifikasi untuk skrip oleh tiga tanda hubung ("---"), dan mengakhiri dengan mengandung bagian tanda tangan mereka oleh dua jeda baris. Segmen markup YAML dalam bagian tanda tangan terdiri dari tiga tanda hubung pada baris segera setelah daftar CIDRs dan apapun tag, diikuti dengan daftar dua dimensi dari pasangan kunci-nilai (dimensi pertama, kategori direktif konfigurasi; dimensi kedua, direktif konfigurasi) untuk mana direktif konfigurasi yang harus dimodifikasi (dan yang nilai-nilai) setiap kali tanda tangan dalam yang bagian tanda tangan dipicu (lihat contoh dibawah ini).

```
# Foobar 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 1
---
general:
 http_response_header_code: 403
 emailaddr: username@domain.tld
logging:
 standard_log: "logfile.{yyyy}-{mm}-{dd}.txt"
 apache_style_log: "access.{yyyy}-{mm}-{dd}.txt"
 serialised_log: "serial.{yyyy}-{mm}-{dd}.txt"
recaptcha:
 lockip: false
 lockuser: true
 expiry: 720
 recaptcha_log: "recaptcha.{yyyy}-{mm}-{dd}.txt"
 enabled: true
template_data:
 css_url: "https://domain.tld/cidram.css"

# Foobar 2.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 2
---
general:
 http_response_header_code: 503
logging:
 standard_log: "logfile.Foobar2.{yyyy}-{mm}-{dd}.txt"
 apache_style_log: "access.Foobar2.{yyyy}-{mm}-{dd}.txt"
 serialised_log: "serial.Foobar2.{yyyy}-{mm}-{dd}.txt"

# Foobar 3.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 3
---
general:
 http_response_header_code: 403
 silent_mode: "http://127.0.0.1/"
```

##### 6.2.1 BAGAIMANA "KHUSUS MENANDAI" BAGIAN TANDA TANGAN UNTUK DIGUNAKAN DENGAN reCAPTCHA/hCaptcha

Ketika "usemode" 2 atau 5, untuk "khusus menandai" bagian tanda tangan untuk digunakan dengan reCAPTCHA/hCaptcha, entri termasuk dalam segmen YAML untuk bagian tanda tangan (lihat contoh dibawah ini).

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Tag: CAPTCHA Marked
---
recaptcha:
 enabled: true
hcaptcha:
 enabled: true
```

#### 6.3 INFORMASI TAMBAHAN

##### 6.3.0 MENGABAIKAN BAGIAN TANDA TANGAN

Juga, jika Anda ingin CIDRAM untuk sama sekali mengabaikan beberapa bagian tertentu dalam salah satu file tanda tangan, Anda dapat menggunakan file `ignore.dat` untuk menentukan bagian untuk mengabaikan. Pada baris baru, menulis `Ignore`, diikuti dengan spasi, diikuti dengan nama bagian yang Anda ingin CIDRAM untuk mengabaikan (lihat contoh dibawah ini).

```
Ignore Bagian 1
```

Ini juga dapat dicapai dengan menggunakan antarmuka yang disediakan oleh halaman "daftar bagian" dari bagian depan CIDRAM.

##### 6.3.1 ATURAN TAMBAHAN

Jika Anda merasa bahwa menulis file tanda tangan atau modul kustom Anda sendiri terlalu rumit untuk Anda, alternatif yang lebih sederhana mungkin menggunakan antarmuka yang disediakan oleh halaman "aturan tambahan" dari bagian depan CIDRAM. Dengan memilih opsi yang sesuai dan menentukan detail tentang jenis permintaan spesifik, Anda dapat menginstruksikan CIDRAM cara menanggapi permintaan tersebut. "Aturan tambahan" dijalankan setelah semua file tanda tangan dan modul telah selesai dijalankan.

#### 6.4 <a name="MODULE_BASICS"></a>DASAR-DASAR (UNTUK MODUL)

Modul dapat digunakan untuk memperluas fungsionalitas CIDRAM, melakukan tugas tambahan, atau memproses logika tambahan.

Karena modul ditulis sebagai file PHP, jika Anda cukup mengenal basis kode CIDRAM, Anda dapat menyusun modul Anda namun Anda inginkan, dan menulis tanda tangan modul Anda namun Anda inginkan (dalam batasan untuk apa yang mungkin di PHP).

*Catat: Jika Anda tidak nyaman bekerja dengan kode PHP, menulis modul Anda sendiri tidak disarankan.*

Beberapa fungsi disediakan oleh CIDRAM yang dapat digunakan oleh modul, yang seharusnya membuatnya lebih sederhana dan mudah untuk menulis modul Anda sendiri. Informasi tentang fungsi ini dijelaskan dibawah ini.

#### 6.5 FUNGSIONALITAS MODUL

##### 6.5.0 "$this->trigger"

Tanda tangan modul biasanya ditulis dengan `$this->trigger`. Dalam kebanyakan kasus, method ini akan lebih penting daripada hal lain untuk tujuan penulisan modul.

`$this->trigger` menerima 4 parameter: `$Condition`, `$ReasonShort`, `$ReasonLong` (opsional), dan `$DefineOptions` (opsional).

Kebenaran dari `$Condition` dievaluasi, dan jika true/benar, tanda tangan "dipicu". Jika false/salah, tanda tangan *tidak* "dipicu". `$Condition` biasanya berisi kode PHP untuk mengevaluasi suatu kondisi yang harus menyebabkan permintaan diblokir.

`$ReasonShort` dikutip di bidang "Mengapa Diblokir" saat tanda tangan "dipicu".

`$ReasonLong` adalah pesan opsional yang akan ditampilkan kepada pengguna/klien saat mereka diblokir, untuk menjelaskan mengapa mereka diblokir. Default ke pesan "Akses Ditolak" standar saat dihilangkan.

`$DefineOptions` adalah array opsional yang berisi pasangan kunci/nilai, digunakan untuk menentukan opsi konfigurasi yang spesifik untuk instance permintaan. Opsi konfigurasi akan diterapkan saat tanda tangan "dipicu".

`$this->trigger` kembali true/benar saat tanda tangan "dipicu", dan false/salah saat tidak.

##### 6.5.1 "$this->bypass"

Tanda tangan bypass biasanya ditulis dengan `$this->bypass`.

`$this->bypass` menerima 3 parameter: `$Condition`, `$ReasonShort`, dan `$DefineOptions` (opsional).

Kebenaran dari `$Condition` dievaluasi, dan jika true/benar, bypass "dipicu". Jika false/salah, bypass *tidak* "dipicu". `$Condition` biasanya berisi kode PHP untuk mengevaluasi suatu kondisi yang harus *tidak* menyebabkan permintaan diblokir.

`$ReasonShort` dikutip di bidang "Mengapa Diblokir" saat bypass "dipicu".

`$DefineOptions` adalah array opsional yang berisi pasangan kunci/nilai, digunakan untuk menentukan opsi konfigurasi yang spesifik untuk instance permintaan. Opsi konfigurasi akan diterapkan saat bypass "dipicu".

`$this->bypass` kembali true/benar saat bypass "dipicu", dan false/salah saat tidak.

##### 6.5.2 "$this->dnsReverse"

Ini bisa digunakan untuk mengambil nama host dari alamat IP. Jika Anda ingin membuat modul untuk memblokir nama host, method ini bisa bermanfaat.

Contoh:
```PHP
<?php
/** Fetch hostname. */
if (empty($this->CIDRAM['Hostname'])) {
    $this->CIDRAM['Hostname'] = $this->dnsReverse($this->BlockInfo['IPAddr']);
}

/** Example signature. */
if (strlen($this->CIDRAM['Hostname']) && $this->CIDRAM['Hostname'] !== $this->BlockInfo['IPAddr']) {
    $this->trigger($this->CIDRAM['Hostname'] === 'www.foobar.tld', 'Foobar.tld', 'Hostname Foobar.tld is not allowed.');
}
```

#### 6.6 MODUL VARIABEL

Modul mengeksekusi dalam lingkup mereka sendiri, dan variabel apapun yang ditentukan oleh modul, tidak akan dapat diakses ke modul lain, atau ke skrip utama, kecuali jika disimpan dalam array `$CIDRAM` (segala sesuatu yang lain dibuang setelah eksekusi modul selesai).

Tercantum dibawah ini adalah beberapa variabel umum yang mungkin berguna untuk modul Anda:

Variabel | Deskripsi
----|----
`$this->BlockInfo['DateTime']` | Tanggal dan waktu sekarang.
`$this->BlockInfo['IPAddr']` | Alamat IP untuk permintaan saat ini.
`$this->BlockInfo['IPAddrResolved']` | Jika alamat IP untuk permintaan saat ini adalah alamat 6to4, Teredo, atau ISATAP, alamat tersebut diselesaikan ke padanan IPv4-nya. Jika tidak, maka alamat IP untuk permintaan saat ini.
`$this->BlockInfo['ScriptIdent']` | Versi skrip CIDRAM.
`$this->BlockInfo['Query']` | "Query" untuk permintaan saat ini.
`$this->BlockInfo['Referrer']` | Perujuk untuk permintaan saat ini (jika ada).
`$this->BlockInfo['UA']` | Agen pengguna (user agent) untuk permintaan saat ini.
`$this->BlockInfo['UALC']` | Agen pengguna (user agent) untuk permintaan saat ini (di huruf kecil).
`$this->BlockInfo['ReasonMessage']` | Pesan yang akan ditampilkan ke pengguna/klien untuk permintaan saat ini jika diblokir.
`$this->BlockInfo['SignatureCount']` | Jumlah tanda tangan dipicu untuk permintaan saat ini.
`$this->BlockInfo['Signatures']` | Informasi referensi untuk tanda tangan yang dipicu untuk permintaan saat ini.
`$this->BlockInfo['WhyReason']` | Informasi referensi untuk tanda tangan yang dipicu untuk permintaan saat ini.
`$this->BlockInfo['Request_Method']` | Metode permintaan untuk permintaan saat ini.
`$this->BlockInfo['Protocol']` | Protokol untuk permintaan saat ini.

---


### 7. <a name="SECTION7"></a>MASALAH KOMPATIBILITAS DIKETAHUI

Paket dan produk berikut telah ditemukan tidak bisa dioperasikan dengan CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Modul telah tersedia untuk memastikan bahwa paket dan produk berikut akan kompatibel dengan CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__
- __[Quic cloud](https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/)__

*Lihat juga: [Bagan Kompatibilitas](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>PERTANYAAN YANG SERING DIAJUKAN (FAQ)

- [Apa yang "tanda tangan"?](#user-content-WHAT_IS_A_SIGNATURE)
- [Apa yang "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [Apa yang dimaksud dengan "positif palsu"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [Dapat CIDRAM blok seluruh negara?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Seberapa sering tanda tangan diperbarui?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Saya mengalami masalah ketika menggunakan CIDRAM dan saya tidak tahu apa saya harus lakukan! Tolong bantu!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Saya diblokir oleh CIDRAM dari situs web yang saya ingin mengunjungi! Tolong bantu!](#user-content-BLOCKED_WHAT_TO_DO)
- [Saya ingin menggunakan CIDRAM v3 dengan versi PHP yang lebih tua dari 7.2; Anda dapat membantu?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Dapatkah saya menggunakan satu instalasi CIDRAM untuk melindungi beberapa domain?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Saya tidak ingin membuang waktu dengan menginstal ini dan membuatnya bekerja dengan situs web saya; Bisakah saya membayar Anda untuk melakukan semuanya untuk saya?](#user-content-PAY_YOU_TO_DO_IT)
- [Dapatkah saya mempekerjakan Anda atau pengembang proyek ini untuk pekerjaan pribadi?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Saya perlu modifikasi khusus, customisasi, dll; Apakah kamu bisa membantu?](#user-content-SPECIALIST_MODIFICATIONS)
- [Saya seorang pengembang, perancang situs web, atau programmer. Dapatkah saya menerima atau menawarkan pekerjaan yang berkaitan dengan proyek ini?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Saya ingin berkontribusi pada proyek ini; Dapatkah saya melakukan ini?](#user-content-WANT_TO_CONTRIBUTE)
- [Dapatkah saya menggunakan cron untuk mengupdate secara otomatis?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [Apa "pelanggaran"?](#user-content-WHAT_ARE_INFRACTIONS)
- [Dapatkah CIDRAM memblokir nama host?](#user-content-BLOCK_HOSTNAMES)
- [Apa yang bisa saya gunakan untuk "default_dns"?](#apa-yang-bisa-saya-gunakan-untuk-default_dns)
- [Dapatkah saya menggunakan CIDRAM untuk melindungi hal-hal selain daripada situs web (misalnya, server email, FTP, SSH, IRC, dll)?](#user-content-PROTECT_OTHER_THINGS)
- [Akankah masalah terjadi jika saya menggunakan CIDRAM pada saat yang sama dengan menggunakan layanan CDN atau cache?](#user-content-CDN_CACHING_PROBLEMS)
- [Akankah CIDRAM melindungi situs web saya dari serangan DDoS?](#user-content-DDOS_ATTACKS)
- [Ketika saya mengaktifkan atau menonaktifkan modul atau file tanda tangan melalui halaman pembaruan, itu memilah mereka secara alfanumerik dalam konfigurasi. Bisakah saya mengubah cara mereka disortir?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [Apa itu "PDO DSN"? Bagaimana saya bisa menggunakan PDO dengan CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM memblokir cronjobs; Bagaimana cara memperbaikinya?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>Apa yang "tanda tangan"?

Dalam konteks CIDRAM, "tanda tangan" mengacu pada data yang bertindak sebagai indikator/pengenal untuk sesuatu spesifik yang kita mencari, biasanya alamat IP atau CIDR, dan termasuk beberapa instruksi untuk CIDRAM, mengatakannya cara terbaik untuk menanggapi saat menemukan apa yang kita mencari. Tanda tangan khas untuk CIDRAM terlihat seperti ini:

Untuk "file tanda tangan":

`1.2.3.4/32 Deny Generic`

Untuk "modul":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Catat: Tanda tangan untuk "file tanda tangan", dan tanda tangan untuk "modul", bukanlah hal yang sama.*

Sering (tapi tidak selalu), tanda tangan akan digabungkan dalam grup-grup, Membentuk "bagian tanda tangan", sering disertai dengan komentar, markup, dan/atau metadata terkait yang bisa digunakan untuk memberikan konteks tambahan untuk tanda tangan dan/atau instruksi tambahan.

#### <a name="WHAT_IS_A_CIDR"></a>Apa yang "CIDR"?

"CIDR" adalah akronim untuk "Classless Inter-Domain Routing" *[[1](https://id.wikipedia.org/wiki/CIDR), [2](https://whatismyipaddress.com/cidr)]*, dan akronim inilah yang digunakan sebagai bagian dari nama paket ini, "CIDRAM", yang merupakan akronim untuk "Classless Inter-Domain Routing Access Manager".

Namun, dalam konteks CIDRAM (seperti, dalam dokumentasi ini, dalam diskusi yang berkaitan dengan CIDRAM, atau dalam data bahasa CIDRAM), kapanpun "CIDR" (tunggal) atau "CIDRs" (jamak) yang disebutkan (dan dengan demikian kita menggunakan kata-kata ini sebagai kata benda dalam hak mereka sendiri, daripada akronim), arti dimaksud dengan ini adalah subnet, dinyatakan menggunakan notasi CIDR. Alasan untuk CIDR (atau CIDRs) adalah digunakan daripada subnet adalah untuk memperjelas bahwa kita mengacu pada subnet yang menggunakan notasi CIDR (karena notasi CIDR hanyalah satu dari sekian banyak cara yang subnet bisa diekspresikan). CIDRAM bisa, oleh karena itu, dianggap sebagai "manajer akses untuk subnet".

Meskipun arti ganda ini untuk "CIDR" mungkin menghadirkan beberapa ambiguitas dalam beberapa kasus, penjelasan ini, bersama dengan konteks yang disediakan, harus membantu menyelesaikan ambiguitas ini.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>Apa yang dimaksud dengan "positif palsu"?

Istilah "positif palsu" (*alternatif: "kesalahan positif palsu"; "alarm palsu"*; Bahasa Inggris: *false positive*; *false positive error*; *false alarm*), dijelaskan dengan sangat sederhana, dan dalam konteks umum, digunakan saat pengujian untuk kondisi, untuk merujuk pada hasil tes, ketika hasilnya positif (yaitu, kondisi adalah dianggap untuk menjadi "positif", atau "benar"), namun diharapkan (atau seharusnya) menjadi negatif (yaitu, kondisi ini, pada kenyataannya, adalah "negatif", atau "palsu"). Sebuah "positif palsu" bisa dianggap analog dengan "menangis serigala" (dimana kondisi dites adalah apakah ada serigala di dekat kawanan, kondisi adalah "palsu" di bahwa tidak ada serigala di dekat kawanan, dan kondisi ini dilaporkan sebagai "positif" oleh gembala dengan cara memanggil "serigala, serigala"), atau analog dengan situasi dalam pengujian medis dimana seorang pasien didiagnosis sebagai memiliki beberapa penyakit, ketika pada kenyataannya, mereka tidak memiliki penyakit tersebut.

Hasil terkait ketika pengujian untuk kondisi dapat digambarkan menggunakan istilah "positif benar", "negatif benar" dan "negatif palsu". Sebuah "positif benar" mengacu pada saat hasil tes dan keadaan sebenarnya dari kondisi adalah keduanya benar (atau "positif"), dan sebuah "negatif benar" mengacu pada saat hasil tes dan keadaan sebenarnya dari kondisi adalah keduanya palsu (atau "negatif"); Sebuah "positif benar" atau "negatif benar" adalah dianggap untuk menjadi sebuah "inferensi benar". Antitesis dari "positif palsu" adalah sebuah "negatif palsu"; Sebuah "negatif palsu" mengacu pada saat hasil tes are negatif (yaitu, kondisi adalah dianggap untuk menjadi "negatif", atau "palsu"), namun diharapkan (atau seharusnya) menjadi positif (yaitu, kondisi ini, pada kenyataannya, adalah "positif", atau "benar").

Dalam konteks CIDRAM, istilah-istilah ini mengacu pada tanda tangan dari CIDRAM dan apa/siapa mereka memblokir. Ketika CIDRAM blok alamat IP karena buruk, usang atau salah tanda tangan, tapi seharusnya tidak melakukannya, atau ketika melakukannya untuk alasan salah, kita menyebut acara ini sebuah "positif palsu". Ketika CIDRAM gagal untuk memblokir alamat IP yang seharusnya diblokir, karena ancaman tak terduga, hilang tanda tangan atau kekurangan dalam tanda tangan nya, kita menyebut acara ini sebuah "deteksi terjawab" atau "missing detection" (ini analog dengan sebuah "negatif palsu").

Ini dapat diringkas dengan tabel dibawah:

&nbsp; | CIDRAM seharusnya *TIDAK* memblokir alamat IP | CIDRAM *SEHARUSNYA* memblokir alamat IP
---|---|---
CIDRAM *TIDAK* memblokir alamat IP | Negatif benar (inferensi benar) | Deteksi terjawab (analog dengan negatif palsu)
CIDRAM memblokir alamat IP | __Positif palsu__ | Positif benar (inferensi benar)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>Dapat CIDRAM blok seluruh negara?

Ya. Cara termudah untuk melakukan ini adalah dengan menginstal modul BGPView dan mengonfigurasinya sesuai dengan kebutuhan Anda.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Seberapa sering tanda tangan diperbarui?

Frekuensi pembaruan bervariasi tergantung pada file tanda tangan. Semua penulis bagi file tanda tangan CIDRAM umumnya mencoba untuk menjaga tanda tangan mereka sebagai diperbarui sebanyak mungkin, tapi karena semua dari kita memiliki komitmen lainnya, kehidupan kita di luar proyek, dan karena kita tidak dikompensasi finansial (yaitu, dibayar) untuk upaya kami pada proyek, jadwal pembaruan yang tepat tidak dapat dijamin. Umumnya, tanda tangan diperbarui ketika ada cukup waktu untuk memperbaruinya, dan umumnya, penulis mencoba untuk memprioritaskan berdasarkan kebutuhan dan frekuensi berbagai perubahan dalam rentang. Bantuan selalu dihargai jika Anda bersedia untuk menawarkan.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Saya mengalami masalah ketika menggunakan CIDRAM dan saya tidak tahu apa saya harus lakukan! Tolong bantu!

- Apakah Anda menggunakan versi terbaru bagi perangkat lunak? Apakah Anda menggunakan versi terbaru bagi file tanda tangan Anda? Jika jawaban untuk salah satu dari dua pertanyaan ini adalah tidak, mencoba untuk memperbarui segala sesuatu pertama, dan memeriksa apakah masalah terus berlanjut. Jika terus berlanjut, lanjutkan membaca.
- Apakah Anda memeriksa semua dokumentasi? Jika tidak, silakan melakukannya. Jika masalah tidak dapat diselesaikan dengan menggunakan dokumentasi, lanjutkan membaca.
- Apakah Anda memeriksa **[halaman issues](https://github.com/CIDRAM/CIDRAM/issues)**, untuk melihat apakah masalah telah disebutkan sebelumnya? Jika sudah disebutkan sebelumnya, memeriksa apakah ada saran, ide, dan/atau solusi yang tersedia, dan ikuti sesuai yang diperlukan untuk mencoba untuk menyelesaikan masalah.
- Jika masalah masih berlanjut, silakan mencari bantuan dengan membuat issue baru di halaman issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>Saya diblokir oleh CIDRAM dari situs web yang saya ingin mengunjungi! Tolong bantu!

CIDRAM menyediakan sarana bagi pemilik situs web untuk memblokir lalu lintas yang tidak diinginkan, tapi pemilik situs web bertanggung jawab untuk memutuskan bagaimana mereka ingin menggunakan CIDRAM. Dalam kasus positif palsu yang berkaitan dengan file tanda tangan yang biasanya disertakan dengan CIDRAM, koreksi dapat dibuat, tetapi dalam hal yang tidak terblokir dari situs web tertentu, Anda harus menghubungi pemilik dari situs yang bersangkutan. Dalam kasus dimana koreksi dibuat, setidaknya, mereka harus memperbarui file tanda tangan mereka dan/atau memperbarui instalasi mereka, dan dalam kasus lain (seperti, misalnya, ketika mereka diubah instalasi mereka, membuat tanda tangan kustom, dll), tanggung jawab untuk memecahkan masalah Anda sepenuhnya milik mereka, dan sepenuhnya di luar kendali kita.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Saya ingin menggunakan CIDRAM v3 dengan versi PHP yang lebih tua dari 7.2; Anda dapat membantu?

Tidak. PHP≥7.2 adalah persyaratan minimum untuk CIDRAM v3.

*Lihat juga: [Bagan Kompatibilitas](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Dapatkah saya menggunakan satu instalasi CIDRAM untuk melindungi beberapa domain?

Ya. Instalasi CIDRAM tidak secara alami terkunci pada domain tertentu, dan dengan demikian dapat digunakan untuk melindungi beberapa domain. Umumnya, kami mengacu pada instalasi CIDRAM yang hanya melindungi satu domain as "instalasi domain tunggal" ("single-domain installations"), dan kami mengacu pada instalasi CIDRAM yang melindungi beberapa domain dan/atau sub-domain sebagai "instalasi domain beberapa" ("multi-domain installations"). Jika Anda mengoperasikan instalasi domain beberapa dan perlu menggunakan berbagai kumpulan file tanda tangan untuk berbagai domain, atau perlu CIDRAM untuk dikonfigurasi secara berbeda untuk domain berbeda, kamu bisa melakukan ini. Setelah memuat file konfigurasi (`config.yml`), CIDRAM akan memeriksa adanya "file untuk pengganti konfigurasi" spesifik untuk domain (atau sub-domain) yang diminta (`domain-yang-diminta.tld.config.yml`), dan jika ditemukan, setiap nilai konfigurasi yang ditentukan oleh file untuk pengganti konfigurasi akan digunakan untuk instance eksekusi daripada nilai konfigurasi yang ditentukan oleh file konfigurasi. File untuk pengganti konfigurasi identik dengan file konfigurasi, dan atas kebijaksanaan Anda, dapat berisi keseluruhan semua konfigurasi yang tersedia untuk CIDRAM, atau apapun bagian kecil yang dibutuhkan yang berbeda dari nilai yang biasanya ditentukan oleh file konfigurasi. File untuk pengganti konfigurasi diberi nama sesuai dengan domain yang mereka inginkan (jadi, misalnya, jika Anda memerlukan file untuk pengganti konfigurasi untuk domain, `https://www.some-domain.tld/`, file untuk pengganti konfigurasi harus diberi nama sebagai `some-domain.tld.config.yml`, dan harus ditempatkan di dalam vault bersama file konfigurasi, `config.yml`). Nama domain untuk instance eksekusi berasal dari header permintaan `HTTP_HOST`; "www" diabaikan.

#### <a name="PAY_YOU_TO_DO_IT"></a>Saya tidak ingin membuang waktu dengan menginstal ini dan membuatnya bekerja dengan situs web saya; Bisakah saya membayar Anda untuk melakukan semuanya untuk saya?

Mungkin. Ini dipertimbangkan berdasarkan kasus per kasus. Beritahu kami apa yang Anda butuhkan, apa yang Anda tawarkan, dan kami akan memberitahu Anda jika kami dapat membantu.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Dapatkah saya mempekerjakan Anda atau pengembang proyek ini untuk pekerjaan pribadi?

*Lihat di atas.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Saya perlu modifikasi khusus, customisasi, dll; Apakah kamu bisa membantu?

*Lihat di atas.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Saya seorang pengembang, perancang situs web, atau programmer. Dapatkah saya menerima atau menawarkan pekerjaan yang berkaitan dengan proyek ini?

Ya. Lisensi kami tidak melarang hal ini.

#### <a name="WANT_TO_CONTRIBUTE"></a>Saya ingin berkontribusi pada proyek ini; Dapatkah saya melakukan ini?

Ya. Kontribusi untuk proyek ini sangat disambut baik. Silakan lihat "CONTRIBUTING.md" untuk informasi lebih lanjut.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Dapatkah saya menggunakan cron untuk mengupdate secara otomatis?

Ya. API dibangun dalam bagian depan untuk berinteraksi dengan halaman pembaruan melalui skrip eksternal. Skrip terpisah, "[Cronable](https://github.com/Maikuolan/Cronable)", tersedia, dan dapat digunakan oleh cron manager atau cron scheduler untuk mengupdate paket ini dan paket didukung lainnya secara otomatis (script ini menyediakan dokumentasi sendiri).

#### <a name="WHAT_ARE_INFRACTIONS"></a>Apa "pelanggaran"?

"Penghitungan tanda tangan" dan "pelanggaran" keduanya berhubungan dengan tingkat keparahan dan jumlah tanda tangan yang dipicu selama permintaan tertentu, tidak peduli apakah karena file tanda tangan, modul, aturan tambahan, atau lainnya, tetapi sementara "penghitungan tanda tangan" hanya bertahan untuk permintaan tertentu itu, "pelanggaran" dapat bertahan atas sejumlah permintaan, selama ditentukan oleh `default_tracktime`.

Ini menyediakan mekanisme untuk memastikan bahwa permintaan dari sumber yang berpotensi berbahaya dapat diblokir atas permintaan sekunder dari sumber tertentu yang mana telah diblokir selama permintaan sebelumnya dengan jumlah pelanggaran yang cukup.

#### <a name="BLOCK_HOSTNAMES"></a>Dapatkah CIDRAM memblokir nama host?

Ya. Ini dapat dicapai dengan membuat aturan tambahan atau modul kustom.

![Aturan tambahan untuk memblokir nama host](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>Apa yang bisa saya gunakan untuk "default_dns"?

Jika Anda mencari saran, [public-dns.info](https://public-dns.info/) dan [OpenNIC](https://servers.opennic.org/) berikan daftar ekstensif dari server DNS publik yang dikenal. Atau, lihat tabel dibawah ini:

IP | Operator
---|---
`1.1.1.1` | [Cloudflare](https://www.cloudflare.com/learning/dns/what-is-1.1.1.1/)
`8.8.4.4`<br />`8.8.8.8`<br />`2001:4860:4860::8844`<br />`2001:4860:4860::8888` | [Google Public DNS](https://developers.google.com/speed/public-dns/)
`9.9.9.9`<br />`149.112.112.112` | [Quad9 DNS](https://www.quad9.net/)
`84.200.69.80`<br />`84.200.70.40`<br />`2001:1608:10:25::1c04:b12f`<br />`2001:1608:10:25::9249:d69b` | [DNS.WATCH](https://dns.watch/index)
`208.67.220.220`<br />`208.67.222.220`<br />`208.67.222.222` | [OpenDNS Home](https://www.opendns.com/)
`77.88.8.1`<br />`77.88.8.8`<br />`2a02:6b8::feed:0ff`<br />`2a02:6b8:0:1::feed:0ff` | [Yandex.DNS](https://dns.yandex.com/advanced/)
`8.20.247.20`<br />`8.26.56.26` | [Comodo Secure DNS](https://www.comodo.com/secure-dns/)
`216.146.35.35`<br />`216.146.36.36` | [Dyn](https://help.dyn.com/internet-guide-setup/)
`64.6.64.6`<br />`64.6.65.6` | [Verisign Public DNS](https://www.verisign.com/en_US/security-services/public-dns/index.xhtml)
`37.235.1.174`<br />`37.235.1.177`<br />`45.33.97.5`<br />`172.104.237.57`<br />`172.104.49.100` | [FreeDNS](https://freedns.zone/en/)
`156.154.70.1`<br />`156.154.71.1`<br />`2610:a1:1018::1`<br />`2610:a1:1019::1` | [Neustar Security](https://www.security.neustar/dns-services/free-recursive-dns-service)
`45.32.36.36`<br />`45.77.165.194` | [Fourth Estate](https://dns.fourthestate.co/)
`74.82.42.42` | [Hurricane Electric](https://dns.he.net/)
`195.46.39.39`<br />`195.46.39.40` | [SafeDNS](https://www.safedns.com/en/features/)
`89.233.43.71`<br />`91.239.100.100 `<br />`2001:67c:28a4::`<br />`2a01:3a0:53:53::` | [UncensoredDNS](https://blog.uncensoreddns.org/)
`208.76.50.50`<br />`208.76.51.51` | [SmartViper](https://www.markosweb.com/free-dns/)

*Catat: Saya tidak membuat klaim atau jaminan berkenaan dengan praktik privasi, keamanan, keampuhan, atau keandalan untuk layanan DNS apapun, apakah terdaftar atau sebaliknya. Silakan lakukan penelitian Anda sendiri ketika membuat keputusan tentang mereka.*

#### <a name="PROTECT_OTHER_THINGS"></a>Dapatkah saya menggunakan CIDRAM untuk melindungi hal-hal selain daripada situs web (misalnya, server email, FTP, SSH, IRC, dll)?

Anda dapat (dalam pengertian hukum), tetapi Anda tidak seharusnya (dalam pengertian teknis dan praktis). Lisensi kami tidak membatasi teknologi mana yang implementasikan CIDRAM, tetapi CIDRAM adalah WAF (Aplikasi Web Firewall) dan selalu dimaksudkan untuk melindungi situs web. Karena itu tidak dirancang dengan teknologi lain dalam pikiran, kemungkinan besar itu tidak akan efektif atau memberikan perlindungan diandalkan untuk teknologi lain, implementasi bisa sulit, dan risiko positif palsu dan deteksi terjawab akan sangat tinggi.

#### <a name="CDN_CACHING_PROBLEMS"></a>Akankah masalah terjadi jika saya menggunakan CIDRAM pada saat yang sama dengan menggunakan layanan CDN atau cache?

Mungkin. Ini tergantung pada sifat layanan yang dipermasalahkan, dan bagaimana Anda menggunakannya. Umumnya, jika Anda hanya menyimpan aset statis dalam cache (gambar, CSS, dll; apapun yang umumnya tidak berubah seiring waktu), seharusnya tidak ada masalah. Namun, mungkin ada masalah, jika Anda menyimpan data dalam cache yang biasanya akan dihasilkan secara dinamis saat diminta, atau jika Anda menyimpan hasil dari permintaan POST (ini pada dasarnya akan membuat situs web Anda dan lingkungannya sebagai statis wajib, dan CIDRAM tidak akan memberikan manfaat yang berarti dalam lingkungan statis wajib). Mungkin juga ada persyaratan konfigurasi khusus untuk CIDRAM, tergantung pada layanan CDN atau cache yang Anda gunakan (Anda harus memastikan bahwa CIDRAM dikonfigurasi benar untuk layanan CDN atau cache spesifik yang Anda gunakan). Kegagalan untuk mengkonfigurasi CIDRAM benar dapat menyebabkan masalah positif palsu dan deteksi terjawab.

#### <a name="DDOS_ATTACKS"></a>Akankah CIDRAM melindungi situs web saya dari serangan DDoS?

Jawaban singkat: Tidak.

Jawaban sedikit lebih panjang: CIDRAM akan membantu mengurangi dampak yang dapat disebabkan oleh lalu lintas yang tidak diinginkan di situs web Anda (sehingga mengurangi biaya bandwidth situs web Anda), akan membantu mengurangi dampak yang dapat disebabkan oleh lalu lintas yang tidak diinginkan pada perangkat keras Anda (misalnya, kemampuan server Anda untuk memproses dan melayani permintaan), dan dapat membantu mengurangi berbagai efek negatif potensial lainnya yang terkait dengan lalu lintas yang tidak diinginkan. Namun, ada dua hal penting yang harus diingat untuk memahami pertanyaan ini.

Pertama, CIDRAM adalah paket PHP, dan karena itu beroperasi di mesin tempat PHP diinstal. Ini berarti bahwa CIDRAM hanya dapat melihat dan memblokir permintaan *setelah* server telah menerimanya. Kedua, mitigasi DDoS yang efektif harus menyaring permintaan *sebelum* mereka mencapai server yang ditargetkan oleh serangan DDoS. Idealnya, serangan DDoS harus dideteksi dan dimitigasi oleh solusi yang mampu menjatuhkan atau merutekan di tempat lain lalu lintas yang terkait dengan serangan, sebelum mencapai server yang ditargetkan di tempat pertama.

Ini dapat diimplementasikan dengan menggunakan solusi perangkat keras on-premise berdedikasi, dan/atau solusi berbasis cloud seperti layanan mitigasi DDoS berdedikasi, dengan merutekan DNS domain melalui jaringan yang dapat menahan serangan DDoS, dengan pemfilteran berbasis cloud, atau dengan beberapa kombinasinya. Bagaimanapun juga, subjek ini agak terlalu kompleks untuk dijelaskan secara menyeluruh hanya dengan satu atau dua paragraf, jadi saya akan merekomendasikan melakukan penelitian lebih lanjut jika ini adalah subjek yang ingin Anda kejar. Ketika sifat serangan DDoS benar dipahami, jawaban ini akan lebih masuk akal.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Ketika saya mengaktifkan atau menonaktifkan modul atau file tanda tangan melalui halaman pembaruan, itu memilah mereka secara alfanumerik dalam konfigurasi. Bisakah saya mengubah cara mereka disortir?

Ya. Jika Anda perlu memaksa beberapa file untuk dieksekusikan dalam urutan tertentu, Anda dapat menambahkan beberapa data sewenang-wenang sebelum nama mereka di direktif konfigurasi dimana mereka terdaftar, dipisahkan oleh titik dua. Ketika halaman pembaruan selanjutnya mengurutkan file lagi, data tambahan ini akan mempengaruhi urutan, menyebabkan mereka secara konsekuen mengeksekusi dalam urutan yang Anda inginkan, tanpa perlu mengganti nama mereka.

Misalnya, dengan asumsi direktif konfigurasi dengan file yang tercantum sebagai berikut:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Jika Anda ingin `file3.php` untuk mengeksekusi terlebih dahulu, Anda bisa menambahkan sesuatu seperti `aaa:` sebelum nama file:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Kemudian, jika file baru, `file6.php`, diaktifkan, ketika halaman pembaruan mengurutkan semuanya lagi, itu akan berakhir seperti ini:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

Situasi adalah sama ketika file dinonaktifkan. Sebaliknya, jika Anda ingin file dieksekusi terakhir, Anda bisa menambahkan sesuatu seperti `zzz:` sebelum nama file. Dalam hal apapun, Anda tidak perlu mengganti nama file yang dimaksud.

#### <a name="HOW_TO_USE_PDO"></a>Apa itu "PDO DSN"? Bagaimana saya bisa menggunakan PDO dengan CIDRAM?

"PDO" adalah akronim dari "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)". Ini menyediakan antarmuka untuk PHP untuk dapat terhubung ke beberapa sistem database yang biasa digunakan oleh berbagai aplikasi PHP.

"DSN" adalah akronim dari "[data source name](https://en.wikipedia.org/wiki/Data_source_name)" (nama sumber data). "PDO DSN" menjelaskan kepada PDO bagaimana seharusnya terhubung ke database.

CIDRAM menyediakan opsi untuk memanfaatkan PDO untuk tujuan caching. Agar ini berfungsi sebagaimana dimaksud, Anda harus mengkonfigurasi CIDRAM yang sesuai, demikian mengaktifkan PDO, membuat basis data baru untuk digunakan oleh CIDRAM (jika Anda belum memiliki basis data untuk digunakan oleh CIDRAM), dan membuat tabel baru di database Anda sesuai dengan struktur yang dijelaskan dibawah.

Ketika koneksi basis data berhasil, tapi tabel yang diperlukan tidak ada, akan berusaha membuatnya secara otomatis. Namun, perilaku ini belum diuji secara luas dan kesuksesan tidak dapat dijamin.

Ini, tentu saja, hanya berlaku jika Anda ingin CIDRAM menggunakan PDO. Jika Anda cukup senang untuk CIDRAM untuk menggunakan caching flatfile (per konfigurasi default), atau salah satu dari berbagai opsi caching lain yang disediakan, Anda tidak perlu repot-repot menyusahkan diri Anda dengan mengatur database, tabel dan sebagainya.

Struktur yang dijelaskan dibawah menggunakan "cidram" sebagai nama basis datanya, tetapi Anda dapat menggunakan nama yang Anda inginkan untuk basis data Anda, asalkan nama yang sama direplikasi pada konfigurasi DSN Anda.

```
╔══════════════════════════════════════════════╗
║ DATABASE "cidram"                            ║
║ │╔═══════════════════════════════════════════╩═════╗
║ └╫─TABLE "Cache" (UTF-8)                           ║
║  ╠═╪═FIELD══CHARSET═DATATYPE═════KEY══NULL═DEFAULT═╣
║  ║ ├─"Key"──UTF-8───VARCHAR(128)─PRI──×────×       ║
║  ║ ├─"Data"─UTF-8───TEXT─────────×────×────×       ║
╚══╣ └─"Time"─×───────INT(>=10)────×────×────×       ║
   ╚═════════════════════════════════════════════════╝
```

Direktif konfigurasi `pdo_dsn` harus dikonfigurasi seperti dijelaskan dibawah.

```
Tergantung pada driver basis data yang digunakan...
├─4d (Peringatan: Eksperimental, belum diuji, tidak direkomendasikan!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └Host untuk terhubung dengan untuk menemukan database.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └Nama basis data yang akan
│                │              │             digunakan.
│                │              │
│                │              └Nomor port yang akan dihubungkan dengan host.
│                │
│                └Host untuk terhubung dengan untuk menemukan database.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └Nama basis data yang akan digunakan.
│    │          │
│    │          └Host untuk terhubung dengan untuk menemukan database.
│    │
│    └Nilai yang mungkin: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Dapat menjadi jalur ke file database lokal.
│                    │
│                    ├Dapat terhubung dengan nomor host dan port.
│                    │
│                    └Anda harus merujuk pada dokumentasi Firebird jika Anda
│                     ingin menggunakan ini.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Database yang di katalog untuk dihubungkan.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Database yang di katalog untuk dihubungkan.
├─mysql (Paling direkomendasikan!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └Nomor port yang akan dihubungkan
│                 │            │               dengan host.
│                 │            │
│                 │            └Host untuk terhubung dengan untuk menemukan
│                 │             database.
│                 │
│                 └Nama basis data yang akan digunakan.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Dapat merujuk ke database terkatalog spesifik.
│               │
│               ├Dapat terhubung dengan nomor host dan port.
│               │
│               └Anda harus merujuk pada dokumentasi Oracle jika Anda ingin
│                menggunakan ini.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Dapat merujuk ke database terkatalog spesifik.
│         │
│         ├Dapat terhubung dengan nomor host dan port.
│         │
│         └Anda harus merujuk pada dokumentasi ODBC/DB2 jika Anda ingin
│          menggunakan ini.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └Nama basis data yang akan
│               │              │            digunakan.
│               │              │
│               │              └Nomor port yang akan dihubungkan dengan host.
│               │
│               └Host untuk terhubung dengan untuk menemukan database.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └Jalur ke file database lokal untuk digunakan.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └Nama basis data yang akan digunakan.
                   │         │
                   │         └Nomor port yang akan dihubungkan dengan host.
                   │
                   └Host untuk terhubung dengan untuk menemukan database.
```

Jika Anda tidak yakin tentang apa yang harus digunakan untuk beberapa bagian tertentu dari DSN Anda, coba lihat terlebih dahulu apakah itu berfungsi sebagaimana mestinya, tanpa mengubah apapun.

Perhatikan bahwa `pdo_username` dan` pdo_password` harus sama dengan nama pengguna dan kata sandi yang Anda pilih untuk basis data Anda.

#### <a name="BLOCK_CRON"></a>CIDRAM memblokir cronjobs; Bagaimana cara memperbaikinya?

Jika Anda menggunakan file yang berdedikasi untuk tujuan cronjobs, dan jika file ini tidak perlu dipanggil selama permintaan pengguna normal (yaitu di luar konteks cronjobs), cara paling mudah untuk memperbaikinya adalah dengan memastikan bahwa CIDRAM tidak dieksekusi sama sekali selama cronjobs Anda (yaitu, jangan menghubungkan CIDRAM ke file yang bertanggung jawab untuk menangani cronjobs Anda).

Atau, jika alamat IP server cron Anda relatif konsisten dan dapat diprediksi, Anda dapat mencoba memasukkan alamat IP server cron Anda ke daftar putih dengan membuat tanda tangan daftar putih untuknya dalam file tanda tangan kustom atau dengan membuat aturan tambahan untuk memasukkannya ke daftar putih. Jika alamat IP server cron Anda secara teratur berubah dan tidak dapat diprediksi, tapi tetap saja dari dalam jaringan tertentu yang sama, Anda bisa mencoba mendaftar di file `ignore.dat` Anda nama bagian tanda tangan yang bertanggung jawab untuk memblokirnya di tempat pertama.

Jika Anda sudah mencoba semua ide ini dan tidak ada bekerja untuk Anda, atau jika Anda perlu bantuan mencari tahu cara melakukannya, Anda dapat membuat issue baru di halaman issues CIDRAM untuk meminta bantuan.

---


### 9. <a name="SECTION9"></a>INFORMASI HUKUM

#### 9.0 PENGANTAR BAGIAN

Bagian dokumentasi ini dimaksudkan untuk menjelaskan kemungkinan pertimbangan hukum mengenai penggunaan dan implementasi paket, dan untuk memberikan beberapa informasi dasar terkait. Ini mungkin penting bagi beberapa pengguna sebagai sarana untuk memastikan kepatuhan dengan persyaratan hukum yang mungkin ada di negara tempat mereka beroperasi, dan beberapa pengguna mungkin perlu menyesuaikan kebijakan situs web mereka sesuai dengan informasi ini.

Pertama dan terutama, silakan menyadari bahwa saya (penulis paket) bukan seorang pengacara, atau profesional hukum yang berkualitas dalam bentuk apapun. Oleh karena itu, saya secara hukum tidak memenuhi syarat untuk memberikan nasihat hukum. Juga, dalam beberapa kasus, persyaratan hukum yang tepat dapat bervariasi antara negara dan yurisdiksi yang berbeda, dan berbagai persyaratan hukum ini terkadang dapat menimbulkan konflik (seperti, misalnya, dalam kasus negara-negara yang mendukung hak privasi dan hak untuk dilupakan, versus negara-negara yang mendukung retensi data diperpanjang). Pertimbangkan juga bahwa akses ke paket tidak terbatas pada negara atau yurisdiksi tertentu, dan oleh karena itu, pengguna paket cenderung ke geografis yang beragam. Poin-poin ini dianggap, saya tidak dalam posisi untuk menyatakan apa artinya "mematuhi hukum" untuk semua pengguna, dalam semua hal. Namun, saya berharap informasi disini akan membantu Anda untuk mengambil keputusan sendiri mengenai apa yang Anda harus lakukan agar tetap mematuhi hukum dalam konteks paket. Jika Anda memiliki keraguan atau kekhawatiran mengenai informasi disini, atau jika Anda membutuhkan bantuan dan saran tambahan dari perspektif hukum, saya merekomendasikan konsultasi dengan profesional hukum yang berkualitas.

#### 9.1 TANGGUNG JAWAB DAN KEWAJIBAN HUKUM

Seperti yang telah dinyatakan oleh lisensi paket, paket ini disediakan tanpa jaminan apapun. Ini termasuk (tetapi tidak terbatas pada) semua lingkup kewajiban hukum. Paket ini diberikan kepada Anda untuk kenyamanan Anda, dengan harapan itu akan berguna, dan itu akan memberikan beberapa manfaat bagi Anda. Namun, apakah Anda menggunakan atau mengimplementasikan paket ini, adalah pilihan Anda sendiri. Anda tidak dipaksa untuk menggunakan atau mengimplementasikan paket ini, tetapi ketika Anda melakukannya, Anda bertanggung jawab atas keputusan itu. Bukan saya, dan tidak ada kontributor lain untuk paket ini, bertanggung jawab secara hukum atas konsekuensi keputusan yang Anda buat, terlepas dari apakah langsung, tidak langsung, tersirat, atau sebaliknya.

#### 9.2 PIHAK KETIGA

Tergantung pada konfigurasi dan implementasinya yang tepat, paket dapat berkomunikasi dan berbagi informasi dengan pihak ketiga dalam beberapa kasus. Informasi ini dapat didefinisikan sebagai "informasi identitas pribadi" (PII) dalam beberapa konteks, oleh beberapa yurisdiksi.

Bagaimana informasi ini dapat digunakan oleh pihak ketiga ini, tunduk pada berbagai kebijakan yang ditetapkan oleh pihak ketiga ini, dan berada di luar ruang lingkup dokumentasi ini. Namun, dalam semua kasus tersebut, berbagi informasi dengan pihak ketiga ini dapat dinonaktifkan. Dalam semua kasus semacam itu, jika Anda memilih untuk mengaktifkannya, Anda bertanggung jawab untuk meneliti setiap kekhawatiran yang mungkin Anda miliki tentang privasi, keamanan, dan penggunaan PII oleh pihak ketiga ini. Jika ada keraguan, atau jika Anda tidak puas dengan perilaku pihak ketiga ini sehubungan dengan PII, mungkin terbaik adalah menonaktifkan semua pembagian informasi dengan pihak ketiga ini.

Untuk tujuan transparansi, jenis informasi yang dibagikan, dan dengan siapa, dijelaskan dibawah ini.

##### 9.2.0 PENCARIAN NAMA HOST

Jika Anda menggunakan fitur atau modul yang dimaksudkan untuk bekerja dengan nama host (seperti "modul pemblokir untuk host buruk", "tor project exit nodes block module", atau "verifikasi mesin pencari", misalnya), CIDRAM harus dapat memperoleh nama host dari permintaan masuk entah bagaimana. Biasanya, ini dilakukan dengan meminta nama host dari alamat IP permintaan masuk dari server DNS, atau dengan meminta informasi melalui fungsionalitas yang disediakan oleh sistem tempat CIDRAM diinstal (ini biasanya disebut sebagai "pencarian nama host"). Server DNS yang ditentukan secara default adalah milik layanan [Google DNS](https://dns.google.com/) (tetapi ini dapat dengan mudah diubah melalui konfigurasi). Layanan yang tepat yang dikomunikasikan dapat dikonfigurasi, dan tergantung pada cara Anda mengonfigurasi paket. Dalam kasus menggunakan fungsionalitas yang disediakan oleh sistem tempat CIDRAM diinstal, Anda harus menghubungi administrator sistem Anda untuk menentukan rute mana yang digunakan oleh pencarian nama host. Pencarian nama host dapat dicegah dalam CIDRAM dengan menghindari modul yang terpengaruh atau dengan memodifikasi konfigurasi paket sesuai dengan kebutuhan Anda.

*Direktif konfigurasi yang relevan:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 VERIFIKASI MESIN PENCARI DAN MEDIA SOSIAL

Ketika verifikasi mesin pencari diaktifkan, CIDRAM mencoba melakukan "pencarian DNS ke depan" untuk memverifikasi apakah permintaan yang mengaku berasal dari mesin pencari adalah asli. Juga, ketika verifikasi media sosial diaktifkan, CIDRAM melakukan hal yang sama untuk permintaan media sosial dugaan. Untuk melakukan ini, verifikasi mesin pencari menggunakan layanan [Google DNS](https://dns.google.com/) untuk mencoba menyelesaikan alamat IP dari nama host dari permintaan masuk ini (dalam proses ini, nama host dari permintaan masuk ini dibagikan dengan layanan).

*Direktif konfigurasi yang relevan:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM mendukung reCAPTCHA dan hCaptcha. Mereka membutuhkan kunci API agar berfungsi dengan benar. Mereka dinonaktifkan secara default, tetapi dapat diaktifkan dengan mengonfigurasi kunci API yang diperlukan. Ketika diaktifkan, komunikasi dapat terjadi antara layanan dan CIDRAM atau browser pengguna. Ini mungkin melibatkan mengkomunikasikan informasi seperti alamat IP pengguna, agen pengguna, sistem operasi, dan detail lain yang tersedia untuk permintaan tersebut.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) adalah layanan fantastis, tersedia secara bebas yang dapat membantu melindungi forum, blog, dan situs web dari spammer. Ini dilakukan dengan menyediakan database spammer yang dikenal, dan API yang dapat dimanfaatkan untuk memeriksa apakah alamat IP, nama pengguna, atau alamat email tercantum dalam database-nya.

CIDRAM menyediakan modul opsional yang memanfaatkan API ini untuk memeriksa apakah alamat IP dari permintaan masuk milik seorang spammer yang dicurigai. Jika dan ketika modul diinstal dan diaktifkan, alamat IP pengguna dapat dibagikan dengan layanan sesuai dengan konfigurasi dan tujuan yang dimaksudkan dari modul.

##### 9.2.4 ABUSEIPDB

CIDRAM menyediakan modul opsional untuk memblokir alamat IP yang memiliki catatan penyalahgunaan oleh menggunakan API [AbuseIPDB](https://www.abuseipdb.com/). Jika dan ketika modul diinstal dan diaktifkan, alamat IP pengguna dapat dibagikan dengan layanan sesuai dengan konfigurasi dan tujuan yang dimaksudkan dari modul.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM menyediakan modul opsional untuk melakukan pencarian ASN dan kode negara menggunakan API [BGPView](https://bgpview.io/) dan API [IP-API](https://ip-api.com/). Pencarian ini menyediakan kemampuan untuk memblokir atau memasukkan daftar putih berdasarkan ASN atau negara asal mereka. Jika dan ketika modul diinstal dan diaktifkan, alamat IP pengguna dapat dibagikan dengan layanan sesuai dengan konfigurasi dan tujuan yang dimaksudkan dari modul.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM menyediakan modul opsional untuk memblokir alamat IP yang memiliki catatan penyalahgunaan oleh menggunakan API [Project Honeypot](https://www.projecthoneypot.org/). Jika dan ketika modul diinstal dan diaktifkan, alamat IP pengguna dapat dibagikan dengan layanan sesuai dengan konfigurasi dan tujuan yang dimaksudkan dari modul.

#### 9.3 PENCATATAN

Pencatatan adalah bagian penting dari CIDRAM karena sejumlah alasan. Mungkin sulit untuk mendiagnosis dan menyelesaikan kesalahan positif ketika kejadian blokir yang menyebabkan mereka tidak dicatat. Tanpa mencatat kejadian blokir, mungkin sulit untuk memastikan secara akurat seberapa baik kinerja CIDRAM dalam konteks tertentu, dan mungkin sulit untuk menentukan dimana kekurangannya, dan perubahan apa yang mungkin diperlukan untuk konfigurasi atau tanda tangan yang sesuai, agar terus berfungsi sebagaimana dimaksud. Apapun, pencatatan mungkin tidak diinginkan untuk semua pengguna, dan tetap sepenuhnya opsional. Di CIDRAM, pencatatan dinonaktifkan secara default. Untuk mengaktifkannya, CIDRAM harus dikonfigurasi dengan benar.

Juga, apakah pencatatan diizinkan secara hukum, dan sejauh diizinkan secara hukum (misalnya, jenis informasi yang dapat dicatat, untuk berapa lama, dan dalam keadaan apa), dapat bervariasi, tergantung pada yurisdiksi dan pada konteks dimana CIDRAM diimplementasikan (misalnya, apakah Anda beroperasi sebagai individu, sebagai entitas perusahaan, dan apakah secara komersial atau non-komersial). Jadi, mungkin berguna bagi Anda untuk membaca bagian ini dengan seksama.

Ada beberapa jenis pencatatan yang dapat dilakukan oleh CIDRAM. Berbagai jenis pencatatan melibatkan berbagai jenis informasi, untuk berbagai alasan.

##### 9.3.0 KEJADIAN BLOKIR

Jenis utama dari pencatatan yang dapat dilakukan oleh CIDRAM berhubungan dengan "kejadian blokir". Jenis pencatatan ini terkait dengan kapan CIDRAM memblokir permintaan, dan dapat diberikan dalam tiga format berbeda:
- File log yang dapat dibaca oleh manusia.
- File log gaya Apache.
- File log dalam format serial.

Kejadian blokir, yang dicatat ke file log yang dapat dibaca oleh manusia, biasanya terlihat seperti ini (sebagai contoh):

```
ID: 1234
Versi Skrip: CIDRAM v1.6.0
Tanggal/Waktu: Day, dd Mon 20xx hh:ii:ss +0000
Alamat IP: x.x.x.x
Nama host: dns.hostname.tld
Menghitung Tanda Tangan: 1
Tanda Tangan Referensi: x.x.x.x/xx
Mengapa Diblokir: Layanan komputasi awan ("Nama Jaringan", Lxx:Fx, [XX])!
Agen Pengguna: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Direkonstruksi URI: https://your-site.tld/index.php
Status CAPTCHA: Diaktifkan.
```

Kejadian blokir yang sama ini, yang dicatat ke file log dalam gaya Apache, akan terlihat seperti ini:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Kejadian blokir yang dicatat biasanya mencakup informasi berikut:
- Nomor ID yang mereferensi pada kejadian blokir.
- Versi CIDRAM sedang digunakan.
- Tanggal dan waktu saat kejadian blokir terjadi.
- Alamat IP dari permintaan yang diblokir.
- Nama host dari alamat IP dari permintaan yang diblokir (bila tersedia).
- Jumlah tanda tangan yang dipicu oleh permintaan.
- Referensi untuk tanda tangan dipicu.
- Referensi ke alasan untuk kejadian blokir dan beberapa informasi debug dasar yang terkait.
- Agen pengguna dari permintaan yang diblokir (yaitu, bagaimana entitas yang meminta mengidentifikasi dirinya untuk permintaan tersebut).
- Rekonstruksi pengidentifikasi untuk sumber yang awalnya diminta.
- Status CAPTCHA untuk permintaan saat ini (bila relevan).

*Direktif konfigurasi yang bertanggung jawab untuk jenis pencatatan ini, dan untuk masing-masing dari tiga format yang tersedia, adalah:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Ketika direktif ini dibiarkan kosong, jenis pencatatan ini akan tetap dinonaktifkan.

##### 9.3.1 LOG CAPTCHA

Jenis pencatatan ini secara khusus berkaitan dengan instance CAPTCHA, dan hanya terjadi ketika pengguna mencoba menyelesaikan instance CAPTCHA.

Entri log CAPTCHA berisi alamat IP pengguna yang berusaha menyelesaikan instance CAPTCHA, tanggal dan waktu ketika itu terjadi, dan status CAPTCHA. Entri log CAPTCHA biasanya terlihat seperti ini (sebagai contoh):

```
Alamat IP: x.x.x.x - Tanggal/Waktu: Day, dd Mon 20xx hh:ii:ss +0000 - Status CAPTCHA: Lulus!
```

*Direktif konfigurasi yang bertanggung jawab untuk pencatatan CAPTCHA adalah:*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 LOG BAGIAN DEPAN

Jenis pencatatan ini berhubungan dengan upaya masuk bagian depan, dan hanya terjadi ketika pengguna mencoba masuk ke bagian depan (dengan asumsi akses bagian depan diaktifkan).

Entri log untuk bagian depan berisi alamat IP pengguna yang mencoba masuk, tanggal dan waktu ketika itu terjadi, dan hasil dari upaya tersebut (berhasil masuk, atau gagal masuk). Entri log untuk bagian depan biasanya terlihat seperti ini (sebagai contoh):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Dimasuk.
```

*Direktif konfigurasi yang bertanggung jawab untuk pencatatan bagian depan adalah:*
- `frontend` -> `frontend_log`

##### 9.3.3 ROTASI LOG

Anda mungkin ingin membersihkan log setelah jangka waktu tertentu, atau mungkin diminta untuk melakukannya oleh hukum (yaitu, jumlah waktu yang diizinkan secara hukum bagi Anda untuk mempertahankan log mungkin dibatasi oleh hukum). Anda dapat mencapai ini dengan menyertakan penanda tanggal/waktu dalam nama-nama file log Anda sesuai yang ditentukan oleh konfigurasi paket Anda (misalnya, `{yyyy}-{mm}-{dd}.log`), dan kemudian mengaktifkan rotasi log (rotasi log memungkinkan Anda untuk melakukan beberapa tindakan pada file log ketika batas yang ditentukan terlampaui).

Sebagai contoh: Jika saya secara hukum diminta untuk menghapus log setelah 30 hari, saya bisa menentukan `{dd}.log` dalam nama file log saya (`{dd}` represents days), atur nilai `log_rotation_limit` ke 30, dan atur nilai `log_rotation_action` ke `Delete`.

Sebaliknya, jika Anda diminta untuk menyimpan log untuk jangka waktu yang panjang, Anda bisa memilih untuk tidak menggunakan rotasi log sama sekali, atau Anda bisa mengatur nilai `log_rotation_action` ke `Archive`, untuk mengompres file log, sehingga mengurangi jumlah total ruang disk yang mereka tempati.

*Direktif konfigurasi yang relevan:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 PEMOTONGAN LOG

Ini juga memungkinkan untuk memotong file log individu ketika mereka melebihi ukuran tertentu, jika ini adalah sesuatu yang mungkin Anda butuhkan atau ingin lakukan.

*Direktif konfigurasi yang relevan:*
- `logging` -> `truncate`

##### 9.3.5 PSEUDONIMISASI ALAMAT IP

Pertama, jika Anda tidak akrab dengan istilah ini, "pseudonimisasi" mengacu pada memproses data pribadi sedemikian rupa sehingga tidak dapat diidentifikasi ke subjek data tertentu lagi tanpa beberapa informasi tambahan, dan dengan ketentuan bahwa informasi tambahan tersebut dipelihara secara terpisah dan tunduk pada tindakan teknis dan organisasi untuk memastikan bahwa data pribadi tidak dapat diidentifikasi kepada orang alami.

Dalam beberapa keadaan, Anda mungkin diperlukan secara hukum untuk membuat dianonimisasi atau dipseudonimisasi setiap PII dikumpulkan, diproses, atau disimpan. Meskipun konsep ini telah ada untuk beberapa waktu sekarang, GDPR/DSGVO terutama menyebutkan, dan secara khusus mendorong "pseudonimisasi".

CIDRAM mampu mem-pseudonimisasi alamat IP ketika melakukan pencatatan, jika ini adalah sesuatu yang mungkin Anda butuhkan atau ingin lakukan. Ketika CIDRAM mem-pseudonimkan alamat IP, saat dicatat, oktet terakhir dari alamat IPv4, dan semuanya setelah bagian kedua dari alamat IPv6 diwakili oleh "x" (efektif membulatkan alamat IPv4 ke alamat awal dari subnet ke-24 dari faktor dimana mereka dimasukkan, dan alamat IPv6 ke alamat awal dari subnet ke-32 dari faktor dimana mereka dimasukkan).

*Catat: Proses pseudonimisasi alamat IP untuk CIDRAM tidak mempengaruhi fitur pelacakan IP untuk CIDRAM. Jika ini masalah bagi Anda, mungkin yang terbaik adalah menonaktifkan pelacakan IP sepenuhnya.*

*Direktif konfigurasi yang relevan:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 MENGHILANGKAN INFORMASI LOG

Jika Anda ingin melangkah lebih jauh dengan mencegah jenis informasi tertentu sedang dicatat sepenuhnya, ini juga mungkin dilakukan. Di halaman konfigurasi, silakan merujuk ke direktif konfigurasi `fields` untuk mengontrol mana bidang yang muncul di entri log dan di halaman "Akses Ditolak".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Catat: Tidak ada alasan untuk menggunakan pseudonim dengan alamat IP ketika menghilangkannya dari log sepenuhnya.*

*Direktif konfigurasi yang relevan:*
- `general` -> `fields`

##### 9.3.7 STATISTIK

CIDRAM secara opsional dapat melacak statistik seperti jumlah total kejadian blokir atau instance CAPTCHA yang telah terjadi sejak beberapa titik waktu tertentu. Fitur ini dinonaktifkan secara default, tetapi dapat diaktifkan melalui konfigurasi paket. Fitur ini hanya melacak jumlah total kejadian yang terjadi, dan tidak termasuk informasi apapun tentang kejadian tertentu (dan dengan demikian, tidak boleh dianggap sebagai PII).

*Direktif konfigurasi yang relevan:*
- `general` -> `statistics`

##### 9.3.8 ENKRIPSI

CIDRAM tidak mengenkripsi cache atau informasi log apapun. [Enkripsi](https://id.wikipedia.org/wiki/Enkripsi) cache dan log dapat diperkenalkan di masa depan, tetapi tidak ada rencana khusus untuk itu saat ini. Jika Anda khawatir tentang pihak ketiga yang tidak sah mendapatkan akses ke bagian depan dari CIDRAM yang mungkin berisi PII atau informasi sensitif seperti cache atau log-nya, saya akan merekomendasikan bahwa CIDRAM tidak diinstal di lokasi yang dapat diakses publik (misalnya, instal CIDRAM di luar direktori `public_html` standar atau yang setara dengan yang tersedia untuk sebagian besar web server standar) dan bahwa perizinan restriktif yang tepat diberlakukan untuk direktori tempat ia tinggal (khususnya, untuk direktori vault). Jika itu tidak cukup untuk mengatasi masalah Anda, konfigurasikan CIDRAM sedemikian rupa sehingga jenis informasi yang menyebabkan kekhawatiran Anda tidak akan dikumpulkan atau dicatat di tempat pertama (seperti, dengan menonaktifkan pencatatan).

#### 9.4 COOKIE

CIDRAM menetapkan [cookie](https://id.wikipedia.org/wiki/Kuki_HTTP) pada dua titik dalam basis kodenya. Pertama, ketika pengguna berhasil menyelesaikan instance CAPTCHA (dan mengasumsikan bahwa `lockuser` diatur ke `true`), CIDRAM menetapkan cookie agar dapat mengingat untuk permintaan berikutnya bahwa pengguna telah menyelesaikan instance CAPTCHA, sehingga tidak perlu meminta pengguna untuk menyelesaikan instance CAPTCHA pada permintaan berikutnya. Kedua, ketika pengguna berhasil masuk ke akses bagian depan, CIDRAM menetapkan cookie agar dapat mengingat pengguna untuk permintaan berikutnya (yaitu, cookie digunakan untuk mengotentikasi pengguna ke sesi masuk).

Dalam kedua kasus, peringatan cookie ditampilkan dengan jelas (bila berlaku), memperingatkan pengguna bahwa cookie akan diatur jika mereka terlibat dalam tindakan yang relevan. Cookie tidak diatur dalam titik lain di basis kode.

*Catat: CAPTCHA API "tak terlihat" mungkin tidak kompatibel dengan hukum cookie di beberapa yurisdiksi, dan harus dihindari oleh situs web apapun yang tunduk pada hukum-hukum tersebut. Memilih untuk menggunakan API lain yang disediakan, atau menonaktifkan CAPTCHA sepenuhnya, mungkin lebih disukai.*

*Direktif konfigurasi yang relevan:*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 PEMASARAN DAN PERIKLANAN

CIDRAM tidak mengumpulkan atau memproses informasi apapun untuk tujuan pemasaran atau periklanan, dan tidak menjual atau memperoleh keuntungan dari informasi yang dikumpulkan atau dicatat. CIDRAM bukan perusahaan komersial, juga tidak terkait dengan kepentingan komersial, sehingga melakukan hal-hal ini tidak akan masuk akal. Ini telah terjadi sejak awal proyek, dan terus menjadi kasus hari ini. Juga, melakukan hal-hal ini akan menjadi kontra-produktif terhadap semangat dan tujuan yang dimaksudkan dari proyek secara keseluruhan, dan selama saya terus mempertahankan proyek, tidak akan pernah terjadi.

#### 9.6 KEBIJAKAN PRIVASI

Dalam beberapa keadaan, Anda mungkin diharuskan secara hukum untuk secara jelas menampilkan tautan ke kebijakan privasi Anda pada semua halaman dan bagian dari situs web Anda. Ini mungkin penting sebagai sarana untuk memastikan bahwa pengguna mendapat informasi yang jelas tentang praktik privasi Anda, jenis PII yang Anda kumpulkan, dan bagaimana Anda akan menggunakannya. Agar dapat menyertakan tautan di halaman "Akses Ditolak" CIDRAM, direktif konfigurasi disediakan untuk menentukan URL ke kebijakan privasi Anda.

*Catat: Sangat disarankan agar halaman kebijakan privasi Anda tidak ditempatkan di belakang perlindungan CIDRAM. Jika CIDRAM melindungi halaman kebijakan privasi Anda, dan pengguna yang diblokir oleh CIDRAM mengklik tautan ke kebijakan privasi Anda, mereka akan diblokir lagi, dan tidak akan dapat melihat kebijakan privasi Anda. Idealnya, Anda harus menautkan ke salinan statis dari kebijakan privasi Anda, seperti halaman HTML atau file teks biasa yang tidak dilindungi oleh CIDRAM.*

*Direktif konfigurasi yang relevan:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

Regulasi Perlindungan Data Umum (GDPR) adalah regulasi dari Uni Eropa, yang mulai berlaku pada 25 Mei 2018. Tujuan utama dari regulasi ini adalah untuk memberikan kontrol kepada warga dan penduduk negara Uni Eropa mengenai data pribadi mereka sendiri, dan untuk menyatukan regulasi di Uni Eropa terkait privasi dan data pribadi.

Regulasi ini tersebut berisi ketentuan khusus yang berkaitan dengan pemrosesan "informasi identitas pribadi" (PII) dari setiap "subjek data" (setiap orang alami yang teridentifikasi atau dapat diidentifikasi) dari atau di dalam Uni Eropa. Agar sesuai dengan regulasi, "perusahaan" atau "enterprise" (sesuai yang didefinisikan oleh regulasi), dan sistem dan proses yang relevan harus mengimplementasikan "privasi berdasarkan desain" secara default, harus menggunakan pengaturan privasi setinggi mungkin, harus mengimplementasikan pengamanan yang diperlukan untuk informasi yang disimpan atau diproses (termasuk, tetapi tidak terbatas pada, mengimplementasikan pseudonimisasi atau anonimisasi yang penuh untuk data), harus jelas dan tidak ambigu menyatakan jenis data yang mereka kumpulkan, bagaimana mereka memprosesnya, untuk alasan apa, untuk berapa lama mereka menyimpannya, dan apakah mereka membagikan data ini dengan pihak ketiga manapun, jenis data yang dibagikan dengan pihak ketiga, bagaimana, mengapa, dan sebagainya.

Data tidak dapat diproses kecuali jika ada dasar yang sah untuk melakukannya, sesuai yang didefinisikan oleh regulasi. Umumnya, ini berarti bahwa untuk memproses data data subjek secara sah, itu harus dilakukan sesuai dengan kewajiban hukum, atau dilakukan hanya setelah persetujuan eksplisit, terinformasi dengan baik, dan tidak ambigu diperoleh dari subjek data.

Karena aspek regulasi dapat berevolusi dalam waktu, untuk menghindari penyebaran informasi yang ketinggalan jaman, mungkin lebih baik untuk belajar tentang regulasi dari sumber yang berwenang, dibandingkan dengan hanya memasukkan informasi yang relevan disini dalam dokumentasi paket (yang akhirnya bisa menjadi usang seiring berkembangnya regulasi).

Beberapa sumber bacaan yang direkomendasikan untuk mempelajari informasi lebih lanjut:
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [Regulasi Perlindungan Data](https://id.wikipedia.org/wiki/Regulasi_Perlindungan_Data)

---


### 10. <a name="SECTION10"></a>MEMUTAKHIRKAN DARI VERSI UTAMA SEBELUMNYA

#### 10.0 CIDRAM v3

Ada perbedaan yang signifikan antara v3 dan versi utama sebelumnya. Cara kerja titik masuk, cara menyusun modul, dan cara kerja pembaru untuk v3 berbeda dengan cara kerja hal-hal tersebut untuk versi utama sebelumnya. Karena perbedaan ini, cara terbaik untuk memutakhirkan ke v3 dari versi utama sebelumnya adalah dengan melakukan penginstalan baru.

Jika Anda ingin mempertahankan konfigurasi dan aturan tambahan Anda, sebelum memulai proses pemutakhiran, buka halaman backup dari front-end. Dari sana, konfigurasi dan aturan tambahan dapat diekspor. Mengekspor akan menyebabkan file diunduh. Setelah memutakhirkan ke versi utama yang baru, file tersebut dapat digunakan untuk mengimpor data yang diekspor sebelumnya ke penginstalan baru.

Karena perubahan struktur modul, modul yang dimaksudkan untuk versi utama sebelumnya perlu ditulis ulang agar berfungsi dengan baik untuk v3. Migrasi langsung tidak akan berhasil. Hal yang sama berlaku untuk acara.

Struktur file tanda tangan tidak berubah, jadi file tanda tangan yang dimaksudkan untuk versi utama sebelumnya dapat langsung dimigrasikan ke v3 tanpa mengantisipasi masalah.

Modul, file tanda tangan, dan acara masing-masing memiliki direktori tersendiri, yang merupakan tambahan baru sejak v3 (jadi, untuk v3, mereka masing-masing akan masuk ke direktori masing-masing, bukan ke root vault).

Beberapa file tanda tangan, modul, dan daftar blokir yang tersedia untuk umum untuk versi utama sebelumnya telah dihentikan, jadi tidak semuanya akan tersedia untuk v3. Dalam kebanyakan kasus, mereka tidak akan diperlukan, karena fitur baru dan fungsionalitas ditambahkan sejak v3.

Ada beberapa perubahan halus pada struktur aturan tambahan, dan ada perubahan pada konfigurasi, tetapi jika Anda menggunakan fitur impor/ekspor di halaman backup dari front-end, Anda tidak perlu menulis ulang, menyesuaikan, atau membuat ulang apapun secara manual. Saat mengimpor, CIDRAM mengetahui apa yang dibutuhkan, dan akan menanganinya untuk Anda secara otomatis.

#### 10.1 CIDRAM v4

CIDRAM v4 belum ada. Namun, ketika saatnya tiba untuk memutakhirkan dari v3 ke v4, proses pemutakhiran seharusnya jauh lebih sederhana. Kami tidak akan tahu persis seberapa signifikan perbedaannya sampai saatnya tiba, tetapi saya memperkirakan perbedaannya akan jauh lebih sedikit dari sebelumnya, dan mekanisme telah diterapkan ke v3 sejak awal untuk memfasilitasi proses pemutakhiran yang lebih lancar. Selama tidak ada perubahan signifikan pada pembaru atau cara kerja titik masuk, secara teori, dimungkinkan untuk memutakhirkan seluruhnya melalui front-end, tanpa perlu melakukan penginstalan baru.

Informasi lebih rinci akan disertakan disini, dalam dokumentasi, pada waktu yang tepat di masa mendatang.

---


Terakhir Diperbarui: 9 Agustus 2025 (2025.08.09).

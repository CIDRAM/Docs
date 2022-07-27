## Dokumentasi untuk CIDRAM v2 (Bahasa Indonesia).

### Isi
- 1. [SEPATAH KATA](#SECTION1)
- 2. [BAGAIMANA CARA MENGINSTAL](#SECTION2)
- 3. [BAGAIMANA CARA MENGGUNAKAN](#SECTION3)
- 4. [MANAJEMEN BAGIAN DEPAN](#SECTION4)
- 5. [FILE YANG DIIKUTKAN DALAM PAKET INI](#SECTION5)
- 6. [OPSI KONFIGURASI](#SECTION6)
- 7. [FORMAT TANDA TANGAN](#SECTION7)
- 8. [MASALAH KOMPATIBILITAS DIKETAHUI](#SECTION8)
- 9. [PERTANYAAN YANG SERING DIAJUKAN (FAQ)](#SECTION9)
- 10. *Dicadangkan untuk penambahan dokumentasi di masa mendatang.*
- 11. [INFORMASI HUKUM](#SECTION11)

*Catatan tentang terjemahan: Dalam hal kesalahan (misalnya, perbedaan antara terjemahan, kesalahan cetak, dll), versi bahasa Inggris dari README dianggap versi asli dan berwibawa. Jika Anda menemukan kesalahan, bantuan Anda dalam mengoreksi mereka akan disambut.*

---


### 1. <a name="SECTION1"></a>SEPATAH KATA

CIDRAM (Classless Inter-Domain Routing Access Manager) adalah skrip PHP dirancang untuk melindungi situs oleh memblokir permintaan-permintaan berasal dari alamat IP yang dianggap sumber lalu lintas yang tidak diinginkan, termasuk (tapi tidak terbatas pada) lalu lintas dari jalur akses yang tidak manusia, layanan cloud, spambots, pencakar/scrapers, dll. Hal ini dilakukan melalui menghitung kisaran CIDR alamat IP dipasok dari permintaan dan mencoba untuk mencocokkan ini kisaran CIDR terhadap file tanda tangan (file tanda tangan ini berisi daftar CIDR alamat IP dianggap sumber lalu lintas yang tidak diinginkan); Jika dicocokkan, permintaan yang diblokir.

*(Lihat: [Apa yang "CIDR"?](#WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) HAK CIPTA 2016 dan di atas GNU/GPLv2 oleh [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Skrip ini adalah perangkat lunak gratis; Anda dapat mendistribusikan kembali dan/atau memodifikasinya dalam batasan dari GNU General Public License, seperti di publikasikan dari Free Software Foundation; baik versi 2 dari License, atau (dalam opsi Anda) versi selanjutnya apapun. Skrip ini didistribusikan untuk harapan dapat digunakan tapi TANPA JAMINAN; tanpa walaupun garansi dari DIPERJUALBELIKAN atau KECOCOKAN UNTUK TUJUAN TERTENTU. Mohon Lihat GNU General Public Licence untuk lebih detail, terletak di file `LICENSE.txt` dan tersedia juga dari:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Dokumen ini dan paket terhubung di dalamnya dapat di unduh secara gratis dari:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>BAGAIMANA CARA MENGINSTAL

#### 2.0 MENGINSTAL SECARA MANUAL

1) Dengan membaca ini, Saya asumsikan Anda telah mengunduh dan menyimpan copy dari skrip, membuka data terkompres dan isinya dan Anda meletakkannya pada mesin komputer lokal Anda. Dari sini, Anda akan latihan dimana di host Anda atau CMS Anda untuk meletakkan isi data terkompres nya. Sebuah direktori seperti `/public_html/cidram/` atau yang lain (walaupun tidak masalah Anda memilih direktori apa, selama dia aman dan dimana pun yang Anda senangi) akan mencukupi. *Sebelum Anda mulai upload, mohon baca dulu..*

2) Mengubah file nama `config.ini.RenameMe` ke `config.ini` (berada di dalam `vault`), dan secara fakultatif (sangat direkomendasikan untuk user dengan pengalaman lebih lanjut, tapi tidak untuk pemula atau yang tidak berpengalaman), membukanya (file ini berisikan semua opsi operasional yang tersedia untuk CIDRAM; di atas tiap opsi seharusnya ada komentar tegas menguraikan tentang apa yang dilakukan dan untuk apa). Atur opsi-opsi ini seperti Anda lihat cocok, seperti apapun yang cocok untuk setup tertentu. Simpan file, menutupnya.

3) Upload isi (CIDRAM dan file-filenya) ke direktori yang telah kamu putuskan sebelumnya (Anda tidak memerlukan file-file `*.txt`/`*.md`, tapi kebanyakan Anda harus mengupload semuanya).

4) Gunakan perinta CHMOD ke direktori `vault` dengan "755" (jika ada masalah, Anda dapat mencoba "777", tapi ini kurang aman). Direktori utama menyimpan isinya (yang Anda putuskan sebelumnya), umumnya dapat di biarkan sendirian, tapi status perintah "CHMOD" seharusnya di cek jika kamu punya izin di sistem Anda (defaultnya, seperti "755"). Pendeknya: Agar paket berfungsi dengan benar, PHP harus dapat membaca dan menulis file di dalam direktori `vault`. Banyak hal (memperbarui, pencatatan, dll) tidak akan mungkin, jika PHP tidak dapat menulis ke direktori `vault`, dan paket tidak akan berfungsi sama sekali jika PHP tidak dapat membaca dari direktori `vault`. Namun, untuk keamanan optimal, direktori `vault` TIDAK harus dapat diakses publik (informasi sensitif, seperti informasi yang dikandung oleh `config.ini` atau `frontend.dat`, dapat diekspos kepada penyerang potensial jika direktori `vault` dapat diakses oleh publik).

5) Selanjutnya Anda perlu menghubungkan CIDRAM ke sistem atau CMS. Ada beberapa cara yang berbeda untuk menghubungkan skrip seperti CIDRAM ke sistem atau CMS, tapi yang paling mudah adalah memasukkan skrip pada permulaan dari file murni dari sistem atau CMS (satu yang akan secara umum di muat ketika seseorang mengakses halaman apapun pada situs web) berdasarkan pernyataan `require` atau `include`. Umumnya, ini akan menjadi sesuatu yang disimpan di sebuah direktori seperti `/includes`, `/assets` atau `/functions` dan akan selalu di namai sesuatu seperti `init.php`, `common_functions.php`, `functions.php` atau yang sama. Anda harus bekerja pada file apa untuk situasi ini; Jika Anda mengalami kesulitan dalam menentukan ini untuk diri sendiri, kunjungi halaman issues (issues) CIDRAM di GitHub untuk bantuan. Untuk melakukannya [menggunakan `require` atau `include`], sisipkan baris kode dibawah pada file murni, menggantikan kata-kata berisikan didalam tanda kutip dari alamat file `loader.php` (alamat lokal, tidak alamat HTTP; akan terlihat seperti alamat vault yang di bicarakan sebelumnya).

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

Simpan file dan tutup. Upload kembali.

-- ATAU ALTERNATIF --

Jika Anda menggunakan webserver Apache dan jika Anda memiliki akses ke `php.ini`, Anda dapat menggunakan `auto_prepend_file` direktif untuk tambahkan CIDRAM setiap kali ada permintaan PHP dibuat. Sesuatu seperti:

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

Atau ini di file `.htaccess`:

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

6) Itu semuanya! :-)

#### 2.1 MENGINSTAL DENGAN COMPOSER

[CIDRAM terdaftar dengan Packagist](https://packagist.org/packages/cidram/cidram). Jika Anda akrab dengan Composer, Anda dapat menggunakan Composer untuk menginstal CIDRAM (Anda masih perlu mempersiapkan konfigurasi, izin dan kait meskipun; melihat "menginstal secara manual" langkah 2, 4, dan 5).

`composer require cidram/cidram`

#### 2.2 MENGINSTAL UNTUK WORDPRESS

Jika Anda ingin menggunakan CIDRAM dengan WordPress, Anda dapat mengabaikan semua petunjuk di atas. [CIDRAM terdaftar sebagai plugin dengan database plugin WordPress](https://wordpress.org/plugins/cidram/), dan Anda dapat menginstal CIDRAM langsung dari plugin dashboard. Anda dapat menginstalnya dengan cara yang sama seperti plugin lainnya, dan tidak ada langkah-langkah selain diperlukan. Sama seperti dengan metode instalasi lain, Anda dapat menyesuaikan instalasi Anda dengan memodifikasi isi file `config.ini` atau dengan menggunakan akses bagian depan halaman konfigurasi. Jika Anda mengaktifkan bagian depan CIDRAM dan memperbarui CIDRAM menggunakan akses bagian depan halaman pembaruan, ini secara otomatis akan sinkron dengan informasi versi plugin ditampilkan di plugin dashboard.

*Peringatan: Memperbarui CIDRAM melalui dashboard plugin menghasilkan instalasi yang bersih! Jika Anda telah menyesuaikan instalasi Anda (mengubah konfigurasi, modul terinstal, dll), kustomisasi ini akan hilang saat memperbarui melalui dashboard plugin! File log juga akan hilang saat memperbarui melalui dashboard plugin! Untuk menyimpan file log dan kustomisasi, perbarui melalui halaman pembaruan bagian depan CIDRAM.*

---


### 3. <a name="SECTION3"></a>BAGAIMANA CARA MENGGUNAKAN

CIDRAM harus secara otomatis memblokir permintaan yang tidak diinginkan ke website Anda tanpa memerlukan bantuan manual, selain dari instalasi.

Anda dapat menyesuaikan konfigurasi Anda dan menyesuaikan apa CIDRs diblokir oleh memodifikasi file konfigurasi Anda dan/atau file tanda tangan Anda.

Jika Anda menemukan positif palsu, tolong hubungi saya untuk membiarkan saya tahu tentang hal itu. *(Lihat: [Apa yang dimaksud dengan "positif palsu"?](#WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM dapat diperbarui secara manual atau melalui bagian depan. CIDRAM juga bisa diperbarui via Composer atau WordPress, jika sudah diinstal dengan cara ini.

---


### 4. <a name="SECTION4"></a>MANAJEMEN BAGIAN DEPAN

#### 4.0 APA YANG MANAJEMEN BAGIAN DEPAN.

Manajemen bagian depan menyediakan cara yang nyaman dan mudah untuk mempertahankan, mengelola, dan memperbarui instalasi CIDRAM Anda. Anda dapat melihat, berbagi, dan download file log melalui halaman log, Anda dapat mengubah konfigurasi melalui halaman konfigurasi, Anda dapat instal dan uninstal/hapus komponen melalui halaman pembaruan, dan Anda dapat upload, download, dan memodifikasi file dalam vault Anda melalui file manager.

Bagian depan adalah dinonaktifkan secara default untuk mencegah akses yang tidak sah (akses yang tidak sah bisa memiliki konsekuensi yang signifikan untuk website Anda dan keamanannya). Instruksi untuk mengaktifkannya termasuk dibawah paragraf ini.

#### 4.1 BAGAIMANA CARA MENGAKTIFKAN MANAJEMEN BAGIAN DEPAN.

1) Menemukan direktif `disable_frontend` dalam `config.ini`, dan mengaturnya untuk `false` (akan menjadi `true` secara default).

2) Mengakses `loader.php` dari browser Anda (misalnya, `http://localhost/cidram/loader.php`).

3) Masuk dengan nama pengguna dan kata sandi default (admin/password).

Catat: Setelah Anda dimasukkan untuk pertama kalinya, untuk mencegah akses tidak sah ke manajemen bagian depan, Anda harus segera mengubah nama pengguna dan kata sandi Anda! Ini sangat penting, karena itu mungkin untuk meng-upload kode PHP sewenang-wenang untuk situs web Anda melalui bagian depan.

Juga, untuk keamanan yang optimal, memungkinkan "otentikasi dua faktor" untuk semua akun bagian depan sangat disarankan (petunjuk disediakan dibawah).

#### 4.2 BAGAIMANA CARA MENGGUNAKAN MANAJEMEN BAGIAN DEPAN.

Instruksi disediakan pada setiap halaman dari manajemen bagian depan, untuk menjelaskan cara yang benar untuk menggunakannya dan tujuan yang telah ditetapkan. Jika Anda membutuhkan penjelasan lebih lanjut atau bantuan khusus, silahkan hubungi dukungan, atau sebagai pilihan lain, ada beberapa video yang tersedia di YouTube yang dapat membantu dengan cara demonstrasi.

#### 4.3 OTENTIKASI DUA FAKTOR

Mungkin untuk membuat bagian depan lebih aman dengan mengaktifkan otentikasi dua faktor ("2FA"). Saat masuk ke akun berkemampuan 2FA, email dikirim ke alamat email yang terkait dengan akun tersebut. Email ini berisi "kode 2FA", yang kemudian harus dimasukkan oleh pengguna, selain nama pengguna dan kata sandi, agar dapat masuk menggunakan akun tersebut. Ini berarti bahwa mendapatkan kata sandi akun tidak akan cukup bagi peretas atau penyerang potensial untuk dapat masuk ke akun tersebut, karena mereka juga harus sudah memiliki akses ke alamat email yang terkait dengan akun tersebut agar dapat menerima dan memanfaatkan kode 2FA yang terkait dengan sesi, sehingga membuat bagian depan lebih aman.

Pertama, untuk mengaktifkan otentikasi dua faktor, menggunakan halaman pembaruan bagian depan, instal komponen PHPMailer. CIDRAM menggunakan PHPMailer untuk mengirim email. Perlu dicatat bahwa meskipun CIDRAM, dengan sendirinya, kompatibel dengan PHP >= 5.4.0, PHPMailer membutuhkan PHP >= 5.5.0, dengan demikian berarti bahwa mengaktifkan otentikasi dua faktor untuk bagian depan CIDRAM tidak akan mungkin bagi pengguna PHP 5.4.

Setelah Anda menginstal PHPMailer, Anda harus mengisi direktif konfigurasi untuk PHPMailer melalui halaman konfigurasi CIDRAM atau file konfigurasi. Informasi lebih lanjut tentang direktif konfigurasi ini termasuk dalam bagian konfigurasi dokumen ini. Setelah Anda mengisi direktif konfigurasi PHPMailer, atur `enable_two_factor` ke `true`. Otentikasi dua faktor sekarang harus diaktifkan.

Selanjutnya, Anda harus mengaitkan alamat email dengan akun, sehingga CIDRAM tahu ke mana harus mengirim 2FA kode ketika masuk dengan akun tersebut. Untuk melakukan ini, gunakan alamat email sebagai nama pengguna untuk akun tersebut (seperti `foo@bar.tld`), atau sertakan alamat email sebagai bagian dari nama pengguna dengan cara yang sama seperti ketika mengirim email secara normal (seperti `Foo Bar <foo@bar.tld>`).

Catat: Melindungi vault Anda terhadap akses yang tidak sah (misalnya, dengan memperketat keamanan server Anda dan izin akses publik), sangat penting disini, karena akses tidak sah ke file konfigurasi Anda (yang disimpan dalam vault Anda), dapat berisiko mengekspos konfigurasi SMTP Anda (termasuk nama pengguna dan kata sandi SMTP). Anda harus memastikan bahwa vault Anda diamankan dengan benar sebelum mengaktifkan otentikasi dua faktor. Jika Anda tidak dapat melakukan ini, setidaknya Anda harus membuat akun email baru, yang didedikasikan untuk tujuan ini, untuk mengurangi risiko yang terkait dengan konfigurasi SMTP yang diekspos.

---


### 5. <a name="SECTION5"></a>FILE YANG DIIKUTKAN DALAM PAKET INI

```
https://github.com/CIDRAM/CIDRAM>v2
│   .gitattributes
│   .gitignore
│   Changelog.txt
│   composer.json
│   LICENSE.txt
│   loader.php
│   README.md
│   tests.php
├───.docker
│       docker-compose.yml
├───.github
│   │   FUNDING.yml
│   │
│   └───workflows
│           php-cs-fixer.yml
│           v2.yml
└───vault
    │   bypasses.php
    │   bypasses.yml
    │   captcha_default.html
    │   channels.yaml
    │   cidramblocklists.dat
    │   components.dat
    │   config.ini.RenameMe
    │   config.php
    │   config.yaml
    │   event_handlers.php
    │   frontend.php
    │   frontend_functions.php
    │   functions.php
    │   ignore.dat
    │   ipv4.dat
    │   ipv4_bogons.dat
    │   ipv4_custom.dat.RenameMe
    │   ipv4_isps.dat
    │   ipv4_nonblocking.dat
    │   ipv4_other.dat
    │   ipv6.dat
    │   ipv6_bogons.dat
    │   ipv6_custom.dat.RenameMe
    │   ipv6_isps.dat
    │   ipv6_nonblocking.dat
    │   ipv6_other.dat
    │   lang.php
    │   modules.dat
    │   outgen.php
    │   template_custom.html
    │   template_default.html
    │   themes.dat
    │   verification.yaml
    ├───classes
    │   │   Aggregator.php
    │   │   Captcha.php
    │   │   Constants.php
    │   │   HCaptcha.php
    │   │   ReCaptcha.php
    │   │   Reporter.php
    │   │
    │   └───Maikuolan
    │           Cache.php
    │           ComplexStringHandler.php
    │           DelayedIO.php
    │           Demojibakefier.php
    │           Events.php
    │           IPHeader.php
    │           L10N.php
    │           Matrix.php
    │           NumberFormatter.php
    │           Operation.php
    │           Request.php
    │           YAML.php
    ├───fe_assets
    │       auxiliary.js
    │       frontend.css
    │       frontend.html
    │       icons.php
    │       lock_bl_c.png
    │       lock_bl_o.png
    │       lock_rd_c.png
    │       lock_rd_o.png
    │       lock_wt_c.png
    │       lock_wt_o.png
    │       pips.php
    │       scripts.js
    │       _2fa.html
    │       _accounts.html
    │       _accounts_row.html
    │       _aux.html
    │       _aux_edit.html
    │       _cache.html
    │       _cidr_calc.html
    │       _cidr_calc_row.html
    │       _config.html
    │       _config_row.html
    │       _files.html
    │       _files_edit.html
    │       _files_rename.html
    │       _files_row.html
    │       _fixer.html
    │       _home.html
    │       _ip_aggregator.html
    │       _ip_test.html
    │       _ip_test_row.html
    │       _ip_tracking.html
    │       _ip_tracking_row.html
    │       _login.html
    │       _logs.html
    │       _nav_complete_access.html
    │       _nav_logs_access_only.html
    │       _range.html
    │       _range_intersector.html
    │       _range_row.html
    │       _range_subtractor.html
    │       _sections.html
    │       _statistics.html
    │       _updates.html
    │       _updates_row.html
    └───lang
            lang.ar.fe.yaml
            lang.ar.yaml
            lang.bn.fe.yaml
            lang.bn.yaml
            lang.de.fe.yaml
            lang.de.yaml
            lang.en.fe.yaml
            lang.en.yaml
            lang.es.fe.yaml
            lang.es.yaml
            lang.fr.fe.yaml
            lang.fr.yaml
            lang.hi.fe.yaml
            lang.hi.yaml
            lang.id.fe.yaml
            lang.id.yaml
            lang.it.fe.yaml
            lang.it.yaml
            lang.ja.fe.yaml
            lang.ja.yaml
            lang.ko.fe.yaml
            lang.ko.yaml
            lang.lv.fe.yaml
            lang.lv.yaml
            lang.nl.fe.yaml
            lang.nl.yaml
            lang.no.fe.yaml
            lang.no.yaml
            lang.pl.fe.yaml
            lang.pl.yaml
            lang.pt.fe.yaml
            lang.pt.yaml
            lang.ru.fe.yaml
            lang.ru.yaml
            lang.sv.fe.yaml
            lang.sv.yaml
            lang.ta.fe.yaml
            lang.ta.yaml
            lang.th.fe.yaml
            lang.th.yaml
            lang.tr.fe.yaml
            lang.tr.yaml
            lang.ur.fe.yaml
            lang.ur.yaml
            lang.vi.fe.yaml
            lang.vi.yaml
            lang.zh-tw.fe.yaml
            lang.zh-tw.yaml
            lang.zh.fe.yaml
            lang.zh.yaml
```

---


### 6. <a name="SECTION6"></a>OPSI KONFIGURASI

Berikut list variabel yang ditemukan pada file konfigurasi CIDRAM `config.ini`, dengan deskripsi dari tujuan dan fungsi.

```
Configuration (v2)
├───general
│       logfile
│       logfile_apache (v1: logfileApache)
│       logfile_serialized (v1: logfileSerialized)
│       error_log
│       error_log_stages
│       truncate
│       log_rotation_limit
│       log_rotation_action
│       timezone
│       time_offset (v1: timeOffset)
│       time_format (v1: timeFormat)
│       ipaddr
│       forbid_on_block
│       silent_mode
│       lang
│       lang_override
│       numbers
│       emailaddr
│       emailaddr_display_style
│       † (v1: disable_cli)
│       disable_frontend
│       max_login_attempts
│       frontend_log (v1: FrontEndLog)
│       signatures_update_event_log
│       ban_override
│       log_banned_ips
│       default_dns
│       search_engine_verification
│       social_media_verification
│       other_verification
│       protect_frontend
│       disable_webfonts
│       maintenance_mode
│       default_algo
│       statistics
│       force_hostname_lookup
│       allow_gethostbyaddr_lookup
│       hide_version
│       empty_fields
│       log_sanitisation
│       disabled_channels
│       default_timeout
│       config_imports
│       events
├───signatures
│       ipv4
│       ipv6
│       block_attacks
│       block_cloud
│       block_bogons
│       block_generic
│       block_legal
│       block_malware
│       block_proxies
│       block_spam
│       modules
│       default_tracktime
│       infraction_limit
│       track_mode
│       tracking_override
├───recaptcha
│       usemode
│       lockip
│       lockuser
│       sitekey
│       secret
│       expiry
│       logfile
│       signature_limit
│       api
│       show_cookie_warning
│       show_api_message
│       nonblocked_status_code
├───hcaptcha
│       usemode
│       lockip
│       lockuser
│       sitekey
│       secret
│       expiry
│       logfile
│       signature_limit
│       api
│       show_cookie_warning
│       show_api_message
│       nonblocked_status_code
├───legal
│       pseudonymise_ip_addresses
│       omit_ip
│       omit_hostname
│       omit_ua
│       privacy_policy
├───template_data
│       theme
│       magnification (v1: Magnification)
│       css_url
├───PHPMailer
│       event_log (v1: EventLog)
│       skip_auth_process (v1: SkipAuthProcess)
│       enable_two_factor (v1: Enable2FA)
│       host (v1: Host)
│       port (v1: Port)
│       smtp_secure (v1: SMTPSecure)
│       smtp_auth (v1: SMTPAuth)
│       username (v1: Username)
│       password (v1: Password)
│       set_from_address (v1: setFromAddress)
│       set_from_name (v1: setFromName)
│       add_reply_to_address (v1: addReplyToAddress)
│       add_reply_to_name (v1: addReplyToName)
├───rate_limiting
│       max_bandwidth
│       max_requests
│       precision_ipv4
│       precision_ipv6
│       allowance_period
│       exceptions
└───supplementary_cache_options
        prefix
        enable_apcu
        enable_memcached
        enable_redis
        enable_pdo
        memcached_host
        memcached_port
        redis_host
        redis_port
        redis_timeout
        pdo_dsn
        pdo_username
        pdo_password
```

#### "general" (Kategori)
Konfigurasi umum dari CIDRAM.

##### "logfile"
- File yang dapat dibaca oleh manusia untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "logfile_apache"
- *v1: "logfileApache"*
- File yang dalam gaya Apache untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "logfile_serialized"
- *v1: "logfileSerialized"*
- File serial untuk mencatat semua upaya akses diblokir. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

*Tip berguna: Jika Anda mau, Anda dapat menambahkan informasi tanggal/waktu untuk nama-nama file log Anda oleh termasuk ini dalam nama: `{yyyy}` untuk tahun lengkap, `{yy}` untuk tahun disingkat, `{mm}` untuk bulan, `{dd}` untuk hari, `{hh}` untuk jam.*

*Contoh:*
- *`logfile='logfile.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_apache='access.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_serialized='serial.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "error_log"
- File untuk mencatat kesalahan tidak fatal yang terdeteksi. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "error_log_stages"
- Daftar tahapan dalam rantai eksekusi yang seharusnya memiliki kesalahan yang dihasilkan dicatat.
- *Default: "Tests,Modules,SearchEngineVerification,SocialMediaVerification,OtherVerification,Aux,Reporting,Tracking,RL,CAPTCHA,Statistics,Webhooks,Output,NonBlockedCAPTCHA"*

##### "truncate"
- Memotong file log ketika mereka mencapai ukuran tertentu? Nilai adalah ukuran maksimum dalam B/KB/MB/GB/TB yang bisa ditambahkan untuk file log sebelum dipotong. Nilai default 0KB menonaktifkan pemotongan (file log dapat tumbuh tanpa batas waktu). Catat: Berlaku untuk file log individu! Ukuran file log tidak dianggap secara kolektif.

##### "log_rotation_limit"
- Rotasi log membatasi jumlah file log yang seharusnya ada pada satu waktu. Ketika file log baru dibuat, jika jumlah total file log melebihi batas yang ditentukan, tindakan yang ditentukan akan dilakukan. Anda dapat menentukan batas yang diinginkan disini. Nilai 0 akan menonaktifkan rotasi log.

##### "log_rotation_action"
- Rotasi log membatasi jumlah file log yang seharusnya ada pada satu waktu. Ketika file log baru dibuat, jika jumlah total file log melebihi batas yang ditentukan, tindakan yang ditentukan akan dilakukan. Anda dapat menentukan tindakan yang diinginkan disini. Delete = Hapus file log tertua, hingga batasnya tidak lagi terlampaui. Archive = Pertama arsipkan, lalu hapus file log tertua, hingga batasnya tidak lagi terlampaui.

*Klarifikasi teknis: Dalam konteks ini, "tertua" berarti tidak dimodifikasi baru-baru.*

##### "timezone"
- Ini digunakan untuk menentukan zona waktu mana yang harus digunakan oleh CIDRAM untuk operasi tanggal/waktu. Jika Anda tidak membutuhkannya, abaikan saja. Nilai yang mungkin ditentukan oleh PHP. Ini umumnya direkomendasikan sebagai gantinya untuk menyesuaikan direktif zona waktu dalam file `php.ini` Anda, tapi terkadang (seperti ketika bekerja dengan terbatas penyedia shared hosting) ini tidak selalu mungkin untuk melakukan, dan demikian, opsi ini disediakan disini.

##### "time_offset"
- *v1: "timeOffset"*
- Jika waktu server Anda tidak cocok waktu lokal Anda, Anda dapat menentukan offset sini untuk menyesuaikan informasi tanggal/waktu dihasilkan oleh CIDRAM sesuai dengan kebutuhan Anda. Ini umumnya direkomendasikan sebagai gantinya untuk menyesuaikan direktif zona waktu dalam file `php.ini` Anda, tapi terkadang (seperti ketika bekerja dengan terbatas penyedia shared hosting) ini tidak selalu mungkin untuk melakukan, dan demikian, opsi ini disediakan disini. Offset adalah dalam menit.
- Contoh (untuk menambahkan satu jam): `time_offset=60`

##### "time_format"
- *v1: "timeFormat"*
- Format notasi tanggal/waktu yang digunakan oleh CIDRAM. Default = `{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}`.

##### "ipaddr"
- Dimana menemukan alamat IP dari permintaan alamat? (Bergunak untuk pelayanan-pelayanan seperti Cloudflare dan sejenisnya). Default = REMOTE_ADDR. PERINGATAN: Jangan ganti ini kecuali Anda tahu apa yang Anda lakukan!

Nilai yang disarankan untuk "ipaddr":

Nilai | Menggunakan
---|---
`HTTP_INCAP_CLIENT_IP` | Incapsula reverse proxy.
`HTTP_CF_CONNECTING_IP` | Cloudflare reverse proxy.
`CF-Connecting-IP` | Cloudflare reverse proxy (alternatif; jika di atas tidak bekerja).
`HTTP_X_FORWARDED_FOR` | Cloudbric reverse proxy.
`X-Forwarded-For` | [Squid reverse proxy](http://www.squid-cache.org/Doc/config/forwarded_for/).
`Forwarded` | *[Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded).*
*Ditetapkan oleh konfigurasi server.* | [Nginx reverse proxy](https://www.nginx.com/resources/admin-guide/reverse-proxy/).
`REMOTE_ADDR` | Tidak ada reverse proxy (nilai default).

##### "forbid_on_block"
- Pesan status HTTP mana yang harus dikirim oleh CIDRAM ketika memblokir permintaan?

Nilai yang didukung saat ini:

Kode status | Pesan status | Deskripsi
---|---|---
`200` | `200 OK` | Nilai default. Paling tidak kuat, tetapi paling ramah-pengguna. Permintaan otomatis kemungkinan besar akan menafsirkan respons ini sebagai indikasi bahwa permintaan berhasil.
`403` | `403 Forbidden` | Lebih kuat, tetapi kurang ramah-pengguna. Direkomendasikan untuk kebanyakan keadaan umum.
`410` | `410 Gone` | Dapat menyebabkan masalah saat menyelesaikan kesalahan positif, karena beberapa browser akan menyimpan pesan status ini di cache dan tidak mengirim permintaan berikutnya, bahkan setelah diblokir. Mungkin yang paling disukai dalam beberapa konteks, untuk jenis lalu lintas tertentu.
`418` | `418 I'm a teapot` | Referensi pada lelucon April Mop ([RFC 2324](https://tools.ietf.org/html/rfc2324#section-6.5.14)). Probabilitas rendah bahwa akan dipahami oleh klien, bot, browser, atau lainnya. Disediakan untuk hiburan dan kenyamanan, tetapi umumnya tidak direkomendasikan.
`451` | `451 Unavailable For Legal Reasons` | Direkomendasikan saat memblokir terutama karena alasan hukum. Tidak direkomendasikan dalam konteks lain.
`503` | `503 Service Unavailable` | Paling kuat, tetapi paling tidak ramah-pengguna. Direkomendasikan untuk saat diserang, atau saat berhadapan dengan lalu lintas yang tidak diinginkan yang sangat persisten.

##### "silent_mode"
- Seharusnya CIDRAM diam-diam mengarahkan diblokir upaya akses bukannya menampilkan halaman "Akses Ditolak"? Jika ya, menentukan lokasi untuk mengarahkan diblokir upaya akses. Jika tidak, kosongkan variabel ini.

##### "lang"
- Tentukan bahasa default untuk CIDRAM.

##### "lang_override"
- Melokalisasikan sesuai dengan HTTP_ACCEPT_LANGUAGE jika memungkinkan? True = Ya [Default]; False = Tidak.

##### "numbers"
- Menentukan bagaimana menampilkan nomor-nomor.

Nilai yang didukung saat ini:

Nilai | Menghasilkan | Deskripsi
---|---|---
`NoSep-1` | `1234567.89`
`NoSep-2` | `1234567,89`
`Latin-1` | `1,234,567.89` | Nilai default.
`Latin-2` | `1 234 567.89`
`Latin-3` | `1.234.567,89`
`Latin-4` | `1 234 567,89`
`Latin-5` | `1,234,567·89`
`China-1` | `123,4567.89`
`India-1` | `12,34,567.89`
`India-2` | `१२,३४,५६७.८९`
`India-3` | `૧૨,૩૪,૫૬૭.૮૯`
`India-4` | `੧੨,੩੪,੫੬੭.੮੯`
`India-5` | `೧೨,೩೪,೫೬೭.೮೯`
`India-6` | `౧౨,౩౪,౫౬౭.౮౯`
`Arabic-1` | `١٢٣٤٥٦٧٫٨٩`
`Arabic-2` | `١٬٢٣٤٬٥٦٧٫٨٩`
`Arabic-3` | `۱٬۲۳۴٬۵۶۷٫۸۹`
`Arabic-4` | `۱۲٬۳۴٬۵۶۷٫۸۹`
`Bengali-1` | `১২,৩৪,৫৬৭.৮৯`
`Burmese-1` | `၁၂၃၄၅၆၇.၈၉`
`Khmer-1` | `១.២៣៤.៥៦៧,៨៩`
`Lao-1` | `໑໒໓໔໕໖໗.໘໙`
`Thai-1` | `๑,๒๓๔,๕๖๗.๘๙`
`Thai-2` | `๑๒๓๔๕๖๗.๘๙`

*Catat: Nilai-nilai ini tidak terstandardisasi dimana pun, dan mungkin tidak akan relevan di luar paket. Juga, nilai yang didukung dapat berubah di masa depan.*

##### "emailaddr"
- Jika Anda ingin, Anda dapat menyediakan alamat email sini untuk diberikan kepada pengguna ketika diblokir, bagi mereka untuk menggunakan sebagai metode kontak untuk dukungan dan/atau bantuan untuk dalam hal mereka menjadi diblokir keliru atau diblokir oleh kesalahan. PERINGATAN: Apapun alamat email Anda menyediakan sini akan pasti diperoleh oleh spambots dan pencakar/scrapers ketika digunakan disini, dan karena itu, jika Anda ingin memberikan alamat email disini, itu sangat direkomendasikan Anda memastikan bahwa alamat email yang Anda berikan disini adalah alamat yang dapat dibuang dan/atau adalah alamat Anda tidak keberatan menjadi di-spam (dengan kata lain, Anda mungkin tidak ingin untuk menggunakan Anda alamat email yang personal primer atau bisnis primer).

##### "emailaddr_display_style"
- Bagaimana Anda lebih suka alamat email yang akan disajikan kepada pengguna? "default" = Link yang dapat diklik. "noclick" = Teks yang tidak dapat diklik.

##### "disable_cli"
- *(Dihapus sejak v2)*.
- Menonaktifkan modus CLI? Modus CLI diaktifkan secara default, tapi kadang-kadang dapat mengganggu alat pengujian tertentu (seperti PHPUnit, sebagai contoh) dan aplikasi CLI berbasis lainnya. Jika Anda tidak perlu menonaktifkan modus CLI, Anda harus mengabaikan direktif ini. False = Mengaktifkan modus CLI [Default]; True = Menonaktifkan modus CLI.

##### "disable_frontend"
- Menonaktifkan akses bagian depan? Akses bagian depan dapat membuat CIDRAM lebih mudah dikelola, tapi juga dapat menjadi potensial resiko keamanan. Itu direkomendasi untuk mengelola CIDRAM melalui bagian belakang bila mungkin, tapi akses bagian depan yang disediakan untuk saat itu tidak mungkin. Memilikinya dinonaktifkan kecuali jika Anda membutuhkannya. False = Mengaktifkan akses bagian depan; True = Menonaktifkan akses bagian depan [Default].

##### "max_login_attempts"
- Jumlah maksimum upaya memasukkan ke bagian depan. Default = 5.

##### "frontend_log"
- *v1: "FrontEndLog"*
- File untuk mencatat upaya masuk bagian depan. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "signatures_update_event_log"
- File untuk mencatat ketika tanda tangan diperbarui melalui bagian depan. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "ban_override"
- Mengesampingkan "forbid_on_block" ketika "infraction_limit" adalah melampaui? Ketika mengesampingkan: Permintaan diblokir menghasilkan halaman kosong (file template tidak digunakan). 200 = Jangan mengesampingkan [Default]. Nilai lainnya sama dengan nilai yang tersedia untuk "forbid_on_block".

##### "log_banned_ips"
- Termasuk permintaan diblokir dari IP dilarang dalam file log? True = Ya [Default]; False = Tidak.

##### "default_dns"
- Sebuah daftar dipisahkan dengan koma dari server DNS yang digunakan untuk pencarian nama host. Default = "8.8.8.8,8.8.4.4" (Google DNS). PERINGATAN: Jangan ganti ini kecuali Anda tahu apa yang Anda lakukan!

*Lihat juga: [Apa yang bisa saya gunakan untuk "default_dns"?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)*

##### "search_engine_verification"
- Mencoba memverifikasi permintaan dari mesin pencari? Verifikasi mesin pencari memastikan bahwa mereka tidak akan dilarang sebagai akibat dari melebihi batas pelanggaran (melarang mesin pencari dari situs web Anda biasanya akan memiliki efek negatif pada peringkat mesin pencari Anda, SEO, dll). Ketika diverifikasi, mesin pencari dapat diblokir seperti biasa, tapi tidak akan dilarang. Ketika tidak diverifikasi, itu mungkin bagi mereka untuk dilarang sebagai akibat dari melebihi batas pelanggaran. Juga, verifikasi mesin pencari memberikan proteksi terhadap permintaan mesin pencari palsu dan terhadap entitas yang berpotensi berbahaya yang menyamar sebagai mesin pencari (permintaan tersebut akan diblokir ketika verifikasi mesin pencari diaktifkan). True = Mengaktifkan verifikasi mesin pencari [Default]; False = Menonaktifkan verifikasi mesin pencari.

Didukung sekarang:
- __[Applebot](https://discussions.apple.com/thread/7090135)__
- __[Baiduspider/百度](https://help.baidu.com/question?prod_en=master&class=Baiduspider)__
- __[Bingbot](https://blogs.bing.com/webmaster/2012/08/31/how-to-verify-that-bingbot-is-bingbot)__
- __[DuckDuckBot](https://duckduckgo.com/duckduckbot)__
- __[Googlebot](https://support.google.com/webmasters/answer/80553?hl=en)__
- __[MojeekBot](https://www.mojeek.com/bot.html)__
- __[PetalBot](https://aspiegel.com/petalbot)__
- __[Qwantify/Bleriot](https://help.qwant.com/bot)__
- __[SeznamBot](https://napoveda.seznam.cz/en/full-text-search/seznambot-crawler/)__
- __[Sogou/搜狗](https://www.sogou.com/docs/help/webmasters.htm#07)__
- __[Yahoo/Slurp](https://help.yahoo.com/help/us/ysearch/slurp)__
- __[Yandex/Яндекс](https://yandex.com/support/webmaster/robot-workings/check-yandex-robots.xml)__
- __[Youdao/有道](https://udger.com/resources/ua-list/bot-detail?bot=YoudaoBot#id1507)__

Tidak kompatibel (menyebabkan konflik):
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

##### "social_media_verification"
- Mencoba memverifikasi permintaan media sosial? Verifikasi media sosial memberikan perlindungan terhadap permintaan media sosial palsu (permintaan semacam ini akan diblokir). True = Mengaktifkan verifikasi media sosial [Default]; False = Mengaktifkan verifikasi media sosial.

Didukung sekarang:
- __[Embedly](https://udger.com/resources/ua-list/bot-detail?bot=Embedly#id22674)__
- __** [Facebook external hit](https://developers.facebook.com/docs/sharing/webmasters/crawler/)__
- __[Pinterest](https://help.pinterest.com/en/articles/about-pinterest-crawler-0)__
- __[Twitterbot](https://udger.com/resources/ua-list/bot-detail?bot=Twitterbot#id6168)__

_**: Memerlukan fungsionalitas pencarian ASN, mis., dari modul BGPView._

##### "other_verification"
- Jika memungkinkan, coba verifikasi jenis permintaan lain (mis., AdSense, pemeriksa SEO, dll)? Saat terdeteksi, permintaan palsu akan diblokir. True = Mengaktifkan [Default]; False = Menonaktifkan.

Didukung sekarang:
- __[AdSense](https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers)__
- __[AmazonAdBot](https://adbot.amazon.com/index.html)__
- __[Oracle Data Cloud Crawler](https://www.oracle.com/corporate/acquisitions/grapeshot/crawler.html)__

##### "protect_frontend"
- Menentukan apakah perlindungan biasanya disediakan oleh CIDRAM harus diterapkan pada bagian depan. True = Ya [Default]; False = Tidak.

##### "disable_webfonts"
- Menonaktifkan webfonts? True = Ya [Default]; False = Tidak.

##### "maintenance_mode"
- Aktifkan modus perawatan? True = Ya; False = Tidak [Default]. Nonaktifkan semuanya selain bagian depan. Terkadang berguna saat memperbarui CMS, kerangka kerja, dll.

##### "default_algo"
- Mendefinisikan algoritma mana yang akan digunakan untuk semua kata sandi dan sesi di masa depan. Opsi: PASSWORD_DEFAULT (default), PASSWORD_BCRYPT, PASSWORD_ARGON2I (membutuhkan PHP >= 7.2.0), PASSWORD_ARGON2ID (membutuhkan PHP >= 7.3.0).

##### "statistics"
- Lacak statistik penggunaan CIDRAM? True = Ya; False = Tidak [Default].

##### "force_hostname_lookup"
- Memaksa periksa untuk nama host? True = Ya; False = Tidak [Default]. Periksa untuk nama host biasanya dilakukan pada dasar "sesuai kebutuhan", tapi bisa dipaksakan untuk semua permintaan. Melakukan hal tersebut mungkin berguna sebagai sarana untuk memberikan informasi lebih rinci di log, tapi mungkin juga memiliki sedikit efek negatif pada kinerja.

##### "allow_gethostbyaddr_lookup"
- Izinkan menggunakan gethostbyaddr saat UDP tidak tersedia? True = Ya [Default]; False = Tidak.
- *Catat: Pencarian IPv6 mungkin tidak bekerja dengan benar pada beberapa sistem 32-bit.*

##### "hide_version"
- Sembunyikan informasi versi dari log dan output halaman? True = Ya; False = Tidak [Default].

##### "empty_fields"
- Bagaimana seharusnya CIDRAM menangani bidang kosong saat membuat log dan menampilkan informasi kejadian blokir? "include" = Sertakan bidang kosong. "omit" = Hilangkan bidang kosong [default].

##### "log_sanitisation"
- Saat menggunakan halaman log untuk melihat data log, CIDRAM mensanitasikan data log sebelum menampilkannya, untuk melindungi pengguna dari serangan XSS dan potensi ancaman lain yang bisa terkandung dalam data. Namun, secara default, data tidak disanitasi selama pencatatan. Ini untuk memastikan bahwa data log dicatatan secara akurat, untuk membantu analisis heuristik atau forensik yang mungkin diperlukan di masa depan. Namun, jika pengguna mencoba membaca data log menggunakan alat eksternal, dan jika alat eksternal itu tidak melakukan proses sanitasi sendiri, pengguna bisa terkena serangan XSS. Jika perlu, Anda dapat mengubah perilaku default menggunakan direktif konfigurasi ini. True = Mensanitasikan data saat mencatatnya (data disimpan kurang akurat, tetapi risiko XSS lebih rendah). False = Jangan mensanitasikan data saat mencatatnya (data disimpan lebih akurat, tetapi risiko XSS lebih tinggi) [Default].

##### "disabled_channels"
- Ini dapat digunakan untuk mencegah CIDRAM dari menggunakan saluran tertentu saat mengirim permintaan (misalnya, saat memperbarui, saat mengambil metadata komponen, dll).
- *Opsi yang tersedia: `GitHub,BitBucket,GoogleDNS`*

##### "default_timeout"
- Batas waktu default untuk digunakan untuk permintaan eksternal? Default = 12 detik.

##### "config_imports"
- Sebuah daftar dipisahkan dengan koma untuk file untuk mengimpor ke konfigurasi default CIDRAM. Biasanya diisi oleh halaman pembaruan saat mengaktifkan komponen yang membutuhkannya saat diperlukan. Dalam kebanyakan kasus, bisa mengabaikannya.

##### "events"
- File yang terdaftar disini dimuat langsung setelah file pengendali acara. Biasanya diisi oleh halaman pembaruan saat mengaktifkan komponen yang membutuhkannya saat diperlukan. Dalam kebanyakan kasus, bisa mengabaikannya.

#### "signatures" (Kategori)
Konfigurasi untuk tanda tangan.

##### "ipv4"
- Daftar file tanda tangan IPv4 yang CIDRAM harus berusaha untuk menggunakan, dipisahkan dengan koma. Anda dapat menambahkan entri disini jika Anda ingin memasukkan file-file tambahan untuk CIDRAM.

##### "ipv6"
- Daftar file tanda tangan IPv6 yang CIDRAM harus berusaha untuk menggunakan, dipisahkan dengan koma. Anda dapat menambahkan entri disini jika Anda ingin memasukkan file-file tambahan untuk CIDRAM.

##### "block_attacks"
- Memblokir CIDR yang terkait dengan serangan dan lalu lintas abnormal lainnya? Misalnya, pemindaian port, peretasan, pemeriksaan kerentanan, dll. Kecuali jika Anda mengalami masalah ketika melakukan itu, umumnya, ini harus selalu didefinisikan untuk true/benar.

##### "block_cloud"
- Memblokir CIDR yang diidentifikasi sebagai milik webhosting dan/atau layanan cloud? Jika Anda mengoperasikan layanan API dari website Anda atau jika Anda mengharapkan website lain untuk menghubungkan ke website Anda, direktif ini harus didefinisikan untuk false/palsu. Jika Anda tidak, maka, direktif ini harus didefinisikan untuk true/benar.

##### "block_bogons"
- Memblokir CIDR bogon/martian? Jika Anda mengharapkan koneksi ke website Anda dari dalam jaringan lokal Anda, dari localhost, atau dari LAN Anda, direktif ini harus didefinisikan untuk false/palsu. Jika Anda tidak mengharapkan ini, direktif ini harus didefinisikan untuk true/benar.

##### "block_generic"
- Memblokir CIDR umumnya direkomendasikan untuk mendaftar hitam? Ini mencakup tanda tangan apapun yang tidak ditandai sebagai bagian dari apapun lainnya kategori tanda tangan lebih spesifik.

##### "block_legal"
- Memblokir CIDR sebagai respons terhadap kewajiban hukum? Direktif ini seharusnya tidak memiliki efek apapun, karena CIDRAM tidak menghubungkan CIDR apapun dengan "kewajiban hukum" secara default, tetapi tetap ada sebagai ukuran kontrol tambahan untuk kepentingan file tanda tangan atau modul dipersonalisasi yang mungkin ada karena alasan hukum.

##### "block_malware"
- Memblokir CIDR yang terkait dengan malware? Ini termasuk server C&C, mesin yang terinfeksi, mesin yang terlibat dalam distribusi malware, dll.

##### "block_proxies"
- Memblokir CIDR yang diidentifikasi sebagai milik layanan proxy atau VPN? Jika Anda membutuhkan bahwa pengguna dapat mengakses situs web Anda dari layanan proxy atau VPN, direktif ini harus didefinisikan untuk false/palsu. Jika Anda tidak membutuhkannya, direktif ini harus didefinisikan untuk true/benar sebagai sarana untuk meningkatkan keamanan.

##### "block_spam"
- Memblokir CIDR yang diidentifikasi sebagai beresiko tinggi karena spam? Kecuali jika Anda mengalami masalah ketika melakukan itu, umumnya, ini harus selalu didefinisikan untuk true/benar.

##### "modules"
- Daftar file modul untuk memuat setelah memeriksa tanda tangan IPv4/IPv6, dipisahkan dengan koma.

##### "default_tracktime"
- Berapa banyak detik untuk melacak IP dilarang oleh modul. Default = 604800 (1 seminggu).

##### "infraction_limit"
- Jumlah maksimum pelanggaran IP diperbolehkan untuk dikenakan sebelum dilarang oleh pelacakan IP. Default = 10.

##### "track_mode"
- Kapan sebaiknya pelanggaran dihitung? False = Ketika IP adalah diblokir oleh modul. True = Ketika IP adalah diblokir untuk alasan apapun. Default = False.

##### "tracking_override"
- Izinkan modul untuk mengganti opsi pelacakan? True = Ya [Default]; False = Tidak.

#### "recaptcha" dan "hcaptcha" (kedua kategori ini memberikan direktif-direktif yang sama).
Jika mau, Anda dapat memberikan tantangan CAPTCHA kepada pengguna untuk membedakan mereka dari bot atau untuk memungkinkan mereka mendapatkan kembali akses jika diblokir. Ini dapat membantu mengurangi positif palsu dan mengurangi lalu lintas otomatis yang tidak diinginkan.

*Catat: CAPTCHA hanya melindungi dari panggilan mesin, bukan dari penyerang manusia.*

Anda bisa mendapatkan "site key" dan "secret key" untuk reCAPTCHA dari sini:
- https://developers.google.com/recaptcha/

Anda bisa mendapatkan "site key" dan "secret key" untuk hCAPTCHA dari sini:
- https://www.hcaptcha.com/

##### "usemode"
- Kapan CAPTCHA harus ditawarkan? Catat: Permintaan yang masuk daftar putih atau diverifikasi dan tidak diblokir tidak perlu menyelesaikan CAPTCHA.

Nilai | Deskripsi
--:|:--
1 | Hanya jika diblokir, dalam batas tanda tangan, dan tidak dilarang.
2 | Hanya jika diblokir, ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.
3 | Hanya jika dalam batas tanda tangan, dan tidak dilarang (terlepas dari apakah diblokir).
4 | Hanya jika tidak diblokir.
5 | Hanya jika tidak diblokir, atau jika ditandai khusus untuk digunakan, dalam batas tanda tangan, dan tidak dilarang.
Nilai lainnya. | Tidak pernah!

##### "lockip"
- Menyatakan apakah hash harus dikunci untuk IP spesifik. False = Cookie dan hash DAPAT digunakan oleh banyak IP (default). True = Cookie dan hash TIDAK dapat digunakan oleh banyak IP (cookie/hash adalah terkunci ke IP).
- Catat: Nilai "lockip" diabaikan ketika "lockuser" adalah false, karena mekanisme untuk mengingat "pengguna" berbeda tergantung pada nilai ini.

##### "lockuser"
- Menyatakan apakah berhasil menyelesaikan instansi reCAPTCHA/hCAPTCHA harus dikunci untuk pengguna spesifik. False = Berhasil menyelesaikan instansi reCAPTCHA/hCAPTCHA akan memberikan akses ke semua permintaan yang berasal dari IP digunakan oleh pengguna yang menyelesaikan instansi reCAPTCHA/hCAPTCHA; Cookie dan hash tidak digunakan; Sebaliknya, sebuah daftar putih IP akan digunakan. True = Berhasil menyelesaikan instansi reCAPTCHA/hCAPTCHA hanya akan memberikan akses kepada pengguna yang menyelesaikan instansi reCAPTCHA/hCAPTCHA; Cookie dan hash digunakan untuk mengingat pengguna; Daftar putih IP tidak digunakan (default).

##### "sitekey"
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

##### "secret"
- Nilai ini dapat ditemukan di dashboard untuk layanan CAPTCHA Anda.

##### "expiry"
- Jumlah jam untuk mengingat instansi CAPTCHA. Default = 720 (1 bulan).

##### "logfile"
- Mencatat hasil semua instansi CAPTCHA? Jika ya, tentukan nama untuk menggunakan untuk file catatan. Jika tidak, variabel ini harus kosong.

*Tip berguna: Jika Anda mau, Anda dapat menambahkan informasi tanggal/waktu untuk nama-nama file log Anda oleh termasuk ini dalam nama: `{yyyy}` untuk tahun lengkap, `{yy}` untuk tahun disingkat, `{mm}` untuk bulan, `{dd}` untuk hari, `{hh}` untuk jam.*

*Contoh:*
- *`logfile='captcha.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "signature_limit"
- Jumlah maksimum tanda tangan yang diperbolehkan sebelum penawaran CAPTCHA ditarik. Default = 1.

##### "api"
- API mana yang akan digunakan?

```
api
├─recaptcha
│ ├─V2
│ └─Invisible
└─hcaptcha
  ├─V1
  └─Invisible
```

*Catat untuk pengguna di Uni Eropa: Saat CIDRAM dikonfigurasi untuk menggunakan cookie (mis., ketika "lockuser" true/benar), peringatan cookie ditampilkan secara mencolok di halaman sesuai persyaratan [hukum-hukum cookie UE](https://www.cookielaw.org/the-cookie-law/). Namun, saat menggunakan API invisible, CIDRAM berupaya menyelesaikan CAPTCHA untuk pengguna secara otomatis, dan bila berhasil, ini bisa mengakibatkan halaman menjadi reload dan cookie dibuat tanpa pengguna diberi waktu yang cukup untuk benar-benar melihat peringatan cookie.*

##### "show_cookie_warning"
- Tampilkan peringatan cookie? True = Ya [Default]; False = Tidak.

*Direktif konfigurasi ini ditambahkan oleh permintaan, untuk pengguna yang ingin menonaktifkan peringatan cookie biasanya ditampilkan bersama CAPTCHA (mis., untuk membantu menyembunyikan indikasi bahwa CIDRAM sedang digunakan). Namun, saya sangat menyarankan agar sebagian besar pengguna (terutama yang berbasis di UE) tetap mengaktifkannya.*

##### "show_api_message"
- Tampilkan pesan API? True = Ya [Default]; False = Tidak.

*Ini mengacu pada pesan tambahan yang tidak penting yang ditampilkan saat permintaan diblokir, kecuali untuk peringatan cookie.*

##### "nonblocked_status_code"
- Kode status mana yang harus digunakan saat menampilkan CAPTCHA ke permintaan yang tidak diblokir?

Nilai yang didukung saat ini:

Kode status | Pesan status
---|---
`200` | `200 OK`
`403` | `403 Forbidden`
`418` | `418 I'm a teapot`
`429` | `429 Too Many Requests`
`451` | `451 Unavailable For Legal Reasons`

#### "legal" (Kategori)
Konfigurasi yang berkaitan dengan persyaratan hukum.

*Untuk informasi lebih lanjut tentang persyaratan hukum dan bagaimana ini dapat mempengaruhi persyaratan konfigurasi Anda, silahkan lihat bagian "[LEGAL INFORMATION](#SECTION11)" pada dokumentasi.*

##### "pseudonymise_ip_addresses"
- Pseudonymise alamat IP saat menulis file log? True = Ya [Default]; False = Tidak.

##### "omit_ip"
- Jangan memasukkan alamat IP di log? True = Ya; False = Tidak [Default]. Catat: "pseudonymise_ip_addresses" menjadi tidak perlu ketika "omit_ip" adalah "true".

##### "omit_hostname"
- Jangan memasukkan nama host di log? True = Ya; False = Tidak [Default].

##### "omit_ua"
- Jangan memasukkan agen pengguna di log? True = Ya; False = Tidak [Default].

##### "privacy_policy"
- Alamat dari kebijakan privasi yang relevan untuk ditampilkan di footer dari setiap halaman yang dihasilkan. Spesifikasikan URL, atau biarkan kosong untuk menonaktifkan.

#### "template_data" (Kategori)
Direktif-direktif dan variabel-variabel untuk template-template dan tema-tema.

Berkaitan dengan HTML digunakan untuk menghasilkan halaman "Akses Ditolak". Jika Anda menggunakan tema kustom untuk CIDRAM, HTML diproduksi yang bersumber dari file `template_custom.html`, dan sebaliknya, HTML diproduksi yang bersumber dari file `template.html`. Variabel ditulis untuk file konfigurasi bagian ini yang diurai untuk HTML diproduksi dengan cara mengganti nama-nama variabel dikelilingi dengan kurung keriting ditemukan dalam HTML diproduksi dengan file variabel sesuai. Sebagai contoh, dimana `foo="bar"`, setiap terjadinya `<p>{foo}</p>` ditemukan dalam HTML diproduksi akan menjadi `<p>bar</p>`.

##### "theme"
- Tema default untuk CIDRAM.

##### "magnification"
- *v1: "Magnification"*
- Perbesaran font. Default = 1.

##### "css_url"
- File template untuk tema kustom menggunakan properti CSS eksternal, sedangkan file template untuk tema default menggunakan properti CSS internal. Untuk menginstruksikan CIDRAM menggunakan file template untuk tema kustom, menentukan alamat HTTP publik file CSS tema kustom Anda menggunakan variable `css_url`. Jika Anda biarkan kosong variabel ini, CIDRAM akan menggunakan file template untuk tema default.

#### "PHPMailer" (Kategori)
Konfigurasi PHPMailer.

Saat ini, CIDRAM menggunakan PHPMailer hanya untuk otentikasi dua faktor untuk bagian depan. Jika Anda tidak menggunakan bagian depan, atau jika Anda tidak menggunakan otentikasi dua-faktor untuk bagian depan, Anda dapat mengabaikan direktif ini.

##### "event_log"
- *v1: "EventLog"*
- File untuk mencatat semua kejadian yang terkait dengan PHPMailer. Spesifikasikan nama file, atau biarkan kosong untuk menonaktifkan.

##### "skip_auth_process"
- *v1: "SkipAuthProcess"*
- Pengaturan direktif ini ke `true` menginstruksikan PHPMailer untuk melewati proses otentikasi normal yang biasanya terjadi ketika mengirim email melalui SMTP. Ini harus dihindari, karena melewatkan proses ini dapat mengekspos email keluar ke serangan MITM, tetapi mungkin diperlukan dalam kasus dimana proses ini mencegah PHPMailer menghubungkan ke server SMTP.

##### "enable_two_factor"
- *v1: "Enable2FA"*
- Direktif ini menentukan apakah akan menggunakan 2FA untuk akun depan.

##### "host"
- *v1: "Host"*
- Host SMTP yang digunakan untuk email keluar.

##### "port"
- *v1: "Port"*
- Nomor port yang digunakan untuk email keluar. Default = 587.

##### "smtp_secure"
- *v1: "SMTPSecure"*
- Protokol yang digunakan saat mengirim email melalui SMTP (TLS atau SSL).

##### "smtp_auth"
- *v1: "SMTPAuth"*
- Direktif ini menentukan apakah akan mengotentikasi sesi SMTP (biasanya harus dibiarkan sendiri).

##### "username"
- *v1: "Username"*
- Nama pengguna yang digunakan saat mengirim email melalui SMTP.

##### "password"
- *v1: "Password"*
- Kata sandi yang digunakan saat mengirim email melalui SMTP.

##### "set_from_address"
- *v1: "setFromAddress"*
- Alamat pengirim yang dikutip saat mengirim email melalui SMTP.

##### "set_from_name"
- *v1: "setFromName"*
- Nama pengirim yang dikutip saat mengirim email melalui SMTP.

##### "add_reply_to_address"
- *v1: "addReplyToAddress"*
- Alamat balasan yang dikutip saat mengirim email melalui SMTP.

##### "add_reply_to_name"
- *v1: "addReplyToName"*
- Nama balasan yang dikutip saat mengirim email melalui SMTP.

#### "rate_limiting" (Kategori)
Direktif konfigurasi opsional untuk pembatasan laju.

Fitur ini diimplementasikan ke CIDRAM karena diminta oleh pengguna yang cukup untuk membenarkan diimplementasikan. Namun, karena agak tidak terkait dengan tujuan yang awalnya ditujukan untuk CIDRAM, kemungkinan besar tidak akan dibutuhkan oleh sebagian besar pengguna. Jika Anda secara khusus membutuhkan CIDRAM untuk menangani pembatasan laju untuk situs web Anda, fitur ini dapat bermanfaat bagi Anda. Namun, ada beberapa hal penting yang harus Anda pertimbangkan:
- Fitur ini, seperti semua fitur CIDRAM lainnya, hanya akan berfungsi untuk halaman yang dilindungi oleh CIDRAM. Demikian, aset situs web apapun yang tidak dirutekan secara khusus melalui CIDRAM tidak dapat dibatasi oleh CIDRAM.
- Jika Anda dapat menggunakan modul server, cPanel, atau beberapa alat jaringan lain untuk menerapkan pembatasan laju, akan lebih baik menggunakan itu untuk membatasi laju, sebagai alternatif untuk CIDRAM.
- Jika pengguna tertentu sangat tertarik untuk terus mengakses situs web Anda setelah dibatasi, dalam banyak kasus, akan sangat mudah bagi mereka untuk menghindari pembatasan laju (misalnya, jika mereka mengubah alamat IP mereka, atau jika mereka menggunakan proxy atau VPN, dan dengan asumsi Anda telah mengonfigurasi CIDRAM untuk tidak memblokir proxy dan VPN, atau bahwa CIDRAM tidak mengetahui proxy atau VPN yang mereka gunakan).
- Pembatasan laju bisa sangat mengganggu bagi pengguna sebenarnya. Mungkin diperlukan jika bandwidth yang tersedia sangat terbatas, dan jika Anda menemukan bahwa ada beberapa sumber lalu lintas khusus, yang belum diblokir, yang menghabiskan sebagian besar bandwidth yang tersedia. Namun jika tidak perlu, itu mungkin harus dihindari.
- Terkadang Anda berisiko memblokir pengguna yang sah, atau bahkan diri Anda sendiri.

Jika Anda merasa bahwa Anda tidak perlu CIDRAM untuk menerapkan pembatasan laju untuk situs web Anda, pastikan direktif dibawah ini ditetapkan sebagai nilai default. Sebaliknya, Anda dapat mengubah nilainya sesuai dengan kebutuhan Anda.

##### "max_bandwidth"
- Jumlah maksimum bandwidth yang diizinkan dalam periode tunjangan sebelum mengaktifkan pembatasan laju untuk permintaan di masa mendatang. Nilai 0 menonaktifkan jenis pembatasan laju ini. Default = 0KB.

##### "max_requests"
- Jumlah maksimum permintaan yang diizinkan dalam periode tunjangan sebelum mengaktifkan pembatasan laju untuk permintaan di masa mendatang. Nilai 0 menonaktifkan jenis pembatasan laju ini. Default = 0.

##### "precision_ipv4"
- Presisi yang akan digunakan saat memonitor penggunaan IPv4. Nilai mencerminkan ukuran blok CIDR. Atur ke 32 untuk presisi terbaik. Default = 32.

##### "precision_ipv6"
- Presisi yang akan digunakan saat memonitor penggunaan IPv6. Nilai mencerminkan ukuran blok CIDR. Atur ke 128 untuk presisi terbaik. Default = 128.

##### "allowance_period"
- Jumlah jam untuk memonitor penggunaan. Default = 0.

##### "exceptions"
- Pengecualian (yaitu, permintaan yang seharusnya tidak dibatasi). Hanya relevan ketika pembatasan laju diaktifkan.
- *Opsi yang tersedia: `Whitelisted,Verified`*

#### "supplementary_cache_options" (Kategori)
Opsi cache tambahan.

##### "prefix"
- Nilai yang ditentukan disini akan ditambahkan ke awal kunci untuk semua entri di cache. Kosong secara default. Ketika beberapa instalasi ada di server, ini dapat berguna untuk menjaga cache mereka terpisah.

##### "enable_apcu"
- Menentukan apakah akan mencoba menggunakan APCu untuk cache. Default = False.

##### "enable_memcached"
- Menentukan apakah akan mencoba menggunakan Memcached untuk cache. Default = False.

##### "enable_redis"
- Menentukan apakah akan mencoba menggunakan Redis untuk cache. Default = False.

##### "enable_pdo"
- Menentukan apakah akan mencoba menggunakan PDO untuk cache. Default = False.

##### "memcached_host"
- Nilai host Memcached. Default = "localhost".

##### "memcached_port"
- Nilai port Memcached. Default = "11211".

##### "redis_host"
- Nilai host Redis. Default = "localhost".

##### "redis_port"
- Nilai port Redis. Default = "6379".

##### "redis_timeout"
- Nilai batas waktu Redis. Default = "2.5".

##### "pdo_dsn"
- Nilai DSN PDO. Default = "`mysql:dbname=cidram;host=localhost;port=3306`".

*Lihat juga: [Apa itu "PDO DSN"? Bagaimana saya bisa menggunakan PDO dengan CIDRAM?](#HOW_TO_USE_PDO)*

##### "pdo_username"
- Nama pengguna PDO.

##### "pdo_password"
- Kata sandi PDO.

---


### 7. <a name="SECTION7"></a>FORMAT TANDA TANGAN

*Lihat juga:*
- *[Apa yang "tanda tangan"?](#WHAT_IS_A_SIGNATURE)*

#### 7.0 DASAR-DASAR (UNTUK FILE TANDA TANGAN)

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

#### 7.1 TAG

##### 7.1.0 TAG BAGIAN

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

##### 7.1.1 TAG KADALUARSA

Jika Anda ingin tanda tangan untuk berakhir setelah beberapa waktu, dengan cara yang sama untuk tag bagian, Anda dapat menggunakan "tag kadaluarsa" untuk menentukan kapan tanda tangan harus berhenti menjadi valid. Tag kadaluarsa menggunakan format "TTTT.BB.HH" (lihat contoh dibawah ini).

```
# Bagian 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Tanda tangan kadaluarsa tidak akan pernah dipicu pada permintaan apapun, tidak masalah apa.

##### 7.1.2 TAG ASAL

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

##### 7.1.3 TAG PENANGGUH

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

##### 7.1.4 TAG PROFIL

Tag profil menyediakan sarana untuk menampilkan informasi tambahan di halaman pengujian IP, dan dapat dimanfaatkan oleh modul dan aturan tambahan untuk perilaku yang lebih kompleks dan pengambilan keputusan yang lebih baik.

Tag profil digunakan serupa dengan jenis tag lainnya. Nilai untuk tag profil dapat digunakan sebagai kondisi untuk modul dan aturan tambahan. Tag profil dapat memberikan beberapa nilai dengan memisahkan nilai tersebut dengan titik koma. Pengguna tidak pernah melihat nilai untuk tag profil.

Contoh:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 7.2 YAML

##### 7.2.0 DASAR-DASAR YAML

Sebuah bentuk sederhana YAML markup dapat digunakan dalam file tanda tangan untuk tujuan perilaku mendefinisikan dan direktif spesifik untuk bagian tanda tangan individu. Ini mungkin berguna jika Anda ingin nilai direktif konfigurasi berbeda atas dasar tanda tangan individu dan bagian tanda tangan (sebagai contoh; jika Anda ingin memberikan alamat email untuk tiket dukungan untuk setiap pengguna diblokir oleh satu tanda tangan tertentu, tapi tidak ingin memberikan alamat email untuk tiket dukungan untuk pengguna diblokir oleh tanda tangan lain; jika Anda ingin beberapa tanda tangan spesifik untuk memicu halaman redireksi; jika Anda ingin menandai bagian tanda tangan untuk digunakan dengan reCAPTCHA/hCAPTCHA; jika Anda ingin merekam diblokir upaya akses untuk memisahkan file berdasarkan tanda tangan individu dan/atau bagian tanda tangan).

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
 logfile: logfile.{yyyy}-{mm}-{dd}.txt
 logfile_apache: access.{yyyy}-{mm}-{dd}.txt
 logfile_serialized: serial.{yyyy}-{mm}-{dd}.txt
 forbid_on_block: false
 emailaddr: username@domain.tld
recaptcha:
 lockip: false
 lockuser: true
 expiry: 720
 logfile: recaptcha.{yyyy}-{mm}-{dd}.txt
 enabled: true
template_data:
 css_url: https://domain.tld/cidram.css

# Foobar 2.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 2
---
general:
 logfile: "logfile.Foobar2.{yyyy}-{mm}-{dd}.txt"
 logfile_apache: "access.Foobar2.{yyyy}-{mm}-{dd}.txt"
 logfile_serialized: "serial.Foobar2.{yyyy}-{mm}-{dd}.txt"
 forbid_on_block: 503

# Foobar 3.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 3
---
general:
 forbid_on_block: 403
 silent_mode: "http://127.0.0.1/"
```

##### 7.2.1 BAGAIMANA "KHUSUS MENANDAI" BAGIAN TANDA TANGAN UNTUK DIGUNAKAN DENGAN reCAPTCHA/hCAPTCHA

Ketika "usemode" 2 atau 5, untuk "khusus menandai" bagian tanda tangan untuk digunakan dengan reCAPTCHA/hCAPTCHA, entri termasuk dalam segmen YAML untuk bagian tanda tangan (lihat contoh dibawah ini).

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

#### 7.3 INFORMASI TAMBAHAN

##### 7.3.0 MENGABAIKAN BAGIAN TANDA TANGAN

Juga, jika Anda ingin CIDRAM untuk sama sekali mengabaikan beberapa bagian tertentu dalam salah satu file tanda tangan, Anda dapat menggunakan file `ignore.dat` untuk menentukan bagian untuk mengabaikan. Pada baris baru, menulis `Ignore`, diikuti dengan spasi, diikuti dengan nama bagian yang Anda ingin CIDRAM untuk mengabaikan (lihat contoh dibawah ini).

```
Ignore Bagian 1
```

Ini juga dapat dicapai dengan menggunakan antarmuka yang disediakan oleh halaman "daftar bagian" dari bagian depan CIDRAM.

##### 7.3.1 ATURAN TAMBAHAN

Jika Anda merasa bahwa menulis file tanda tangan atau modul kustom Anda sendiri terlalu rumit untuk Anda, alternatif yang lebih sederhana mungkin menggunakan antarmuka yang disediakan oleh halaman "aturan tambahan" dari bagian depan CIDRAM. Dengan memilih opsi yang sesuai dan menentukan detail tentang jenis permintaan spesifik, Anda dapat menginstruksikan CIDRAM cara menanggapi permintaan tersebut. "Aturan tambahan" dijalankan setelah semua file tanda tangan dan modul telah selesai dijalankan.

#### 7.4 <a name="MODULE_BASICS"></a>DASAR-DASAR (UNTUK MODUL)

Modul dapat digunakan untuk memperluas fungsionalitas CIDRAM, melakukan tugas tambahan, atau memproses logika tambahan.

Karena modul ditulis sebagai file PHP, jika Anda cukup mengenal basis kode CIDRAM, Anda dapat menyusun modul Anda namun Anda inginkan, dan menulis tanda tangan modul Anda namun Anda inginkan (dalam batasan untuk apa yang mungkin di PHP).

*Catat: Jika Anda tidak nyaman bekerja dengan kode PHP, menulis modul Anda sendiri tidak disarankan.*

Beberapa fungsi disediakan oleh CIDRAM yang dapat digunakan oleh modul, yang seharusnya membuatnya lebih sederhana dan mudah untuk menulis modul Anda sendiri. Informasi tentang fungsi ini dijelaskan dibawah ini.

#### 7.5 FUNGSIONALITAS MODUL

##### 7.5.0 "$Trigger"

Tanda tangan modul biasanya ditulis dengan `$Trigger`. Dalam kebanyakan kasus, closure ini akan lebih penting daripada hal lain untuk tujuan penulisan modul.

`$Trigger` menerima 4 parameter: `$Condition`, `$ReasonShort`, `$ReasonLong` (opsional), dan `$DefineOptions` (opsional).

Kebenaran dari `$Condition` dievaluasi, dan jika true/benar, tanda tangan "dipicu". Jika false/salah, tanda tangan *tidak* "dipicu". `$Condition` biasanya berisi kode PHP untuk mengevaluasi suatu kondisi yang harus menyebabkan permintaan diblokir.

`$ReasonShort` dikutip di bidang "Mengapa Diblokir" saat tanda tangan "dipicu".

`$ReasonLong` adalah pesan opsional yang akan ditampilkan kepada pengguna/klien saat mereka diblokir, untuk menjelaskan mengapa mereka diblokir. Default ke pesan "Akses Ditolak" standar saat dihilangkan.

`$DefineOptions` adalah array opsional yang berisi pasangan kunci/nilai, digunakan untuk menentukan opsi konfigurasi yang spesifik untuk instance permintaan. Opsi konfigurasi akan diterapkan saat tanda tangan "dipicu".

`$Trigger` kembali true/benar saat tanda tangan "dipicu", dan false/salah saat tidak.

Untuk menggunakan closure ini di modul Anda, ingat dulu untuk mewarisi dari lingkup luar:
```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### 7.5.1 "$Bypass"

Tanda tangan bypass biasanya ditulis dengan `$Bypass`.

`$Bypass` menerima 3 parameter: `$Condition`, `$ReasonShort`, dan `$DefineOptions` (opsional).

Kebenaran dari `$Condition` dievaluasi, dan jika true/benar, bypass "dipicu". Jika false/salah, bypass *tidak* "dipicu". `$Condition` biasanya berisi kode PHP untuk mengevaluasi suatu kondisi yang harus *tidak* menyebabkan permintaan diblokir.

`$ReasonShort` dikutip di bidang "Mengapa Diblokir" saat bypass "dipicu".

`$DefineOptions` adalah array opsional yang berisi pasangan kunci/nilai, digunakan untuk menentukan opsi konfigurasi yang spesifik untuk instance permintaan. Opsi konfigurasi akan diterapkan saat bypass "dipicu".

`$Bypass` kembali true/benar saat bypass "dipicu", dan false/salah saat tidak.

Untuk menggunakan closure ini di modul Anda, ingat dulu untuk mewarisi dari lingkup luar:
```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### 7.5.2 "$CIDRAM['DNS-Reverse']"

Ini bisa digunakan untuk mengambil nama host dari alamat IP. Jika Anda ingin membuat modul untuk memblokir nama host, closure ini bisa bermanfaat.

Contoh:
```PHP
<?php
/** Inherit trigger closure (see functions.php). */
$Trigger = $CIDRAM['Trigger'];

/** Fetch hostname. */
if (empty($CIDRAM['Hostname'])) {
    $CIDRAM['Hostname'] = $CIDRAM['DNS-Reverse']($CIDRAM['BlockInfo']['IPAddr']);
}

/** Example signature. */
if ($CIDRAM['Hostname'] && $CIDRAM['Hostname'] !== $CIDRAM['BlockInfo']['IPAddr']) {
    $Trigger($CIDRAM['Hostname'] === 'www.foobar.tld', 'Foobar.tld', 'Hostname Foobar.tld is not allowed.');
}
```

#### 7.6 MODUL VARIABEL

Modul mengeksekusi dalam lingkup mereka sendiri, dan variabel apapun yang ditentukan oleh modul, tidak akan dapat diakses ke modul lain, atau ke skrip utama, kecuali jika disimpan dalam array `$CIDRAM` (segala sesuatu yang lain dibuang setelah eksekusi modul selesai).

Tercantum dibawah ini adalah beberapa variabel umum yang mungkin berguna untuk modul Anda:

Variabel | Deskripsi
----|----
`$CIDRAM['BlockInfo']['DateTime']` | Tanggal dan waktu sekarang.
`$CIDRAM['BlockInfo']['IPAddr']` | Alamat IP untuk permintaan saat ini.
`$CIDRAM['BlockInfo']['ScriptIdent']` | Versi skrip CIDRAM.
`$CIDRAM['BlockInfo']['Query']` | "Query" untuk permintaan saat ini.
`$CIDRAM['BlockInfo']['Referrer']` | Perujuk untuk permintaan saat ini (jika ada).
`$CIDRAM['BlockInfo']['UA']` | Agen pengguna (user agent) untuk permintaan saat ini.
`$CIDRAM['BlockInfo']['UALC']` | Agen pengguna (user agent) untuk permintaan saat ini (di huruf kecil).
`$CIDRAM['BlockInfo']['ReasonMessage']` | Pesan yang akan ditampilkan ke pengguna/klien untuk permintaan saat ini jika diblokir.
`$CIDRAM['BlockInfo']['SignatureCount']` | Jumlah tanda tangan dipicu untuk permintaan saat ini.
`$CIDRAM['BlockInfo']['Signatures']` | Informasi referensi untuk tanda tangan yang dipicu untuk permintaan saat ini.
`$CIDRAM['BlockInfo']['WhyReason']` | Informasi referensi untuk tanda tangan yang dipicu untuk permintaan saat ini.

---


### 8. <a name="SECTION8"></a>MASALAH KOMPATIBILITAS DIKETAHUI

Paket dan produk berikut telah ditemukan tidak bisa dioperasikan dengan CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Modul telah tersedia untuk memastikan bahwa paket dan produk berikut akan kompatibel dengan CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Lihat juga: [Bagan Kompatibilitas](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 9. <a name="SECTION9"></a>PERTANYAAN YANG SERING DIAJUKAN (FAQ)

- [Apa yang "tanda tangan"?](#WHAT_IS_A_SIGNATURE)
- [Apa yang "CIDR"?](#WHAT_IS_A_CIDR)
- [Apa yang dimaksud dengan "positif palsu"?](#WHAT_IS_A_FALSE_POSITIVE)
- [Dapat CIDRAM blok seluruh negara?](#BLOCK_ENTIRE_COUNTRIES)
- [Seberapa sering tanda tangan diperbarui?](#SIGNATURE_UPDATE_FREQUENCY)
- [Saya mengalami masalah ketika menggunakan CIDRAM dan saya tidak tahu apa saya harus lakukan! Tolong bantu!](#ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Saya diblokir oleh CIDRAM dari situs web yang saya ingin mengunjungi! Tolong bantu!](#BLOCKED_WHAT_TO_DO)
- [Saya ingin menggunakan CIDRAM (sebelum v2) dengan versi PHP yang lebih tua dari 5.4.0; Anda dapat membantu?](#MINIMUM_PHP_VERSION)
- [Saya ingin menggunakan CIDRAM (v2) dengan versi PHP yang lebih tua dari 7.2.0; Anda dapat membantu?](#MINIMUM_PHP_VERSION_V2)
- [Dapatkah saya menggunakan satu instalasi CIDRAM untuk melindungi beberapa domain?](#PROTECT_MULTIPLE_DOMAINS)
- [Saya tidak ingin membuang waktu dengan menginstal ini dan membuatnya bekerja dengan situs web saya; Bisakah saya membayar Anda untuk melakukan semuanya untuk saya?](#PAY_YOU_TO_DO_IT)
- [Dapatkah saya mempekerjakan Anda atau pengembang proyek ini untuk pekerjaan pribadi?](#HIRE_FOR_PRIVATE_WORK)
- [Saya perlu modifikasi khusus, customisasi, dll; Apakah kamu bisa membantu?](#SPECIALIST_MODIFICATIONS)
- [Saya seorang pengembang, perancang situs web, atau programmer. Dapatkah saya menerima atau menawarkan pekerjaan yang berkaitan dengan proyek ini?](#ACCEPT_OR_OFFER_WORK)
- [Saya ingin berkontribusi pada proyek ini; Dapatkah saya melakukan ini?](#WANT_TO_CONTRIBUTE)
- [Dapatkah saya menggunakan cron untuk mengupdate secara otomatis?](#CRON_TO_UPDATE_AUTOMATICALLY)
- [Apa "pelanggaran"?](#WHAT_ARE_INFRACTIONS)
- [Dapatkah CIDRAM memblokir nama host?](#BLOCK_HOSTNAMES)
- [Apa yang bisa saya gunakan untuk "default_dns"?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)
- [Dapatkah saya menggunakan CIDRAM untuk melindungi hal-hal selain daripada situs web (misalnya, server email, FTP, SSH, IRC, dll)?](#PROTECT_OTHER_THINGS)
- [Akankah masalah terjadi jika saya menggunakan CIDRAM pada saat yang sama dengan menggunakan layanan CDN atau cache?](#CDN_CACHING_PROBLEMS)
- [Akankah CIDRAM melindungi situs web saya dari serangan DDoS?](#DDOS_ATTACKS)
- [Ketika saya mengaktifkan atau menonaktifkan modul atau file tanda tangan melalui halaman pembaruan, itu memilah mereka secara alfanumerik dalam konfigurasi. Bisakah saya mengubah cara mereka disortir?](#CHANGE_COMPONENT_SORT_ORDER)
- [Apa itu "PDO DSN"? Bagaimana saya bisa menggunakan PDO dengan CIDRAM?](#HOW_TO_USE_PDO)
- [CIDRAM memblokir cronjobs; Bagaimana cara memperbaikinya?](#BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>Apa yang "tanda tangan"?

Dalam konteks CIDRAM, "tanda tangan" mengacu pada data yang bertindak sebagai indikator/pengenal untuk sesuatu spesifik yang kita mencari, biasanya alamat IP atau CIDR, dan termasuk beberapa instruksi untuk CIDRAM, mengatakannya cara terbaik untuk menanggapi saat menemukan apa yang kita mencari. Tanda tangan khas untuk CIDRAM terlihat seperti ini:

Untuk "file tanda tangan":

`1.2.3.4/32 Deny Generic`

Untuk "modul":

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
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
- Apakah Anda memeriksa semua dokumentasi? Jika tidak, silahkan melakukannya. Jika masalah tidak dapat diselesaikan dengan menggunakan dokumentasi, lanjutkan membaca.
- Apakah Anda memeriksa **[halaman issues](https://github.com/CIDRAM/CIDRAM/issues)**, untuk melihat apakah masalah telah disebutkan sebelumnya? Jika sudah disebutkan sebelumnya, memeriksa apakah ada saran, ide, dan/atau solusi yang tersedia, dan ikuti sesuai yang diperlukan untuk mencoba untuk menyelesaikan masalah.
- Jika masalah masih berlanjut, silahkan mencari bantuan dengan membuat issue baru di halaman issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>Saya diblokir oleh CIDRAM dari situs web yang saya ingin mengunjungi! Tolong bantu!

CIDRAM menyediakan sarana bagi pemilik situs web untuk memblokir lalu lintas yang tidak diinginkan, tapi pemilik situs web bertanggung jawab untuk memutuskan bagaimana mereka ingin menggunakan CIDRAM. Dalam kasus positif palsu yang berkaitan dengan file tanda tangan yang biasanya disertakan dengan CIDRAM, koreksi dapat dibuat, tetapi dalam hal yang tidak terblokir dari situs web tertentu, Anda harus menghubungi pemilik dari situs yang bersangkutan. Dalam kasus dimana koreksi dibuat, setidaknya, mereka harus memperbarui file tanda tangan mereka dan/atau memperbarui instalasi mereka, dan dalam kasus lain (seperti, misalnya, ketika mereka diubah instalasi mereka, membuat tanda tangan kustom, dll), tanggung jawab untuk memecahkan masalah Anda sepenuhnya milik mereka, dan sepenuhnya di luar kendali kita.

#### <a name="MINIMUM_PHP_VERSION"></a>Saya ingin menggunakan CIDRAM (sebelum v2) dengan versi PHP yang lebih tua dari 5.4.0; Anda dapat membantu?

Tidak. PHP >= 5.4.0 adalah persyaratan minimum untuk CIDRAM < v2.

#### <a name="MINIMUM_PHP_VERSION_V2"></a>Saya ingin menggunakan CIDRAM (v2) dengan versi PHP yang lebih tua dari 7.2.0; Anda dapat membantu?

Tidak. PHP >= 7.2.0 adalah persyaratan minimum untuk CIDRAM v2.

*Lihat juga: [Bagan Kompatibilitas](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Dapatkah saya menggunakan satu instalasi CIDRAM untuk melindungi beberapa domain?

Ya. Instalasi CIDRAM tidak secara alami terkunci pada domain tertentu, dan dengan demikian dapat digunakan untuk melindungi beberapa domain. Umumnya, kami mengacu pada instalasi CIDRAM yang hanya melindungi satu domain as "instalasi domain tunggal" ("single-domain installations"), dan kami mengacu pada instalasi CIDRAM yang melindungi beberapa domain dan/atau sub-domain sebagai "instalasi domain beberapa" ("multi-domain installations"). Jika Anda mengoperasikan instalasi domain beberapa dan perlu menggunakan berbagai kumpulan file tanda tangan untuk berbagai domain, atau perlu CIDRAM untuk dikonfigurasi secara berbeda untuk domain berbeda, kamu bisa melakukan ini. Setelah memuat file konfigurasi (`config.ini`), CIDRAM akan memeriksa adanya "file untuk pengganti konfigurasi" spesifik untuk domain (atau sub-domain) yang diminta (`domain-yang-diminta.tld.config.ini`), dan jika ditemukan, setiap nilai konfigurasi yang ditentukan oleh file untuk pengganti konfigurasi akan digunakan untuk instance eksekusi daripada nilai konfigurasi yang ditentukan oleh file konfigurasi. File untuk pengganti konfigurasi identik dengan file konfigurasi, dan atas kebijaksanaan Anda, dapat berisi keseluruhan semua konfigurasi yang tersedia untuk CIDRAM, atau apapun bagian kecil yang dibutuhkan yang berbeda dari nilai yang biasanya ditentukan oleh file konfigurasi. File untuk pengganti konfigurasi diberi nama sesuai dengan domain yang mereka inginkan (jadi, misalnya, jika Anda memerlukan file untuk pengganti konfigurasi untuk domain, `https://www.some-domain.tld/`, file untuk pengganti konfigurasi harus diberi nama sebagai `some-domain.tld.config.ini`, dan harus ditempatkan di dalam vault bersama file konfigurasi, `config.ini`). Nama domain untuk instance eksekusi berasal dari header permintaan `HTTP_HOST`; "www" diabaikan.

#### <a name="PAY_YOU_TO_DO_IT"></a>Saya tidak ingin membuang waktu dengan menginstal ini dan membuatnya bekerja dengan situs web saya; Bisakah saya membayar Anda untuk melakukan semuanya untuk saya?

Mungkin. Ini dipertimbangkan berdasarkan kasus per kasus. Beritahu kami apa yang Anda butuhkan, apa yang Anda tawarkan, dan kami akan memberitahu Anda jika kami dapat membantu.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Dapatkah saya mempekerjakan Anda atau pengembang proyek ini untuk pekerjaan pribadi?

*Lihat di atas.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Saya perlu modifikasi khusus, customisasi, dll; Apakah kamu bisa membantu?

*Lihat di atas.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Saya seorang pengembang, perancang situs web, atau programmer. Dapatkah saya menerima atau menawarkan pekerjaan yang berkaitan dengan proyek ini?

Ya. Lisensi kami tidak melarang hal ini.

#### <a name="WANT_TO_CONTRIBUTE"></a>Saya ingin berkontribusi pada proyek ini; Dapatkah saya melakukan ini?

Ya. Kontribusi untuk proyek ini sangat disambut baik. Silahkan lihat "CONTRIBUTING.md" untuk informasi lebih lanjut.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Dapatkah saya menggunakan cron untuk mengupdate secara otomatis?

Ya. API dibangun dalam bagian depan untuk berinteraksi dengan halaman pembaruan melalui skrip eksternal. Skrip terpisah, "[Cronable](https://github.com/Maikuolan/Cronable)", tersedia, dan dapat digunakan oleh cron manager atau cron scheduler untuk mengupdate paket ini dan paket didukung lainnya secara otomatis (script ini menyediakan dokumentasi sendiri).

#### <a name="WHAT_ARE_INFRACTIONS"></a>Apa "pelanggaran"?

"Pelanggaran" menentukan kapan IP yang belum diblokir oleh file tanda tangan tertentu seharusnya mulai diblokir untuk permintaan di masa mendatang, dan mereka terkait erat dengan pelacakan IP. Beberapa fungsi dan modul ada yang memungkinkan permintaan menjadi diblokir karena alasan selain IP asal (seperti kehadiran agen pengguna [user agent] yang sesuai dengan spambot atau hacktool, permintaan berbahaya, DNS ditempa dan seterusnya), dan kapan ini terjadi, "pelanggaran" dapat terjadi. Mereka menyediakan cara untuk mengidentifikasi alamat IP yang sesuai dengan permintaan yang tidak diinginkan yang mungkin belum terhalang oleh file tanda tangan tertentu. Pelanggaran biasanya sesuai 1-ke-1 dengan berapa kali IP diblokir, namun tidak selalu (kejadian blokir yang parah dapat menimbulkan nilai pelanggaran lebih besar dari satu, dan jika "track_mode" false, pelanggaran tidak akan terjadi karena kejadian blokir yang hanya dipicu oleh file tanda tangan).

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

*Catat: Saya tidak membuat klaim atau jaminan berkenaan dengan praktik privasi, keamanan, keampuhan, atau keandalan untuk layanan DNS apapun, apakah terdaftar atau sebaliknya. Silahkan lakukan penelitian Anda sendiri ketika membuat keputusan tentang mereka.*

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

`file1.php,file2.php,file3.php,file4.php,file5.php`

Jika Anda ingin `file3.php` untuk mengeksekusi terlebih dahulu, Anda bisa menambahkan sesuatu seperti `aaa:` sebelum nama file:

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

Kemudian, jika file baru, `file6.php`, diaktifkan, ketika halaman pembaruan mengurutkan semuanya lagi, itu akan berakhir seperti ini:

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

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


### 11. <a name="SECTION11"></a>INFORMASI HUKUM

#### 11.0 PENGANTAR BAGIAN

Bagian dokumentasi ini dimaksudkan untuk menjelaskan kemungkinan pertimbangan hukum mengenai penggunaan dan implementasi paket, dan untuk memberikan beberapa informasi dasar terkait. Ini mungkin penting bagi beberapa pengguna sebagai sarana untuk memastikan kepatuhan dengan persyaratan hukum yang mungkin ada di negara tempat mereka beroperasi, dan beberapa pengguna mungkin perlu menyesuaikan kebijakan situs web mereka sesuai dengan informasi ini.

Pertama dan terutama, harap menyadari bahwa saya (penulis paket) bukan seorang pengacara, atau profesional hukum yang berkualitas dalam bentuk apapun. Oleh karena itu, saya secara hukum tidak memenuhi syarat untuk memberikan nasihat hukum. Juga, dalam beberapa kasus, persyaratan hukum yang tepat dapat bervariasi antara negara dan yurisdiksi yang berbeda, dan berbagai persyaratan hukum ini terkadang dapat menimbulkan konflik (seperti, misalnya, dalam kasus negara-negara yang mendukung hak privasi dan hak untuk dilupakan, versus negara-negara yang mendukung retensi data diperpanjang). Pertimbangkan juga bahwa akses ke paket tidak terbatas pada negara atau yurisdiksi tertentu, dan oleh karena itu, pengguna paket cenderung ke geografis yang beragam. Poin-poin ini dianggap, saya tidak dalam posisi untuk menyatakan apa artinya "mematuhi hukum" untuk semua pengguna, dalam semua hal. Namun, saya berharap informasi disini akan membantu Anda untuk mengambil keputusan sendiri mengenai apa yang Anda harus lakukan agar tetap mematuhi hukum dalam konteks paket. Jika Anda memiliki keraguan atau kekhawatiran mengenai informasi disini, atau jika Anda membutuhkan bantuan dan saran tambahan dari perspektif hukum, saya merekomendasikan konsultasi dengan profesional hukum yang berkualitas.

#### 11.1 TANGGUNG JAWAB DAN KEWAJIBAN HUKUM

Seperti yang telah dinyatakan oleh lisensi paket, paket ini disediakan tanpa jaminan apapun. Ini termasuk (tetapi tidak terbatas pada) semua lingkup kewajiban hukum. Paket ini diberikan kepada Anda untuk kenyamanan Anda, dengan harapan itu akan berguna, dan itu akan memberikan beberapa manfaat bagi Anda. Namun, apakah Anda menggunakan atau mengimplementasikan paket ini, adalah pilihan Anda sendiri. Anda tidak dipaksa untuk menggunakan atau mengimplementasikan paket ini, tetapi ketika Anda melakukannya, Anda bertanggung jawab atas keputusan itu. Bukan saya, dan tidak ada kontributor lain untuk paket ini, bertanggung jawab secara hukum atas konsekuensi keputusan yang Anda buat, terlepas dari apakah langsung, tidak langsung, tersirat, atau sebaliknya.

#### 11.2 PIHAK KETIGA

Tergantung pada konfigurasi dan implementasinya yang tepat, paket dapat berkomunikasi dan berbagi informasi dengan pihak ketiga dalam beberapa kasus. Informasi ini dapat didefinisikan sebagai "informasi identitas pribadi" (PII) dalam beberapa konteks, oleh beberapa yurisdiksi.

Bagaimana informasi ini dapat digunakan oleh pihak ketiga ini, tunduk pada berbagai kebijakan yang ditetapkan oleh pihak ketiga ini, dan berada di luar ruang lingkup dokumentasi ini. Namun, dalam semua kasus tersebut, berbagi informasi dengan pihak ketiga ini dapat dinonaktifkan. Dalam semua kasus semacam itu, jika Anda memilih untuk mengaktifkannya, Anda bertanggung jawab untuk meneliti setiap kekhawatiran yang mungkin Anda miliki tentang privasi, keamanan, dan penggunaan PII oleh pihak ketiga ini. Jika ada keraguan, atau jika Anda tidak puas dengan perilaku pihak ketiga ini sehubungan dengan PII, mungkin terbaik adalah menonaktifkan semua pembagian informasi dengan pihak ketiga ini.

Untuk tujuan transparansi, jenis informasi yang dibagikan, dan dengan siapa, dijelaskan dibawah ini.

##### 11.2.0 PENCARIAN NAMA HOST

Jika Anda menggunakan fitur atau modul yang dimaksudkan untuk bekerja dengan nama host (seperti "modul pemblokir untuk host buruk", "tor project exit nodes block module", atau "verifikasi mesin pencari", misalnya), CIDRAM harus dapat memperoleh nama host dari permintaan masuk entah bagaimana. Biasanya, ini dilakukan dengan meminta nama host dari alamat IP permintaan masuk dari server DNS, atau dengan meminta informasi melalui fungsionalitas yang disediakan oleh sistem tempat CIDRAM diinstal (ini biasanya disebut sebagai "pencarian nama host"). Server DNS yang ditentukan secara default adalah milik layanan [Google DNS](https://dns.google.com/) (tetapi ini dapat dengan mudah diubah melalui konfigurasi). Layanan yang tepat yang dikomunikasikan dapat dikonfigurasi, dan tergantung pada cara Anda mengonfigurasi paket. Dalam kasus menggunakan fungsionalitas yang disediakan oleh sistem tempat CIDRAM diinstal, Anda harus menghubungi administrator sistem Anda untuk menentukan rute mana yang digunakan oleh pencarian nama host. Pencarian nama host dapat dicegah dalam CIDRAM dengan menghindari modul yang terpengaruh atau dengan memodifikasi konfigurasi paket sesuai dengan kebutuhan Anda.

*Direktif konfigurasi yang relevan:*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

##### 11.2.1 FONT WEB

Beberapa tema kustom, serta UI standar ("antarmuka pengguna") untuk halaman bagian depan CIDRAM dan halaman "Akses Ditolak", dapat menggunakan font web untuk alasan estetika. Font web dinonaktifkan secara default, tetapi ketika diaktifkan, komunikasi langsung antara browser pengguna dan layanan hosting font web terjadi. Ini mungkin melibatkan informasi komunikasi seperti alamat IP pengguna, agen pengguna, sistem operasi, dan detail lainnya yang tersedia untuk permintaan tersebut. Sebagian besar font web ini dihosting oleh layanan [Google Fonts](https://fonts.google.com/).

*Direktif konfigurasi yang relevan:*
- `general` -> `disable_webfonts`

##### 11.2.2 VERIFIKASI MESIN PENCARI DAN MEDIA SOSIAL

Ketika verifikasi mesin pencari diaktifkan, CIDRAM mencoba melakukan "pencarian DNS ke depan" untuk memverifikasi apakah permintaan yang mengaku berasal dari mesin pencari adalah asli. Juga, ketika verifikasi media sosial diaktifkan, CIDRAM melakukan hal yang sama untuk permintaan media sosial dugaan. Untuk melakukan ini, verifikasi mesin pencari menggunakan layanan [Google DNS](https://dns.google.com/) untuk mencoba menyelesaikan alamat IP dari nama host dari permintaan masuk ini (dalam proses ini, nama host dari permintaan masuk ini dibagikan dengan layanan).

*Direktif konfigurasi yang relevan:*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 11.2.3 CAPTCHA

CIDRAM mendukung reCAPTCHA dan hCAPTCHA. Mereka membutuhkan kunci API agar berfungsi dengan benar. Mereka dinonaktifkan secara default, tetapi dapat diaktifkan dengan mengonfigurasi kunci API yang diperlukan. Ketika diaktifkan, komunikasi dapat terjadi antara layanan dan CIDRAM atau browser pengguna. Ini mungkin melibatkan mengkomunikasikan informasi seperti alamat IP pengguna, agen pengguna, sistem operasi, dan detail lain yang tersedia untuk permintaan tersebut.

##### 11.2.4 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) adalah layanan fantastis, tersedia secara bebas yang dapat membantu melindungi forum, blog, dan situs web dari spammer. Ini dilakukan dengan menyediakan database spammer yang dikenal, dan API yang dapat dimanfaatkan untuk memeriksa apakah alamat IP, nama pengguna, atau alamat email tercantum dalam database-nya.

CIDRAM menyediakan modul opsional yang memanfaatkan API ini untuk memeriksa apakah alamat IP dari permintaan masuk milik seorang spammer yang dicurigai. Modul ini tidak diinstal secara default, tetapi jika Anda memilih untuk menginstalnya, alamat IP pengguna dapat dibagikan dengan API Stop Forum Spam sesuai dengan tujuan yang dimaksudkan dari modul. Ketika modul diinstal, CIDRAM berkomunikasi dengan API ini setiap kali permintaan masuk meminta sumber halaman yang diakui oleh CIDRAM sebagai jenis sumber halaman yang sering ditargetkan oleh pelaku spam (seperti halaman login, halaman registrasi, halaman verifikasi email, formulir komentar, dll).

##### 11.2.5 ABUSEIPDB

CIDRAM menyediakan modul opsional untuk memblokir alamat IP yang memiliki catatan penyalahgunaan oleh menggunakan API [AbuseIPDB](https://www.abuseipdb.com/). Modul ini tidak diinstal secara default, tetapi jika Anda memilih untuk menginstalnya, alamat IP pengguna dapat dibagikan dengan API AbuseIPDB sesuai dengan tujuan yang dimaksudkan dari modul.

##### 11.2.6 BGPVIEW

CIDRAM menyediakan modul opsional untuk melakukan pencarian ASN dan kode negara menggunakan API [BGPView](https://bgpview.io/). Pencarian ini menyediakan kemampuan untuk memblokir atau memasukkan daftar putih berdasarkan ASN atau negara asal mereka. Modul ini tidak diinstal secara default, tetapi jika Anda memilih untuk menginstalnya, alamat IP pengguna dapat dibagikan dengan API BGPView sesuai dengan tujuan yang dimaksudkan dari modul.

#### 11.3 PENCATATAN

Pencatatan adalah bagian penting dari CIDRAM karena sejumlah alasan. Mungkin sulit untuk mendiagnosis dan menyelesaikan kesalahan positif ketika kejadian blokir yang menyebabkan mereka tidak dicatat. Tanpa mencatat kejadian blokir, mungkin sulit untuk memastikan secara akurat seberapa baik kinerja CIDRAM dalam konteks tertentu, dan mungkin sulit untuk menentukan dimana kekurangannya, dan perubahan apa yang mungkin diperlukan untuk konfigurasi atau tanda tangan yang sesuai, agar terus berfungsi sebagaimana dimaksud. Apapun, pencatatan mungkin tidak diinginkan untuk semua pengguna, dan tetap sepenuhnya opsional. Di CIDRAM, pencatatan dinonaktifkan secara default. Untuk mengaktifkannya, CIDRAM harus dikonfigurasi dengan benar.

Juga, apakah pencatatan diizinkan secara hukum, dan sejauh diizinkan secara hukum (misalnya, jenis informasi yang dapat dicatat, untuk berapa lama, dan dalam keadaan apa), dapat bervariasi, tergantung pada yurisdiksi dan pada konteks dimana CIDRAM diimplementasikan (misalnya, apakah Anda beroperasi sebagai individu, sebagai entitas perusahaan, dan apakah secara komersial atau non-komersial). Jadi, mungkin berguna bagi Anda untuk membaca bagian ini dengan seksama.

Ada beberapa jenis pencatatan yang dapat dilakukan oleh CIDRAM. Berbagai jenis pencatatan melibatkan berbagai jenis informasi, untuk berbagai alasan.

##### 11.3.0 KEJADIAN BLOKIR

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
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

Ketika direktif ini dibiarkan kosong, jenis pencatatan ini akan tetap dinonaktifkan.

##### 11.3.1 LOG CAPTCHA

Jenis pencatatan ini secara khusus berkaitan dengan instance CAPTCHA, dan hanya terjadi ketika pengguna mencoba menyelesaikan instance CAPTCHA.

Entri log CAPTCHA berisi alamat IP pengguna yang berusaha menyelesaikan instance CAPTCHA, tanggal dan waktu ketika itu terjadi, dan status CAPTCHA. Entri log CAPTCHA biasanya terlihat seperti ini (sebagai contoh):

```
Alamat IP: x.x.x.x - Tanggal/Waktu: Day, dd Mon 20xx hh:ii:ss +0000 - Status CAPTCHA: Lulus!
```

*Direktif konfigurasi yang bertanggung jawab untuk pencatatan CAPTCHA adalah:*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 11.3.2 LOG BAGIAN DEPAN

Jenis pencatatan ini berhubungan dengan upaya masuk bagian depan, dan hanya terjadi ketika pengguna mencoba masuk ke bagian depan (dengan asumsi akses bagian depan diaktifkan).

Entri log untuk bagian depan berisi alamat IP pengguna yang mencoba masuk, tanggal dan waktu ketika itu terjadi, dan hasil dari upaya tersebut (berhasil masuk, atau gagal masuk). Entri log untuk bagian depan biasanya terlihat seperti ini (sebagai contoh):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Dimasuk.
```

*Direktif konfigurasi yang bertanggung jawab untuk pencatatan bagian depan adalah:*
- `general` -> `frontend_log`

##### 11.3.3 ROTASI LOG

Anda mungkin ingin membersihkan log setelah jangka waktu tertentu, atau mungkin diminta untuk melakukannya oleh hukum (yaitu, jumlah waktu yang diizinkan secara hukum bagi Anda untuk mempertahankan log mungkin dibatasi oleh hukum). Anda dapat mencapai ini dengan menyertakan penanda tanggal/waktu dalam nama-nama file log Anda sesuai yang ditentukan oleh konfigurasi paket Anda (misalnya, `{yyyy}-{mm}-{dd}.log`), dan kemudian mengaktifkan rotasi log (rotasi log memungkinkan Anda untuk melakukan beberapa tindakan pada file log ketika batas yang ditentukan terlampaui).

Sebagai contoh: Jika saya secara hukum diminta untuk menghapus log setelah 30 hari, saya bisa menentukan `{dd}.log` dalam nama file log saya (`{dd}` represents days), atur nilai `log_rotation_limit` ke 30, dan atur nilai `log_rotation_action` ke `Delete`.

Sebaliknya, jika Anda diminta untuk menyimpan log untuk jangka waktu yang panjang, Anda bisa memilih untuk tidak menggunakan rotasi log sama sekali, atau Anda bisa mengatur nilai `log_rotation_action` ke `Archive`, untuk mengompres file log, sehingga mengurangi jumlah total ruang disk yang mereka tempati.

*Direktif konfigurasi yang relevan:*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 11.3.4 PEMOTONGAN LOG

Ini juga memungkinkan untuk memotong file log individu ketika mereka melebihi ukuran tertentu, jika ini adalah sesuatu yang mungkin Anda butuhkan atau ingin lakukan.

*Direktif konfigurasi yang relevan:*
- `general` -> `truncate`

##### 11.3.5 PSEUDONIMISASI ALAMAT IP

Pertama, jika Anda tidak akrab dengan istilah ini, "pseudonimisasi" mengacu pada memproses data pribadi sedemikian rupa sehingga tidak dapat diidentifikasi ke subjek data tertentu lagi tanpa beberapa informasi tambahan, dan dengan ketentuan bahwa informasi tambahan tersebut dipelihara secara terpisah dan tunduk pada tindakan teknis dan organisasi untuk memastikan bahwa data pribadi tidak dapat diidentifikasi kepada orang alami.

Dalam beberapa keadaan, Anda mungkin diperlukan secara hukum untuk membuat dianonimisasi atau dipseudonimisasi setiap PII dikumpulkan, diproses, atau disimpan. Meskipun konsep ini telah ada untuk beberapa waktu sekarang, GDPR/DSGVO terutama menyebutkan, dan secara khusus mendorong "pseudonimisasi".

CIDRAM mampu mem-pseudonimisasi alamat IP ketika melakukan pencatatan, jika ini adalah sesuatu yang mungkin Anda butuhkan atau ingin lakukan. Ketika CIDRAM mem-pseudonimkan alamat IP, saat dicatat, oktet terakhir dari alamat IPv4, dan semuanya setelah bagian kedua dari alamat IPv6 diwakili oleh "x" (efektif membulatkan alamat IPv4 ke alamat awal dari subnet ke-24 dari faktor dimana mereka dimasukkan, dan alamat IPv6 ke alamat awal dari subnet ke-32 dari faktor dimana mereka dimasukkan).

*Catat: Proses pseudonimisasi alamat IP untuk CIDRAM tidak mempengaruhi fitur pelacakan IP untuk CIDRAM. Jika ini masalah bagi Anda, mungkin yang terbaik adalah menonaktifkan pelacakan IP sepenuhnya. Ini dapat dicapai dengan mengatur `track_mode` ke `false` dan dengan menghindari modul apapun.*

*Direktif konfigurasi yang relevan:*
- `signatures` -> `track_mode`
- `legal` -> `pseudonymise_ip_addresses`

##### 11.3.6 MENGHILANGKAN INFORMASI LOG

Jika Anda ingin melangkah lebih jauh dengan mencegah jenis informasi tertentu sedang dicatat sepenuhnya, ini juga mungkin dilakukan. CIDRAM menyediakan direktif-direktif konfigurasi untuk mengontrol apakah alamat IP, nama host, dan agen pengguna termasuk dalam log. Secara default, ketiga titik data ini termasuk dalam log bila tersedia. Menetapkan apapun direktif-direktif konfigurasi ini ke `true` akan menghilangkan informasi terkait dari log.

*Catat: Tidak ada alasan untuk menggunakan pseudonim dengan alamat IP ketika menghilangkannya dari log sepenuhnya.*

*Direktif konfigurasi yang relevan:*
- `legal` -> `omit_ip`
- `legal` -> `omit_hostname`
- `legal` -> `omit_ua`

##### 11.3.7 STATISTIK

CIDRAM secara opsional dapat melacak statistik seperti jumlah total kejadian blokir atau instance CAPTCHA yang telah terjadi sejak beberapa titik waktu tertentu. Fitur ini dinonaktifkan secara default, tetapi dapat diaktifkan melalui konfigurasi paket. Fitur ini hanya melacak jumlah total kejadian yang terjadi, dan tidak termasuk informasi apapun tentang kejadian tertentu (dan dengan demikian, tidak boleh dianggap sebagai PII).

*Direktif konfigurasi yang relevan:*
- `general` -> `statistics`

##### 11.3.8 ENKRIPSI

CIDRAM tidak mengenkripsi cache atau informasi log apapun. [Enkripsi](https://id.wikipedia.org/wiki/Enkripsi) cache dan log dapat diperkenalkan di masa depan, tetapi tidak ada rencana khusus untuk itu saat ini. Jika Anda khawatir tentang pihak ketiga yang tidak sah mendapatkan akses ke bagian depan dari CIDRAM yang mungkin berisi PII atau informasi sensitif seperti cache atau log-nya, saya akan merekomendasikan bahwa CIDRAM tidak diinstal di lokasi yang dapat diakses publik (misalnya, instal CIDRAM di luar direktori `public_html` standar atau yang setara dengan yang tersedia untuk sebagian besar web server standar) dan bahwa perizinan restriktif yang tepat diberlakukan untuk direktori tempat ia tinggal (khususnya, untuk direktori vault). Jika itu tidak cukup untuk mengatasi masalah Anda, konfigurasikan CIDRAM sedemikian rupa sehingga jenis informasi yang menyebabkan kekhawatiran Anda tidak akan dikumpulkan atau dicatat di tempat pertama (seperti, dengan menonaktifkan pencatatan).

#### 11.4 COOKIE

CIDRAM menetapkan [cookie](https://id.wikipedia.org/wiki/Kuki_HTTP) pada dua titik dalam basis kodenya. Pertama, ketika pengguna berhasil menyelesaikan instance CAPTCHA (dan mengasumsikan bahwa `lockuser` diatur ke `true`), CIDRAM menetapkan cookie agar dapat mengingat untuk permintaan berikutnya bahwa pengguna telah menyelesaikan instance CAPTCHA, sehingga tidak perlu meminta pengguna untuk menyelesaikan instance CAPTCHA pada permintaan berikutnya. Kedua, ketika pengguna berhasil masuk ke akses bagian depan, CIDRAM menetapkan cookie agar dapat mengingat pengguna untuk permintaan berikutnya (yaitu, cookie digunakan untuk mengotentikasi pengguna ke sesi masuk).

Dalam kedua kasus, peringatan cookie ditampilkan dengan jelas (bila berlaku), memperingatkan pengguna bahwa cookie akan diatur jika mereka terlibat dalam tindakan yang relevan. Cookie tidak diatur dalam titik lain di basis kode.

*Catat: CAPTCHA API "tak terlihat" mungkin tidak kompatibel dengan hukum cookie di beberapa yurisdiksi, dan harus dihindari oleh situs web apapun yang tunduk pada hukum-hukum tersebut. Memilih untuk menggunakan API lain yang disediakan, atau menonaktifkan CAPTCHA sepenuhnya, mungkin lebih disukai.*

*Direktif konfigurasi yang relevan:*
- `general` -> `disable_frontend`
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 11.5 PEMASARAN DAN PERIKLANAN

CIDRAM tidak mengumpulkan atau memproses informasi apapun untuk tujuan pemasaran atau periklanan, dan tidak menjual atau memperoleh keuntungan dari informasi yang dikumpulkan atau dicatat. CIDRAM bukan perusahaan komersial, juga tidak terkait dengan kepentingan komersial, sehingga melakukan hal-hal ini tidak akan masuk akal. Ini telah terjadi sejak awal proyek, dan terus menjadi kasus hari ini. Juga, melakukan hal-hal ini akan menjadi kontra-produktif terhadap semangat dan tujuan yang dimaksudkan dari proyek secara keseluruhan, dan selama saya terus mempertahankan proyek, tidak akan pernah terjadi.

#### 11.6 KEBIJAKAN PRIVASI

Dalam beberapa keadaan, Anda mungkin diharuskan secara hukum untuk secara jelas menampilkan tautan ke kebijakan privasi Anda pada semua halaman dan bagian dari situs web Anda. Ini mungkin penting sebagai sarana untuk memastikan bahwa pengguna mendapat informasi yang jelas tentang praktik privasi Anda, jenis PII yang Anda kumpulkan, dan bagaimana Anda akan menggunakannya. Agar dapat menyertakan tautan di halaman "Akses Ditolak" CIDRAM, direktif konfigurasi disediakan untuk menentukan URL ke kebijakan privasi Anda.

*Catat: Sangat disarankan agar halaman kebijakan privasi Anda tidak ditempatkan di belakang perlindungan CIDRAM. Jika CIDRAM melindungi halaman kebijakan privasi Anda, dan pengguna yang diblokir oleh CIDRAM mengklik tautan ke kebijakan privasi Anda, mereka akan diblokir lagi, dan tidak akan dapat melihat kebijakan privasi Anda. Idealnya, Anda harus menautkan ke salinan statis dari kebijakan privasi Anda, seperti halaman HTML atau file teks biasa yang tidak dilindungi oleh CIDRAM.*

*Direktif konfigurasi yang relevan:*
- `legal` -> `privacy_policy`

#### 11.7 GDPR/DSGVO

Regulasi Perlindungan Data Umum (GDPR) adalah regulasi dari Uni Eropa, yang mulai berlaku pada 25 Mei 2018. Tujuan utama dari regulasi ini adalah untuk memberikan kontrol kepada warga dan penduduk negara Uni Eropa mengenai data pribadi mereka sendiri, dan untuk menyatukan regulasi di Uni Eropa terkait privasi dan data pribadi.

Regulasi ini tersebut berisi ketentuan khusus yang berkaitan dengan pemrosesan "informasi identitas pribadi" (PII) dari setiap "subjek data" (setiap orang alami yang teridentifikasi atau dapat diidentifikasi) dari atau di dalam Uni Eropa. Agar sesuai dengan regulasi, "perusahaan" atau "enterprise" (sesuai yang didefinisikan oleh regulasi), dan sistem dan proses yang relevan harus mengimplementasikan "privasi berdasarkan desain" secara default, harus menggunakan pengaturan privasi setinggi mungkin, harus mengimplementasikan pengamanan yang diperlukan untuk informasi yang disimpan atau diproses (termasuk, tetapi tidak terbatas pada, mengimplementasikan pseudonimisasi atau anonimisasi yang penuh untuk data), harus jelas dan tidak ambigu menyatakan jenis data yang mereka kumpulkan, bagaimana mereka memprosesnya, untuk alasan apa, untuk berapa lama mereka menyimpannya, dan apakah mereka membagikan data ini dengan pihak ketiga manapun, jenis data yang dibagikan dengan pihak ketiga, bagaimana, mengapa, dan sebagainya.

Data tidak dapat diproses kecuali jika ada dasar yang sah untuk melakukannya, sesuai yang didefinisikan oleh regulasi. Umumnya, ini berarti bahwa untuk memproses data data subjek secara sah, itu harus dilakukan sesuai dengan kewajiban hukum, atau dilakukan hanya setelah persetujuan eksplisit, terinformasi dengan baik, dan tidak ambigu diperoleh dari subjek data.

Karena aspek regulasi dapat berevolusi dalam waktu, untuk menghindari penyebaran informasi yang ketinggalan jaman, mungkin lebih baik untuk belajar tentang regulasi dari sumber yang berwenang, dibandingkan dengan hanya memasukkan informasi yang relevan disini dalam dokumentasi paket (yang akhirnya bisa menjadi usang seiring berkembangnya regulasi).

Beberapa sumber bacaan yang direkomendasikan untuk mempelajari informasi lebih lanjut:
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [Regulasi Perlindungan Data](https://id.wikipedia.org/wiki/Regulasi_Perlindungan_Data)

---


Terakhir Diperbarui: 27 Juli 2022 (2022.07.27).

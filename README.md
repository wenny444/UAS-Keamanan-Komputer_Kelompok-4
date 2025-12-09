#  Penetration Testing: Pendeteksi Asap Rokok Otomatis (ESP8266)

----

##  👥 Anggota Kelompok V

| No | Nama | NIM |
|----|------|-----|
| 1. | **Alvita Revina** | 09030282327008 |
| 2. | **Wenny Arthaliawati** | 09030282327011 |
| 3. | **Syai Dean Putri** | 09030282327044 |
| 4. | **Komala Maysaroh** | 0903058327086 |
| 5. | **Alwaan Faramesta** | 09030582327110 |
| 6. | **M. Rifki Putra Pradana** | 09030282327116 |

----

## Latar Belakang dan Tujuan
Web server merupakan komponen utama dalam layanan berbasis jaringan. Namun, server sering menjadi target serangan yang bertujuan membuatnya tidak dapat memberikan layanan kepada pengguna. Salah satu teknik serangan yang umum adalah SYN Flood, yaitu serangan yang membanjiri server dengan permintaan koneksi palsu hingga server kehabisan sumber daya.

**Tujuan Pengujian:**
1. Mengidentifikasi respons server ketika terjadi serangan SYN Flood.
2. Mendapatkan insight mengenai potensi kelemahan dan kebutuhan mekanisme mitigasi.
3. Memberikan pembelajaran mengenai cara kerja serangan.

----

## Target Pengujian
Target pengujian berfokus pada sisi software dan network yang beroperasi pada perangkat keras tersebut.
* **Perangkat:** ESP8266 Web Server (Pendeteksi Asap Rokok Otomatis)
* **Fitur Web:** Dashboard Monitoring
* **IP target:** 10.239.234.59
* **Port terbuka:** 80/tcp (HTTP)

**Deskripsi Web Service:**
Web Service ini dirancang sebagai pusat monitoring (*dashboard*) yang menampilkan data secara *real-time*.

| Tampilan Dashboard Monitoring |
| :---: |
|![WhatsApp Image 2025-12-10 at 03 54 11_b7f49240](https://github.com/user-attachments/assets/86e58261-a92f-4549-944d-241bad80b6c2)|

## Skenario Serangan 1: Brute Force Attack

### Apa itu DoS SYN flood?
DoS SYN Flood adalah salah satu bentuk serangan Denial of Service (DoS) yang menargetkan kelemahan dalam proses TCP three-way handshake pada komunikasi jaringan.

----

### Langkah-langkah Pengujian

#### 1. Pertama, perangkat penguji perlu terhubung ke jaringan Wi-Fi yang digunakan oleh modul ESP. 
Koneksi ini diperlukan agar penguji dapat berada pada satu segmen jaringan yang sama dengan target.

#### 2. Laptop kemudian harus terhubung ke hotspot yang berasal dari ponsel.
karena ponsel tersebut sebelumnya sudah terhubung dengan jaringan ESP. Setelah koneksi berhasil, penguji dapat membuka Windows PowerShell dan menampilkan daftar perangkat yang ada di jaringan menggunakan perintah untuk melihat tabel ARP. Dengan menjalankan perintah ```arp -a``` 

|![WhatsApp Image 2025-12-10 at 03 24 20_3beaa710](https://github.com/user-attachments/assets/fd563051-0183-42d4-85b7-55a272c86e93)
|

#### 3. Jika muncul banyak alamat IP, setiap entri perlu diidentifikasi satu per satu.
untuk memastikan mana yang merupakan alamat perangkat ESP yang menjadi target pengujian.

#### 4. Proses identifikasi lebih lanjut dilakukan menggunakan Kali Linux.
yaitu dengan melakukan pemetaan port dan layanan pada setiap IP yang mencurigakan menggunakan teknik pemindaian SYN berbasis keamanan (SYN scanning). Dengan menjalankan perintah ```nmap -sS -Pn 10.239.234.59```

|![WhatsApp Image 2025-12-10 at 03 24 22_c29c6c10](https://github.com/user-attachments/assets/f80fd012-cfaa-40d0-8b07-d3d95420c992)
|

#### 5. Setelah alamat IP target berhasil dipastikan, barulah dilakukan pengujian ketahanan server.
menggunakan tool pengujian jaringan yang mampu mensimulasikan beban lalu lintas paket SYN dalam jumlah besar ke port layanan tertentu dalam studi ini biasanya port layanan web.

#### 6. Hasil pengujian menunjukkan bahwa serangan SYN flood dapat menyebabkan perangkat mengalami overload.
sehingga respons menjadi sangat lambat atau server berhenti merespons. Kondisi ini dapat diibaratkan seperti perangkat yang “menyala tetapi tidak dapat berpikir”, karena sumber dayanya habis untuk memproses permintaan palsu.

----

## Kesimpulan
Pengujian penetrasi pada web server detektor asap menggunakan serangan DoS SYN Flood menunjukkan sejauh mana server mampu mempertahankan ketersediaan layanan saat dibanjiri permintaan koneksi palsu. Jika server rentan, serangan ini dapat memenuhi buffer koneksi sehingga layanan web termasuk tampilan data sensor dan notifikasi menjadi tidak dapat diakses. Namun, jika server memiliki mekanisme pertahanan seperti SYN cookies atau rate limiting, dampak dapat diminimalkan meski penggunaan sumber daya meningkat. Hasil ini menegaskan perlunya penguatan konfigurasi keamanan jaringan untuk mencegah gangguan pada fungsi kritis detektor asap.

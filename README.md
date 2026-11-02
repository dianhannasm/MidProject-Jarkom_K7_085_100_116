# MidProject-Jarkom_K7_085_100_116

# Soal 1 - Topologi

Pada implementasi jaringan Smart City Kota Surabaya, kelompok menggunakan skema **Classless Inter-Domain Routing (CIDR)** sebagai metode pengalamatan jaringan.

CIDR dipilih karena memungkinkan penggunaan prefix yang berbeda sesuai kebutuhan jumlah host pada setiap subnet. Dengan demikian, alokasi alamat IP dapat disesuaikan dengan skala masing-masing jaringan, mulai dari jaringan WiFi publik dengan kebutuhan host yang besar hingga jaringan server dan koneksi antar-router dengan kebutuhan host yang lebih kecil.

Jaringan menggunakan blok alamat `10.56.0.0/15` yang dibagi menjadi beberapa subnet untuk masing-masing lokasi. Setiap LAN menggunakan alamat host pertama sebagai default gateway sesuai ketentuan tugas.

### Desain Topologi Jaringan

<img width="508" height="318" alt="image" src="https://github.com/user-attachments/assets/df919c3c-0454-4ce0-8517-dbc4c2d1a77e" />


Topologi jaringan dirancang menggunakan pendekatan hierarkis dengan R-PUSAT sebagai router utama yang menghubungkan beberapa wilayah, yaitu DC, Utara, Barat, Timur, Selatan, dan Pelabuhan.

Secara keseluruhan, perangkat jaringan terdiri atas delapan router, switch, perangkat pengguna, access point, dan server. Setiap lokasi memiliki router yang berfungsi sebagai penghubung antara jaringan lokal dengan jaringan backbone.

R-PUSAT berfungsi sebagai pusat konektivitas yang menghubungkan router-router wilayah lainnya serta R-ISP untuk akses menuju jaringan internet. Sementara itu, R-UTARA berfungsi sebagai penghubung tambahan menuju R-PELABUHAN melalui link L6.

### Pertimbangan Pemilihan Perangkat

| Perangkat | Pertimbangan Pemilihan |
|---|---|
| Cisco 2911 Router | Digunakan sebagai perangkat routing untuk menghubungkan beberapa subnet dan jaringan antarwilayah. |
| Cisco 2960 Switch | Digunakan untuk menghubungkan beberapa perangkat dalam satu LAN melalui koneksi kabel. |
| PC-PT | Digunakan sebagai perangkat perwakilan untuk jaringan pengguna atau perangkat monitoring pada setiap LAN. |
| Server-PT | Digunakan untuk menyediakan layanan jaringan seperti DNS, web, FTP, email, DHCP, dan server internet sesuai pembagian layanan. |
| Access Point-PT | Digunakan untuk menyediakan konektivitas wireless pada jaringan WiFi publik. |
| Laptop-PT | Digunakan sebagai perangkat perwakilan pengguna yang mengakses jaringan melalui koneksi wireless. |

### Pertimbangan Media Koneksi

Media koneksi dipilih berdasarkan kebutuhan komunikasi antarperangkat dan karakteristik masing-masing jaringan.

**a. Koneksi Backbone Antar-Router**

Backbone L1–L6 menggunakan kabel serial dengan modul HWIC-2T pada router Cisco 2911. Media ini dipilih sebagai desain koneksi point-to-point antar-router untuk menghubungkan jaringan di berbagai wilayah.

Penambahan modul HWIC-2T dilakukan karena router Cisco 2911 yang digunakan memerlukan antarmuka serial tambahan untuk mendukung koneksi backbone. R-PUSAT menggunakan tiga modul HWIC-2T untuk memenuhi kebutuhan enam port serial, sedangkan router lainnya menggunakan satu modul sesuai kebutuhan koneksinya.

**b. Koneksi Router ke Switch**

Koneksi antara router dan switch menggunakan kabel Copper Straight-Through. Media ini digunakan untuk menghubungkan interface GigabitEthernet pada router dengan interface FastEthernet pada switch sehingga masing-masing LAN dapat terhubung ke gateway-nya.

**c. Koneksi Switch ke Perangkat LAN**

Koneksi antara switch dengan PC, server, dan access point menggunakan kabel Copper Straight-Through. Penggunaan koneksi kabel dipilih untuk menyediakan jalur komunikasi langsung bagi perangkat dalam jaringan lokal.

**d. Koneksi Wireless**

Jaringan WiFi publik di wilayah Utara, Barat, Timur, dan Selatan menggunakan Access Point sebagai penyedia akses wireless. Laptop digunakan sebagai perangkat perwakilan pengguna yang terhubung ke Access Point tanpa memerlukan kabel fisik.

Pemilihan wireless bertujuan memberikan fleksibilitas konektivitas bagi pengguna yang mengakses jaringan publik.

### Pertimbangan Pembagian Switch dan LAN

Setiap wilayah memiliki switch yang dipisahkan berdasarkan subnet atau fungsi jaringan. Pemisahan ini dilakukan agar perangkat dalam satu kelompok jaringan terhubung melalui switch masing-masing.

Sebagai contoh, wilayah DC memiliki SW-CCTV dan SW-SERVER-DC. Keduanya digunakan untuk menghubungkan perangkat pada subnet CCTV Kota serta Server dan Storage DC.

Pembagian serupa diterapkan pada wilayah lainnya, seperti WiFi publik, jaringan sensor, jaringan perkantoran, dan jaringan server.

Pemisahan switch tersebut membantu pengelolaan perangkat berdasarkan fungsi dan subnet masing-masing serta memudahkan proses konfigurasi dan pengujian jaringan.

### Pertimbangan Jumlah Perangkat Perwakilan

Dalam implementasi menggunakan Cisco Packet Tracer, kelompok hanya memasang satu perangkat perwakilan untuk setiap LAN sesuai ketentuan tugas.

Meskipun demikian, perhitungan subnet tetap menggunakan seluruh kebutuhan host yang telah ditentukan pada UTS. Oleh karena itu, jumlah perangkat yang ditampilkan dalam simulasi tidak merepresentasikan keseluruhan kapasitas atau kebutuhan host pada jaringan sebenarnya.

Pendekatan ini digunakan untuk menyederhanakan simulasi tanpa mengubah perencanaan pengalamatan jaringan.

### Kesimpulan Desain

Desain topologi ini dibuat untuk merepresentasikan jaringan Smart City Kota Surabaya yang menghubungkan berbagai wilayah melalui jaringan backbone dengan R-PUSAT sebagai pusat konektivitas.

Penggunaan router, switch, server, access point, serta kombinasi media kabel dan wireless disesuaikan dengan kebutuhan masing-masing jaringan. Dengan desain tersebut, jaringan diharapkan dapat mendukung komunikasi antarwilayah, akses pengguna, serta penyediaan layanan jaringan sesuai ketentuan Mid-Project Komunikasi Data dan Jaringan Komputer.
  
# Soal 3 - Static Routing

Konfigurasi static routing dilakukan agar seluruh jaringan LAN pada topologi Smart City Surabaya dapat saling berkomunikasi melalui router yang terhubung. Setiap router diberikan rute menuju jaringan yang tidak terhubung secara langsung menggunakan static route.

Sesuai ketentuan soal, R-PUSAT dan R-UTARA harus memiliki static route menuju seluruh jaringan LAN yang berada di bawah router cabangnya. Selain itu, setiap router cabang menggunakan default route untuk meneruskan paket menuju jaringan di luar jaringan lokalnya.

### Konfigurasi Interface Router

Sebelum melakukan konfigurasi routing, setiap interface router diberikan alamat IP statis sesuai tabel subnetting CIDR yang telah dibuat pada Soal 2.

Interface LAN berfungsi sebagai gateway bagi perangkat pengguna, sedangkan interface serial digunakan untuk menghubungkan router-router pada backbone jaringan.

Seluruh interface yang digunakan telah dikonfigurasi dan menunjukkan status `up/up` berdasarkan pemeriksaan menggunakan perintah:

```cisco
show ip interface brief
```

### Konfigurasi Static Route pada R-PUSAT

R-PUSAT berfungsi sebagai router pusat yang menghubungkan jaringan Balai Kota dengan router-router cabang lainnya. Oleh karena itu, R-PUSAT dikonfigurasi dengan static route menuju seluruh LAN yang berada di bawah R-DC, R-UTARA, R-BARAT, R-TIMUR, R-SELATAN, dan R-PELABUHAN.

Berikut daftar static route pada R-PUSAT:

| Jaringan Tujuan | Next Hop | Keterangan |
|---|---|---|
| 10.56.128.0/19 | 10.56.161.2 | LAN CCTV Kota |
| 10.56.160.0/24 | 10.56.161.2 | LAN Server dan Storage DC |
| 10.56.0.0/18 | 10.56.66.2 | LAN WiFi Publik Utara |
| 10.56.64.0/23 | 10.56.66.2 | LAN Sensor Lalu Lintas Utara |
| 10.56.192.0/19 | 10.56.225.2 | LAN WiFi Publik Barat |
| 10.56.224.0/24 | 10.56.225.2 | LAN Puskesmas dan Sekolah Barat |
| 10.57.0.0/19 | 10.57.36.2 | LAN WiFi Publik Timur |
| 10.57.32.0/22 | 10.57.36.2 | LAN Sensor Banjir Timur |
| 10.57.64.0/19 | 10.57.96.130 | LAN WiFi Publik Selatan |
| 10.57.96.0/25 | 10.57.96.130 | LAN PJU Pintar Selatan |
| 10.57.128.0/19 | 10.56.66.2 | LAN Sensor dan SCADA Pelabuhan |
| 10.57.160.0/25 | 10.56.66.2 | LAN Kantor Pelabuhan |
| 10.57.160.128/30 | 10.56.66.2 | Link L6 menuju R-PELABUHAN |

Selain static route menuju jaringan cabang, R-PUSAT juga dikonfigurasi dengan default route menuju R-ISP menggunakan perintah:

```cisco
ip route 0.0.0.0 0.0.0.0 203.0.113.30
```

Default route tersebut digunakan untuk meneruskan paket menuju jaringan di luar jaringan internal Smart City melalui R-ISP.  

<img width="523" height="529" alt="Screenshot 2026-11-02 184955" src="https://github.com/user-attachments/assets/3fc9a3a0-dd28-4f50-bd0f-07d4bf882bdb" />  

R-PUSAT memiliki static route menuju seluruh LAN cabang dan default route menuju R-ISP.

### Konfigurasi Static Route pada R-UTARA

R-UTARA memiliki dua jaringan LAN lokal, yaitu WiFi Publik Utara dan Sensor Lalu Lintas Utara. R-UTARA juga terhubung ke R-PELABUHAN melalui link L6.

Sesuai ketentuan soal, R-UTARA dikonfigurasi dengan static route menuju seluruh LAN milik R-PELABUHAN.

Konfigurasi static route:

```cisco
ip route 10.57.128.0 255.255.224.0 10.57.160.130
ip route 10.57.160.0 255.255.255.128 10.57.160.130
```

Default route pada R-UTARA diarahkan menuju R-PUSAT:

```cisco
ip route 0.0.0.0 0.0.0.0 10.56.66.1
```

Dengan demikian, R-UTARA dapat meneruskan paket menuju jaringan Pelabuhan melalui L6 dan meneruskan paket menuju jaringan lainnya melalui R-PUSAT.

<img width="527" height="314" alt="Screenshot 2026-11-02 185122" src="https://github.com/user-attachments/assets/7448d760-827f-4d6d-a958-3a1653e8df1d" />  
  
R-UTARA memiliki static route menuju LAN Sensor dan SCADA Pelabuhan serta LAN Kantor Pelabuhan.  

### Konfigurasi Default Route pada Router Cabang

Router cabang lainnya dikonfigurasi menggunakan default route menuju router yang menjadi jalur keluar atau upstream masing-masing.

| Router | Default Route / Next Hop | Tujuan |
|---|---|---|
| R-DC | 10.56.161.1 | Menuju R-PUSAT melalui L1 |
| R-BARAT | 10.56.225.1 | Menuju R-PUSAT melalui L5 |
| R-TIMUR | 10.57.36.1 | Menuju R-PUSAT melalui L4 |
| R-SELATAN | 10.57.96.129 | Menuju R-PUSAT melalui L3 |
| R-PELABUHAN | 10.57.160.129 | Menuju R-UTARA melalui L6 |

Contoh konfigurasi default route pada R-PELABUHAN:

```cisco
ip route 0.0.0.0 0.0.0.0 10.57.160.129
```

Konfigurasi tersebut memungkinkan router cabang meneruskan paket menuju jaringan yang tidak tercantum sebagai jaringan lokal maupun static route khusus melalui router upstream.

<img width="521" height="256" alt="image" src="https://github.com/user-attachments/assets/7b1d7e3b-18b1-42b5-8988-c0814af33f86" />  
  
Router cabang memiliki default route menuju router upstream masing-masing.  
Jaringan yang terhubung langsung ditampilkan sebagai connected route, sedangkan jaringan yang dikonfigurasi secara manual ditampilkan sebagai static route.  

### Pengujian Konektivitas

Pengujian dilakukan menggunakan perintah `ping` untuk memastikan bahwa perangkat dan router dapat menjangkau jaringan tujuan.

Beberapa hasil pengujian yang berhasil:

| Sumber Pengujian | Tujuan | Hasil |
|---|---|---|
| PC-PEGAWAI | Gateway CCTV Kota (10.56.128.1) | Berhasil |
| PC-CCTV-KOTA | PC-PEGAWAI (10.57.192.2) | Berhasil |
| PC-PEGAWAI | Gateway WiFi Publik Utara (10.56.0.1) | Berhasil |
| PC-PEGAWAI | Gateway WiFi Publik Barat (10.56.192.1) | Berhasil |
| PC-PEGAWAI | Gateway WiFi Publik Timur (10.57.0.1) | Berhasil |
| PC-PEGAWAI | Gateway WiFi Publik Selatan (10.57.64.1) | Berhasil |
| PC-PEGAWAI | Gateway Puskesmas dan Sekolah Barat (10.56.224.1) | Berhasil |
| PC-PEGAWAI | Gateway Sensor Banjir Timur (10.57.32.1) | Berhasil |
| PC-PEGAWAI | Gateway Sensor Lalu Lintas Utara (10.56.64.1) | Berhasil |
| PC-PEGAWAI | Gateway PJU Pintar Selatan (10.57.96.1) | Berhasil |
| PC-PEGAWAI | Gateway Sensor dan SCADA Pelabuhan (10.57.128.1) | Berhasil |
| PC-PEGAWAI | Gateway Kantor Pelabuhan (10.57.160.1) | Berhasil |
| PC-PEGAWAI | Gateway Server dan Storage DC (10.56.160.1) | Berhasil |
| PC-PEGAWAI | Gateway Server Balai Kota (10.57.200.1) | Berhasil |  

<img width="524" height="530" alt="ping-pgwai" src="https://github.com/user-attachments/assets/bfd2bb58-2474-421f-bbe1-4dd515961695" />  
<img width="524" height="528" alt="ping-from-cctv-to-pegawai" src="https://github.com/user-attachments/assets/dce86cd7-349c-4e76-beba-dd9f84cd3e72" />  

Pengujian tambahan dilakukan dari R-UTARA menuju gateway LAN Pelabuhan:

- `ping 10.57.128.1` — berhasil.
- `ping 10.57.160.1` — berhasil.
  
<img width="521" height="220" alt="image" src="https://github.com/user-attachments/assets/997527b7-3f54-4bac-a234-5c22660b431a" />  

Pengujian dari R-PELABUHAN menuju gateway LAN Pegawai Balai Kota juga berhasil setelah penambahan static route untuk jaringan link L6 pada R-PUSAT.  
<img width="523" height="141" alt="image" src="https://github.com/user-attachments/assets/e5fe4d84-88f1-4fe9-bbd5-8d54c502be1c" />  

Hasil pengujian tersebut menunjukkan bahwa routing antarjaringan telah berjalan sesuai jalur yang dikonfigurasi.  

# Soal 4 - Konfigurasi DHCP (Dynamic Host Configuration Protocol)

Konfigurasi DHCP dilakukan untuk memberikan alamat IP secara otomatis kepada perangkat pengguna pada jaringan Smart City Surabaya. Setiap perangkat pengguna memperoleh konfigurasi jaringan berupa IP Address, Subnet Mask, Default Gateway, dan DNS Server tanpa perlu melakukan pengaturan secara manual.

Sesuai ketentuan soal, seluruh interface router dan server menggunakan alamat IP statis. Khusus subnet CCTV Kota, alokasi alamat IP dilakukan oleh DHCP Server yang berada di LAN Server dan Storage DC, bukan oleh router.

Implementasi DHCP dilakukan menggunakan dua metode, yaitu DHCP Server pada SERVER-DC untuk subnet CCTV Kota dan DHCP pool pada masing-masing router untuk LAN pengguna lainnya.

### Konfigurasi IP Statis Server

Sebelum mengaktifkan layanan DHCP, kedua server dikonfigurasi menggunakan alamat IP statis.

| Perangkat | IP Address | Subnet Mask | Default Gateway | DNS Server |
|---|---|---|---|---|
| SERVER-DC | 10.56.160.2 | 255.255.255.0 | 10.56.160.1 | 10.56.160.2 |
| SERVER-BALAI | 10.57.200.2 | 255.255.255.224 | 10.57.200.1 | 10.56.160.2 |

### DHCP Server untuk CCTV Kota

DHCP Server dikonfigurasi pada SERVER-DC yang terhubung ke LAN Server dan Storage DC. Pada menu **Services → DHCP**, layanan DHCP diaktifkan dan dibuat pool dengan nama `CCTV_POOL`.

Konfigurasi pool CCTV Kota:

| Parameter | Nilai |
|---|---|
| Pool Name | CCTV_POOL |
| Default Gateway | 10.56.128.1 |
| DNS Server | 10.56.160.2 |
| Start IP Address | 10.56.128.10 |
| Subnet Mask | 255.255.224.0 |
| Maximum Users | 6000 |
| DHCP Service | On |

Agar permintaan DHCP dari subnet CCTV Kota dapat diteruskan menuju SERVER-DC yang berada di subnet berbeda, dilakukan konfigurasi DHCP Relay pada interface G0/0 milik R-DC menggunakan perintah:

```cisco
interface gigabitEthernet 0/0
ip helper-address 10.56.160.2
```

Dengan konfigurasi tersebut, permintaan DHCP dari perangkat CCTV diteruskan oleh R-DC ke SERVER-DC. Dengan demikian, alamat IP CCTV Kota diperoleh dari DHCP Server, bukan dari router.

### DHCP pada Router untuk LAN Pengguna Lainnya

Untuk LAN pengguna selain CCTV Kota, DHCP dikonfigurasi secara lokal pada router yang menjadi gateway masing-masing subnet.

Sebelum membuat DHCP pool, alamat IP 10.1 sampai 10.9 pada setiap subnet dikecualikan dari pembagian DHCP. Hal ini bertujuan untuk menghindari konflik dengan alamat gateway dan alamat yang disediakan untuk kebutuhan statis.

Konfigurasi DHCP menggunakan tiga parameter utama:
- `network` untuk menentukan network ID dan subnet mask.
- `default-router` untuk memberikan alamat gateway kepada perangkat pengguna.
- `dns-server` untuk memberikan alamat DNS Server, yaitu 10.56.160.2.

Berikut daftar DHCP pool yang dikonfigurasi:

| Router | Nama DHCP Pool | Network ID / Prefix | Gateway | Awal IP DHCP |
|---|---|---|---|---|
| R-PUSAT | PEGAWAI_BALAI | 10.57.192.0/21 | 10.57.192.1 | 10.57.192.10 |
| R-UTARA | WIFI_UTARA | 10.56.0.0/18 | 10.56.0.1 | 10.56.0.10 |
| R-UTARA | SENSOR_LALIN_UTARA | 10.56.64.0/23 | 10.56.64.1 | 10.56.64.10 |
| R-BARAT | WIFI_BARAT | 10.56.192.0/19 | 10.56.192.1 | 10.56.192.10 |
| R-BARAT | PUSKESMAS_SEKOLAH | 10.56.224.0/24 | 10.56.224.1 | 10.56.224.10 |
| R-TIMUR | WIFI_TIMUR | 10.57.0.0/19 | 10.57.0.1 | 10.57.0.10 |
| R-TIMUR | SENSOR_BANJIR_TIMUR | 10.57.32.0/22 | 10.57.32.1 | 10.57.32.10 |
| R-SELATAN | WIFI_SELATAN | 10.57.64.0/19 | 10.57.64.1 | 10.57.64.10 |
| R-SELATAN | PJU_SELATAN | 10.57.96.0/25 | 10.57.96.1 | 10.57.96.10 |
| R-PELABUHAN | SENSOR_SCADA_PELABUHAN | 10.57.128.0/19 | 10.57.128.1 | 10.57.128.10 |
| R-PELABUHAN | KANTOR_PELABUHAN | 10.57.160.0/25 | 10.57.160.1 | 10.57.160.10 |

DNS Server pada seluruh DHCP pool diarahkan ke alamat 10.56.160.2, yaitu SERVER-DC. Alamat tersebut dipersiapkan untuk layanan DNS pada Soal 8.

### Pengujian DHCP

Pengujian dilakukan dengan mengubah konfigurasi IPv4 pada setiap perangkat pengguna menjadi DHCP melalui menu **Desktop → IP Configuration**. Hasil pengujian menunjukkan bahwa seluruh perangkat perwakilan memperoleh alamat IP secara otomatis beserta subnet mask, default gateway, dan DNS Server yang sesuai dengan subnet masing-masing.

### Hasil Pengujian Perangkat Pengguna

| No. | Perangkat | IPv4 Address yang Diperoleh | Gateway | Hasil |
|---|---|---|---|---|
| 1 | PC-PEGAWAI | 10.57.192.10 | 10.57.192.1 | Berhasil |
| 2 | LAPTOP-WIFI-UTARA | 10.56.0.10 | 10.56.0.1 | Berhasil |
| 3 | PC-SENSOR-LALIN | 10.56.64.10 | 10.56.64.1 | Berhasil |
| 4 | LAPTOP-WIFI-BARAT | 10.56.192.10 | 10.56.192.1 | Berhasil |
| 5 | PC-PUSKESMAS | 10.56.224.10 | 10.56.224.1 | Berhasil |
| 6 | LAPTOP-WIFI-TIMUR | 10.57.0.10 | 10.57.0.1 | Berhasil |
| 7 | PC-SENSOR-BANJIR | 10.57.32.10 | 10.57.32.1 | Berhasil |
| 8 | LAPTOP-WIFI-SELATAN | 10.57.64.10 | 10.57.64.1 | Berhasil |
| 9 | PC-PJU | 10.57.96.10 | 10.57.96.1 | Berhasil |
| 10 | PC-SCADA | 10.57.128.10 | 10.57.128.1 | Berhasil |
| 11 | PC-KANTOR-PELABUHAN | 10.57.160.10 | 10.57.160.1 | Berhasil |
| 12 | PC-CCTV-KOTA | 10.56.128.10 | 10.56.128.1 | Berhasil |

Beberapa contoh hasil pengujian:  
<img width="518" height="185" alt="Screenshot 2026-11-02 183120" src="https://github.com/user-attachments/assets/d59610d0-ce84-4858-9175-fb1f813379d9" />  
<img width="524" height="178" alt="Screenshot 2026-11-02 182944" src="https://github.com/user-attachments/assets/7fcb418f-6cd8-49a4-a764-5cad03cf2bc3" />  
<img width="518" height="177" alt="Screenshot 2026-11-02 183024" src="https://github.com/user-attachments/assets/2a4af0e5-7cd2-402f-a507-d925a919269f" />  
<img width="523" height="187" alt="Screenshot 2026-11-02 183110" src="https://github.com/user-attachments/assets/7d6a257a-e322-4766-90f7-0052b273c919" />  
<img width="524" height="182" alt="Screenshot 2026-11-02 183038" src="https://github.com/user-attachments/assets/ab41d754-b9f1-4e8e-b678-d5ae2912bc54" />  

Seluruh perangkat memperoleh DNS Server 10.56.160.2. Pada setiap perangkat, proses pengujian menampilkan pesan **DHCP request successful**.

### Verifikasi DHCP Binding

Selain melalui IP Configuration pada perangkat pengguna, pemberian alamat IP juga diverifikasi melalui perintah `show ip dhcp binding` pada router.

Contoh hasil verifikasi pada R-PUSAT:

<img width="521" height="250" alt="image" src="https://github.com/user-attachments/assets/4f68f5c2-44fa-4ad9-b362-0fe306b603df" />


Hasil tersebut menunjukkan bahwa alamat 10.57.192.10 telah tercatat sebagai alamat yang diberikan secara otomatis kepada PC-PEGAWAI.

Verifikasi pada R-PELABUHAN:

<img width="522" height="216" alt="image" src="https://github.com/user-attachments/assets/84528e1b-4214-4c48-9c4e-b97254116516" />


Hasil tersebut membuktikan bahwa PC-SCADA dan PC-KANTOR-PELABUHAN telah memperoleh alamat IP melalui DHCP pada R-PELABUHAN.


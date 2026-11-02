# MidProject-Jarkom_K7_085_100_116

## 1. Penjelasan Desain Topologi

### 1.1 Pemilihan Skema Pengalamatan

Pada implementasi jaringan Smart City Kota Surabaya, kelompok menggunakan skema **Classless Inter-Domain Routing (CIDR)** sebagai metode pengalamatan jaringan.

CIDR dipilih karena memungkinkan penggunaan prefix yang berbeda sesuai kebutuhan jumlah host pada setiap subnet. Dengan demikian, alokasi alamat IP dapat disesuaikan dengan skala masing-masing jaringan, mulai dari jaringan WiFi publik dengan kebutuhan host yang besar hingga jaringan server dan koneksi antar-router dengan kebutuhan host yang lebih kecil.

Jaringan menggunakan blok alamat `10.56.0.0/15` yang dibagi menjadi beberapa subnet untuk masing-masing lokasi. Setiap LAN menggunakan alamat host pertama sebagai default gateway sesuai ketentuan tugas.

### 1.2 Desain Topologi Jaringan

<img width="508" height="318" alt="image" src="https://github.com/user-attachments/assets/df919c3c-0454-4ce0-8517-dbc4c2d1a77e" />


Topologi jaringan dirancang menggunakan pendekatan hierarkis dengan R-PUSAT sebagai router utama yang menghubungkan beberapa wilayah, yaitu DC, Utara, Barat, Timur, Selatan, dan Pelabuhan.

Secara keseluruhan, perangkat jaringan terdiri atas delapan router, switch, perangkat pengguna, access point, dan server. Setiap lokasi memiliki router yang berfungsi sebagai penghubung antara jaringan lokal dengan jaringan backbone.

R-PUSAT berfungsi sebagai pusat konektivitas yang menghubungkan router-router wilayah lainnya serta R-ISP untuk akses menuju jaringan internet. Sementara itu, R-UTARA berfungsi sebagai penghubung tambahan menuju R-PELABUHAN melalui link L6.

### 1.3 Pertimbangan Pemilihan Perangkat

| Perangkat | Pertimbangan Pemilihan |
|---|---|
| Cisco 2911 Router | Digunakan sebagai perangkat routing untuk menghubungkan beberapa subnet dan jaringan antarwilayah. |
| Cisco 2960 Switch | Digunakan untuk menghubungkan beberapa perangkat dalam satu LAN melalui koneksi kabel. |
| PC-PT | Digunakan sebagai perangkat perwakilan untuk jaringan pengguna atau perangkat monitoring pada setiap LAN. |
| Server-PT | Digunakan untuk menyediakan layanan jaringan seperti DNS, web, FTP, email, DHCP, dan server internet sesuai pembagian layanan. |
| Access Point-PT | Digunakan untuk menyediakan konektivitas wireless pada jaringan WiFi publik. |
| Laptop-PT | Digunakan sebagai perangkat perwakilan pengguna yang mengakses jaringan melalui koneksi wireless. |

### 1.4 Pertimbangan Media Koneksi

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

### 1.5 Pertimbangan Pembagian Switch dan LAN

Setiap wilayah memiliki switch yang dipisahkan berdasarkan subnet atau fungsi jaringan. Pemisahan ini dilakukan agar perangkat dalam satu kelompok jaringan terhubung melalui switch masing-masing.

Sebagai contoh, wilayah DC memiliki SW-CCTV dan SW-SERVER-DC. Keduanya digunakan untuk menghubungkan perangkat pada subnet CCTV Kota serta Server dan Storage DC.

Pembagian serupa diterapkan pada wilayah lainnya, seperti WiFi publik, jaringan sensor, jaringan perkantoran, dan jaringan server.

Pemisahan switch tersebut membantu pengelolaan perangkat berdasarkan fungsi dan subnet masing-masing serta memudahkan proses konfigurasi dan pengujian jaringan.

### 1.6 Pertimbangan Jumlah Perangkat Perwakilan

Dalam implementasi menggunakan Cisco Packet Tracer, kelompok hanya memasang satu perangkat perwakilan untuk setiap LAN sesuai ketentuan tugas.

Meskipun demikian, perhitungan subnet tetap menggunakan seluruh kebutuhan host yang telah ditentukan pada UTS. Oleh karena itu, jumlah perangkat yang ditampilkan dalam simulasi tidak merepresentasikan keseluruhan kapasitas atau kebutuhan host pada jaringan sebenarnya.

Pendekatan ini digunakan untuk menyederhanakan simulasi tanpa mengubah perencanaan pengalamatan jaringan.

### 1.7 Kesimpulan Desain

Desain topologi ini dibuat untuk merepresentasikan jaringan Smart City Kota Surabaya yang menghubungkan berbagai wilayah melalui jaringan backbone dengan R-PUSAT sebagai pusat konektivitas.

Penggunaan router, switch, server, access point, serta kombinasi media kabel dan wireless disesuaikan dengan kebutuhan masing-masing jaringan. Dengan desain tersebut, jaringan diharapkan dapat mendukung komunikasi antarwilayah, akses pengguna, serta penyediaan layanan jaringan sesuai ketentuan Mid-Project Komunikasi Data dan Jaringan Komputer.

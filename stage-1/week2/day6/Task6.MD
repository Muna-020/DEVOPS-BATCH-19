#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 6

# Web Server & Reverse Proxy & Load Balancing use Nginx

+ Web server adalah perangkat keras atau perangkat lunak yang menyediakan layanan untuk menerima, mengelola, dan mengirimkan konten web kepada pengguna melalui internet. Fungsi utama web server adalah menanggapi permintaan HTTP (Hypertext Transfer Protocol) dari klien, seperti browser web, dan menyajikan halaman web atau sumber daya lainnya.

+ Reverse proxy adalah perangkat server atau perangkat lunak yang berada di antara klien dan server utama (backend server). Fungsinya adalah menerima permintaan dari klien dan meneruskannya ke server backend, kemudian mengembalikan respons dari server backend kepada klien. Sebaliknya dengan proxy biasa yang berfungsi melindungi klien dari server, reverse proxy melindungi server dari klien. Selain itu, reverse proxy dapat digunakan untuk memuat seimbang lalu lintas (load balancing), menyediakan keamanan dengan fungsi firewall dan keamanan aplikasi, serta memantau dan mengoptimalkan kinerja server backend. 

+ Load balancing adalah proses pendistribusian traffic atau lalu lintas jaringan secara efisien ke dalam sekelompok server, atau yang lebih dikenal dengan server pool atau server farm. Load balancing ini berguna agar salah satu server dari website yang mendapatkan banyak lalu lintas kunjungan tidak mengalami kelebihan beban

Tahapan ringkas dalam penggunaan Reverse Proxy dengan Nginx sebagai web server:
+ melakukan persiapan aplikasi yang akan digunakan untuk deploy menggunakan reverse proxy dan load balancing
+ mennginstall seluruh package aplikasi untuk bisa dijalankan dan PM2 untuk menjalankan aplikasi di latar belakang
+ membuat konfigurasi Reverse Proxy serta load balancing kemudian menambahkan nama domain kostum untuk bisa diakses pada web browser
+ terakhir mengakses aplikasi sesuai domain dibuat di web browser

berikut gambaran pengerjaan reverse proxy dan load balancing:

1.  pada keempat gambar ini untuk persiapan aplikasi yang akan digunakan untuk reverse proxy dan load balancing yaitu aplikasi dumbsound dengan menggunakan node.js

![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/4%20install%20nvm.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/5%20install%20npm%20.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/6%20npm%20start.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/9%20hasil%20clone%20yang%20sudah%20di%20jalankan.png?raw=true)

2. pada keempat gambar ini untuk melakukan instalasi nginx sebagai web server untuk pembuatan reverse pada aplikasi dumbsound kemudian membuat file berisi konfigurasi reverse proxy serta pada file di direktori `/etc/hosts/` untuk menggunakan domain kostum yang masih berjalan secara local.

![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/11%20cek%20status%20nginx.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/14%20configuration%20proxy%20sudah%20dibuat.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/17%20config%20pada%20local.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/reverse%20proxy/19%20reverse%20proxy%20berhasil%20dibuat.png?raw=true)

3. pada kelima gambar ini untuk implementasi load balancing agar saat terjadi banyak lalu lintas akses ke web dombsound tidak terlalu membebankan server utama yang digunakan dumbsound yang terlebih dulu membuat dua buah vm yang digunakan sebagai server load balance. kemudian, mengambil ip dari kedua vm lalu menambahkan konfigurasi di file reverse proxy untuk ip dari server load balance. terakhir, melakukan tes untuk mengetahui load balance berhasil atau tidak.

![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/load%20balancer/4%20cek%20ip.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/load%20balancer/6%20konfigurasi%20load%20balance.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/load%20balancer/10%20aplikasi%20dapat%20berjalan.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/load%20balancer/11%20test%20salah%20satu%20server%20mati.png?raw=true)
![alt text](https://github.com/sinambela99/DEVOPS-BATCH-19/blob/master/load%20balancer/12%20aplkasi%20masih%20dapat%20berjlan%20.png?raw=true)

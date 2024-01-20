#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 6

# Web Server & Reverse Proxy & Load Balancing use Nginx

+ Web server adalah perangkat keras atau perangkat lunak yang menyediakan layanan untuk menerima, mengelola, dan mengirimkan konten web kepada pengguna melalui internet. Fungsi utama web server adalah menanggapi permintaan HTTP (Hypertext Transfer Protocol) dari klien, seperti browser web, dan menyajikan halaman web atau sumber daya lainnya.

+ Reverse proxy adalah perangkat server atau perangkat lunak yang berada di antara klien dan server utama (backend server). Fungsinya adalah menerima permintaan dari klien dan meneruskannya ke server backend, kemudian mengembalikan respons dari server backend kepada klien. Sebaliknya dengan proxy biasa yang berfungsi melindungi klien dari server, reverse proxy melindungi server dari klien. Selain itu, reverse proxy dapat digunakan untuk memuat seimbang lalu lintas (load balancing), menyediakan keamanan dengan fungsi firewall dan keamanan aplikasi, serta memantau dan mengoptimalkan kinerja server backend. 

Tahapan ringkas dalam penggunaan Reverse Proxy dengan Nginx sebagai web server:
+ melakukan persiapan aplikasi yang akan digunakan untuk deploy menggunakan reverse proxy dan load balancing
+ mennginstall seluruh package aplikasi untuk bisa dijalankan dan PM2 untuk menjalankan aplikasi di latar belakang
+ membuat konfigurasi Reverse Proxy serta load balancing kemudian menambahkan nama domain kostum untuk bisa diakses pada web browser
+ terakhir mengakses aplikasi sesuai domain dibuat di web browser

berikut gambaran pengerjaan reverse proxy dan load balancing:


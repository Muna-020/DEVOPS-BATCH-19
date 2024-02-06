#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 2

# Basic Network & Linux Shell


Jaringan atau Network adalah kumpulan perangkat jaringan (network devices) dan perangkat komputer (end devices) 
yang saling terhubung melalui perantara media transmisi untuk dapat melakukan sharing data dan sumber daya.

### IP Public dan IP Private
Alamat IP (Internet Protocol) terbagi menjadi dua jenis utama, yaitu IP Publik dan IP Pribadi.

IP Publik dirancang untuk digunakan secara langsung di internet dan berfungsi sebagai identifikasi unik untuk perangkat yang terhubung ke internet.
Contoh format IP Publik untuk IPv4 adalah 203.0.113.1, sedangkan untuk IPv6 adalah 2001:0db8:85a3:0000:0000:8a2e:0370:7334. IP Publik dapat diakses 
secara langsung dari internet dan biasanya digunakan untuk menyediakan layanan publik seperti hosting situs web atau server email. 

Di sisi lain, IP Pribadi digunakan dalam jaringan lokal (LAN) atau jaringan pribadi, dan tidak dirancang untuk diakses langsung dari internet.
Contoh format IP Pribadi untuk IPv4 adalah 192.168.1.1, dan untuk IPv6 adalah fd12:3456:789a:1::1. IP Pribadi memungkinkan komunikasi antara perangkat dalam 
jaringan lokal tetapi tidak dapat diakses secara langsung dari internet. IP Pribadi biasanya digunakan di rumah atau kantor untuk mengatur perangkat di dalam jaringan lokal.

### IP Static dan IP Dynamic
Alamat IP statis adalah alamat IP yang tetap atau tidak berubah, ditetapkan secara manual pada perangkat jaringan. Dalam konteks ini, setiap perangkat memiliki alamat IP yang ditentukan 
dan tidak berubah meskipun terjadi restart atau pemutusan koneksi. IP statis sering digunakan untuk perangkat atau server yang perlu memiliki alamat yang konsisten dan dapat diakses
dengan mudah. Misalnya, server web atau router mungkin diberikan IP statis untuk memastikan ketersediaan dan aksesibilitas yang konsisten. Meskipun memberikan stabilitas, penggunaan IP
statis dapat memerlukan konfigurasi manual dan pengelolaan yang lebih intensif, terutama pada jaringan yang berkembang atau berubah.

Sebaliknya, alamat IP dinamis diberikan secara otomatis oleh server DHCP (Dynamic Host Configuration Protocol) dalam jaringan. Setiap kali perangkat terhubung ke jaringan, server DHCP memberikan alamat IP 
yang tersedia secara dinamis. Pendekatan ini memungkinkan alokasi alamat IP yang efisien dan fleksibel, terutama pada jaringan besar di mana jumlah perangkat terhubung dapat berubah-ubah. IP dinamis mempermudah 
manajemen jaringan karena tidak memerlukan konfigurasi manual pada setiap perangkat, namun, dapat menyebabkan perubahan alamat IP dari waktu ke waktu. Meskipun umumnya digunakan di lingkungan rumahan dan kantor, 
IP dinamis lebih mudah dielola dalam skenario jaringan yang memerlukan penanganan alokasi alamat yang efisien.

Linux Shell adalah antarmuka pengguna teks yang memungkinkan pengguna untuk berinteraksi dengan sistem operasi Linux melalui perintah-perintah baris perintah. 
Shell berfungsi sebagai penerjemah antara pengguna dan inti sistem operasi, menerima perintah-perintah dari pengguna dan mengeksekusinya. Salah satu keunggulan utama 
Linux Shell adalah fleksibilitasnya yang tinggi, memungkinkan pengguna untuk mengotomatiskan tugas-tugas dengan skrip perintah atau "shell scripts".

cd (change directory):
```
 melakukan perpindahan antar direktori
```
mkdir (make directory):
```
membuat suatu direktori
```
ls (list)
```
melihat daftar file atau direktori
```
cp (copy)
```
melakukan copy atau salin suatu file atau direktori
```
mv (move)
```
melakukan perpindahan suatu file atau direktori serta dapat merubah nama suatu file
```
cat (concatenate)
```
membaca, menggabungkan, dan menampilkan isi teks dari satu atau beberapa file
```
echo
```
untuk menampilkan teks atau variabel di layar. 
```

berikut gambaran penggunaan perintah pada linux shell:

![Screenshot from 2023-11-22 16-08-00](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/72d39a57-015a-432d-bdbb-f788f7ec2983)
![Screenshot from 2023-11-22 16-06-39](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b2d8895b-bd59-48e8-8c31-2c095ec9382f)
![Screenshot from 2023-11-22 16-05-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/2d7ae665-6ac0-4c81-b1ce-7dcb6e6ba438)
![Screenshot from 2023-11-22 16-00-49](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/76197bdb-6af7-49e6-a2b1-a39c7a487310)
![Screenshot from 2023-11-22 15-58-17](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/77233366-5843-44e3-8a8a-31495b10826c)
![Screenshot from 2023-11-22 15-54-48](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/0e020de0-59c2-4f6b-aaef-e78281eb9941)
![Screenshot from 2023-11-22 15-53-53](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/00a1e916-16e9-4c55-ab11-69dd83d54bbd)
![Screenshot from 2023-11-22 15-53-05](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/763c0d1b-34b9-40ac-ab1f-9e1cc07a436e)
![Screenshot from 2023-11-22 15-51-21](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5df7a954-de9d-4d57-83b1-0025d9182484)





#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 2

```
Application Backend merupakan  aplikasi Backend adalah bagian dari suatu aplikasi yang tidak terlihat oleh pengguna tetapi 
sangat penting untuk menyediakan fungsionalitas dan mendukung pengalaman pengguna. Backend mencakup server, database, 
dan logika aplikasi yang menjalankan proses di belakang layar. 
Sedangkan Deploy Application Backend adalah proses memindahkan aplikasi backend dari lingkungan pengembangan atau pengujian ke 
lingkungan produksi, sehingga dapat diakses oleh pengguna akhir. Proses ini melibatkan pemasangan atau implementasi kode aplikasi,
konfigurasi server, dan menyusun sumber daya lain yang dibutuhkan agar aplikasi dapat berjalan dengan baik secara online.

ringkasan tahapan pengerjaan untuk Deploy Application Backend:
- membuat sebuah VM di biznetGio dengan spesifikasi 2 CPU, 2 GB RAM, 60 GB STORAGE dengan nama appserver
- Penggunaan Server VM yang telah dibuat untuk membuat user baru membuat SSH-Key untuk remote dari local ke VM
- melakukan pembuatan database dengan penggunaan database mysql
- konfigurasi aplikasi backend untuk migrasi data ke database mysql di VM appserver
- serta konfigurasi API pada aplikasi frontend pada VM gateway
- konfigurasi reverse proxy dan domain pada frontend dan backend serta pembuatan certifitcate untuk SSL pada kedua domain
- mengakses seluruh frontend dan backend pada web browser dengan domain yang sudah dibuat 
- terakhir melakukan register pada aplikasi dan mengecek di database data register sudah tersimpan. 
```

#### 1. pembuatan server untuk VM di BiznetGio:

+ pada ketiga gambar ini melakukan login ke akun biznetgio untuk melakukan pembuatan VM (Virtual Machine). Dalam pembuatannya terdapat tahapan yaitu pembuatan nama server, memilih produk yang akan digunakan oleh VM yaitu SS 2.2, jenis operasi sistem yaitu ubuntu-20.04, membuat SSH-Key, terakhir pembuatan username dan password untuk VM.

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4255d17f-7895-49f2-9984-45daefb5fdca?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5f173bc3-f08d-4f0b-b7a0-a6231f16ba4e?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/af813ff7-2bf7-4364-80ad-33e0747c10df?raw=true)

#### 2. implementasi ssh config untuk koneksi antar server local dan vm:

+ Pada ketiga gambar ini untuk melakukan konfigurasi penggunaan ssh file config untuk memudahkan akses lebih cepat dan efisien ke setiap server.

![Screenshot from 2023-12-26 10-49-16](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ed9e17d7-4f57-454b-ad0b-dd9d238a9f55)
![Screenshot from 2023-12-26 10-35-35](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/83b97112-4bd8-47dc-81a6-886f04b7c516)
![Screenshot from 2023-12-26 10-35-46](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/766ed942-bf60-4f17-866d-452a87ac604c)

#### 3. penggunaan database mysql pada vm appserver1 :

+ Pada kelima gambar ini untuk penggunaan database mysql yang tahapan nya dari konfigurasi keamanan dari mysql, pembuatan user `ROOT` baru untuk mengakses dengan password, pembuatan user `ahmad` dan password untuk digunakan dalam akses ke mysql, lalu mengkonfigurasi file `/etc/mysql/mysql.conf.d/mysql.cnf` untuk merubah konfigurasi pada bagian bind-address dengan menggantinya menjadi `0.0.0.0` agar mengizinkan ip darimana saja yang dapat mengakses mysql.

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6e235856-6f74-45d3-860d-74a465aadf21?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f4aa20c8-0055-41db-be9f-bad6b15faf55?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/65209687-c9e3-4656-bce7-a36516205843?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1447e5b9-6bc4-4d55-b0fb-419236d298b4?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8231a185-0b6c-44a5-ae59-d17e34121ef1?raw=true)
![Screenshot from 2023-12-21 10-22-37](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/9aff0cfc-9f17-4c86-817e-3c034b7d8959)

#### 4. Deploy aplikasi backend serta migrasi ke database mysql dan konfigurasi api di frontend pada server gatewaynginx:

+ Pada kedelapan gambar ini untuk persiapan dalam mendeploy aplikasi backend dan frontend dengan melakukan konfigurasi pada masing-masing aplikasi dari konfigurasi file backend agar dapat migrasi data backend ke database. lalu untuk frontend melakukan konfigurasi pada file untuk memasukkan link api agar data frontend akan terkirim ke backend lalu mengirimkan nya ke database.

![Screenshot from 2023-12-21 10-41-16](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f0e2ee4b-04fb-45ed-b834-ddee216db68e)
![Screenshot from 2023-12-21 10-46-36](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/62a397ff-96ff-4e41-a0cc-28f9a7f0b88e)
![Screenshot from 2023-12-21 10-49-43](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/a6af80c4-9c03-4071-90a8-64b1b4c4742c)
![Screenshot from 2023-12-21 10-51-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/eb8bdec1-3660-48c5-803e-94a1737de2ec)
![Screenshot from 2023-12-21 10-53-49](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e3cb1a9d-fca2-4cc7-88c9-c8777be01fb7)
![Screenshot from 2023-12-21 11-02-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/55801892-ad1e-4cfb-865d-912b0ff67ff8)
![Screenshot from 2023-12-21 18-49-30](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5720b8a0-b5c3-476d-930a-f9d85fcf16eb)
![Screenshot from 2023-12-21 19-44-10](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4fbd6f40-5efb-4f8c-8f8b-1623404ce113)

#### 5. pembuatan domain pada frontend dan backend serta pembuatan certifcate untuk ssl pada domain:

+ Pada keduabelas gambar ini untuk pembuatan domain masih menggunakan dns dari cloudflare yang mana membuat dua buah domain dengan nama domain frontend `ahmad.studentdumbways.my.id` dan untuk nama domain backend `api.ahmad.studentdumbways.my.id`. kemudian membuat konfigurasi untuk reverse proxy dengan menggunakan kedua domain yang dibuat dan untuk penggunaan ssl pada domain yang digunakan yaitu cerbot yang merupakan penyedia sertifikat keamanan Web Let's Encrypt dimana Lets Encrypt ini menyediakan SSL secara gratis. Dengan adanya SSL ini kita bisa menggunakan situs kita dengan metode HTTPS atau port 443. selanjutnya setelah ssl berhasil dilakukan dan reverse proxy sudah berhasil berjalan lalu melakukan akses dengan domain yang dibuat di web browser dan mencoba melakukan register akun yang ketika register berhasil data tersebut akan terkirim ke database mysql.

![Screenshot from 2023-12-21 19-13-41](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/94c900f9-4b55-464f-b2c8-d9e55c2c3168)
![Screenshot from 2023-12-21 19-15-19](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/41577d88-9d80-4d17-9a2e-6d6deb06f4b9)
![Screenshot from 2023-12-21 19-20-31](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7e8b0ba4-17d5-45f8-ab56-48e3177d579e)
![Screenshot from 2023-12-21 19-23-47](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/893bf5d8-7d39-460c-96be-3700a0d9f9fc)
![Screenshot from 2023-12-21 19-24-40](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ec906b71-94f0-4c83-a7f9-3980b7408f75)
![Screenshot from 2023-12-21 19-27-49](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e085b91f-505b-4ea7-9153-75a6ffba5f4d)
![Screenshot from 2023-12-21 19-28-25](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1f706301-a251-4b15-8f0a-b15958325b0e)
![Screenshot from 2023-12-21 19-33-03](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/982b8ee6-375c-4356-a8ea-c9a933d95cd7)
![Screenshot from 2023-12-21 19-34-04](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e19c3ebc-467d-44d1-9ba1-559e1c5245a7)
![photo_2023-12-23_09-09-31](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1e7c5f1c-9de2-4522-9304-798709d2e6c3)
![photo_2023-12-23_09-09-37](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/75b44bc5-d4a3-42fe-b6c1-f8d1d2258a7b)
![Screenshot from 2023-12-21 19-50-19](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/70b9a713-b2fd-41a4-ae81-ed8fcbcbee31)

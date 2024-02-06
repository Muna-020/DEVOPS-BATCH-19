#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 1

# Deploy Application Frontend
```
Application Frontend merupakan sebuah aplikasi yang berfokus pada pengembangan antarmuka pengguna (UI) dan interaksi 
pengguna yang dapat dilihat dalam bentuk elemen-elemen visual agar pengguna dapat berkomunikasi dengan aplikasi.
sedangkan Deploy Application Frontend adalah langkah-langkah yang diperlukan untuk mempublikasikan atau 
meluncurkan aplikasi frontend secara online, sehingga dapat diakses dan digunakan oleh pengguna.

ringkasan tahapan pengerjaan untuk Deploy Application Frontend:
- membuat sebuah VM di biznetGio dengan spesifikasi 1 CPU, 1 GB RAM, 60 GB STORAGE
- Penggunaan Server VM yang telah dibuat untuk membuat user baru dan melakukan SSH-Key untuk mengakses secara remote ke VM
- persiapan untuk clone Repo aplikasi frontend lalu melakukan deploy menggunakan PM2 
- terakhir melakukan konfigurasi reverse proxy dan pembuatan domain melalui cloudflare
```

#### pembuatan VM di BiznetGio :

+ pada ketiga gambar ini melakukan login ke akun biznetgio untuk melakukan pembuatan VM (Virtual Machine). Dalam pembuatannya terdapat tahapan yaitu pembuatan nama server, memilih produk yang akan digunakan oleh VM yaitu XS 1.1, jenis operasi sistem yaitu ubuntu-20.04, membuat SSH-Key, terakhir pembuatan username dan password untuk VM.

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f810a4f4-8e15-41da-a22b-98c06f1319be?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/838acba0-9764-416d-a3e9-f6b6a2db38d3?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b482d525-92ac-4d67-a867-58be63253811?raw=true)

#### penggunaan server dan implementasi ssh-key:
+ pada keempat gambar ini untuk melakukan akses ke VM server yang sudah dibuat dengan menggakses menggunakan SSH-Key dengan perintah `ssh -i ssh-key_app1.pem flomun@103.150.191.16`. kemudian melakukan tambahan public key yang dari local server lalu di masukkan ke file `authorized_keys` pada VM server yang dimiliki agar memudahkan akses remote ssh ke VM server.

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/0a79923a-d092-452d-a75a-708d7be86845?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4a2a862f-601b-4ee8-bbd4-6cafda0797ad?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4d005e88-123c-46a6-bf72-49ad18c60cbb?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/a95f8bc1-1489-46f9-9c2d-21245c07de18?raw=true)

#### Clone Repository wayshub-frontend dan melakukan deploy aplikasi menggunakan PM2:
+ Pada keempat gambar ini untuk menyiapkan aplikasi frontend  yang akan di deploy dengan menggunakan Node.js dan PM2 

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/929fc530-3618-4e3b-929d-cab07264d103?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f1cbbabe-bd54-4023-96d0-0f929efd0b46?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/783f9037-5625-4078-9f21-76016d666ce0?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7ffe4588-f6bf-4c13-977b-54d9810c5fc7?raw=true)

#### konfigurasi reverse proxy serta implementasi penggunaan domain melalui cloudflare:
+ pada keenam gambar ini untuk membuat sebuah nama domain dengan menggunakan cloudflare yaitu `ahmad.studentdumbways.my.id`. kemudian membuat sebuah reverse proxy dengan menggunakan domain yang dibuat dan menambahkan konfigurasi directory include pada file nginx.conf setelah itu melakukan reload dan restart nginx. terakhir melakukan percobaan akses dengan menggunakan domain menuju aplikasi frontend yang berjalan di web browser.

![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7c0778a3-8d01-4fbe-a903-42c3ac98d9da?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/73f0ebb1-0ee8-457a-b900-f09b26591121?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/42d15a10-eff3-4259-b30d-ed835f8e893a?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/62e1d5a7-6b49-4e11-9ab6-80c63345b33e?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/d1dcb27c-dc4e-4b0e-906b-8880c8a4e817?raw=true)
![alt text](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/840e8ba9-1c4d-4ba5-8485-557e6dcb03b0?raw=true)

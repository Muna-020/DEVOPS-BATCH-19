# Monitoring
```
Monitoring server adalah proses dalam pemantaun sebuah server serta mengumpulkan data tersebut untuk mengidentifikasi potensi masalah, 
mencegah kegagalan sistem, meningkatkan kinerja, dan memastikan ketersediaan layanan.

Grafana, Prometheus, dan Node Exporter adalah alat-alat populer yang digunakan bersama-sama untuk membangun sistem monitoring

Tahapan-tahapan ringkasan dalam pengerjaan monitoring:
    - setup Container untuk membuat service Node Exporter, Prometheus, dan Grafana dan dijalankan pada setiap server yang ingin dimonitor.
    - menjaalankan Prometheus untuk menyaring metrik dari Node Exporter dan menyimpannya dalam penyimpanan time series internal.
    - Pembuatan Dashboard dengan menggunakan Grafana untuk memonitoring di seluruh server baik dari CPU, RAM, dan Penggunaan Disk
    - konfigurasi pembuatan alerting notifikasi pada seluruh server apabila terdapat masalah.
    - terakhir, melihat hasil notifikasi alert yang terkirim di discord.
```

#### 1. membuat konfigurasi reverse proxy untuk node-exporter untuk kedua server, grafana dan prometheus di server gateway  

+  pada kedua gambar ini untuk melakukan penambahan konfigurasi reverse proxy nginx pada penggunaan domain node-exporter, grafana, dan prometheus pada server gateway.

![Screenshot from 2024-01-14 14-21-01](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6345226d-123e-4aa0-bf70-0003e37002e3)
![Screenshot from 2024-01-14 14-21-41](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/fab25ece-e459-41d6-8bac-cac89c67f68f)

#### 2. melakukan setup dengan docker untuk pembuatan container node-exporter pada kedua server serta grafana dan prometheus di server gateway


+ pada ketiga gambar ini untuk penambahan docker container node-exporter, grafana, dan prometheus yang berjalan di docker compose.

![Screenshot from 2024-01-14 14-27-05](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/30e30892-e8f3-4467-9ad4-9f7a4ca52a70)
![Screenshot from 2024-01-14 14-27-32](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b5e6aa7c-ba46-4aa4-825d-e173df73b8e2)
![Screenshot from 2024-01-14 14-27-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/a4d33454-cb65-4190-8982-3e37b3f01f50)


#### 3. mengakses seluruh node-exporter, grafana, prometheus dengan domain dari reverse proxy

+ Pada keempat gambar ini untuk melakukan akses di web browser untuk node-exporter, grafana, prometheus dengan domain yang sudah digunakan sebagai reverse proxy.

![Screenshot from 2024-01-13 15-17-43](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4b0b12bf-6794-4a49-93f6-d22370744d99)
![Screenshot from 2024-01-13 15-17-47](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/499ea75a-9b5b-47ed-a222-8b659843b5dc)
![Screenshot from 2024-01-13 15-17-50](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/aecead38-722b-4947-a541-00b7e5933fe7)
![Screenshot from 2024-01-13 15-17-55](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/35ea798d-5941-47e8-8cd1-b2a51216af69)

#### 4. Membuat Dashboard monitoring menggunakan grafana

+ pada kedua gambar ini untuk pembuatan sebuah dashboard dalam melakukan monitoring pada kedua server yaitu server appserver dan gateway. terdapat beberapa hal yang di monitoring yaitu dari docker container yang berjalan pada server appserver, total persentase penggunaan cpu, jumlah cpu yang dimiliki masing-masing server, persentase penggunaan disk, persentase penggunaan RAM pada kedua server.

![Screenshot from 2024-01-15 09-29-29](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4d55af50-12ec-4e81-9f72-a0ef72eb04dd)
![Screenshot from 2024-01-15 09-30-52](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/30bf4b71-37fc-4634-a7e8-3cfe7e215856)

#### 5. Notifikasi Alerting di discord adanya penggunaan CPU dan RAM berlebihan pada Server App-server  

+ Pada kedua gambar ini untuk menampilkan sebuah bentuk notifikasi yang diimplementasikan pada grafana untuk pesan peringatan atau `alerting` pada penggunaan cpu dan RAM yang berlebihan pada kedua server.

![Screenshot from 2024-01-13 15-25-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/919519d3-f293-4854-9792-b0d2c6528010)
![Screenshot from 2024-01-13 15-25-41](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/cd34ee8b-9acc-4b8d-88e2-62efb1e1cc2c)


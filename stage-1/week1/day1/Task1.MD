#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 1

# Fundamental DevOps
```
DevOps adalah suatu pendekatan dalam pengembangan perangkat lunak yang mengintegrasikan tim pengembangan (developers) dan operasi (operations) 
dengan tujuan meningkatkan kolaborasi dan efisiensi dalam siklus pengembangan, pengujian, dan implementasi perangkat lunak. 
Istilah "DevOps" sendiri berasal dari penggabungan kata "development" (pengembangan) dan "operations" (operasi).
Tujuan utama dari DevOps adalah untuk menciptakan proses pengembangan perangkat lunak yang lebih cepat, lebih andal, dan lebih terukur.
Pekerjaan seorang DevOps merupakan pekerjaan terus-menerus dengan alur dan fungsi sebagai berikut :
- Perencanaan (Planning):
  Tim pengembangan dan operasi terlibat dalam pembuatan dan perumusan rencana pengembangan yang mencakup kebutuhan pengguna, 
  prioritas fitur, dan tenggat waktu proyek.
- Pengembangan (Development):
  Pengembang menulis kode sumber berdasarkan kebutuhan dan spesifikasi. Kode ini dapat diunggah ke sistem kontrol versi.
- Pengujian (Testing):
  Tim QA (Quality Assurance) dapat melakukan pengujian unit, integrasi, dan fungsionalitas perangkat lunak. 
  Otomatisasi pengujian juga dapat digunakan untuk mempercepat proses ini.
- Integrasi (Integration):
  Proses integrasi berlangsung secara terus-menerus, menggabungkan perubahan kode dari pengembang ke dalam lingkungan pengujian
  untuk memastikan bahwa fitur baru atau perbaikan tidak merusak fungsionalitas yang ada.
- Penerapan (Deployment):
  Penerapan dapat dilakukan secara otomatis atau manual, tergantung pada kebijakan organisasi. 
  Pemantauan dan pemecahan masalah sepanjang proses ini sangat penting.
- Operasi (Operation):
  Tim operasi bertanggung jawab untuk memantau kinerja sistem, menanggapi masalah, dan mengelola konfigurasi infrastruktur.
  Pembaruan dan perbaikan keamanan juga dapat dilakukan di sini.
- Pemantauan (Monitoring) dan Perbaikan Masalah (Incident Response):
  Pemantauan kontinu dilakukan untuk mendeteksi masalah potensial. Tim respons insiden merespons cepat terhadap gangguan dan masalah keamanan.
```
```
manfaat dari DevOps adalah sebagai berikut:
  1. Penyampaian Cepat: Implementasi perubahan lebih cepat.
  2. Peningkatan Kualitas: Pengujian otomatis meningkatkan kualitas.
  3. Kolaborasi Tim: Integrasi tim pengembangan dan operasi.
  4. Efisiensi Operasional: Otomatisasi mengurangi beban kerja operasional.
  5. Ketersediaan dan Kinerja: Pemantauan kontinu dan pemecahan masalah cepat.
  6. Skalabilitas: Mudah menyesuaikan sumber daya sesuai kebutuhan.
  7. Keamanan: Praktik keamanan terintegrasi dalam siklus hidup.
  8. Umpan Balik Berkelanjutan: Peningkatan terus-menerus dari pemantauan dan pengujian.
  9. Time-to-Market Cepat: Peningkatan kecepatan pengiriman produk atau fitur.
  10. Pengurangan Biaya dan Risiko: Otomatisasi mengurangi biaya operasional dan risiko.
```
```
Adapun ringkasan tahap-tahap dalam pembuatan server ubuntu:
 - menginstall sebuah file ISO untuk ubuntu server dan software VMWare untuk jalankan VM Ubuntu.
 - menjalankan VMWare untuk membuat VM baru
 - membuat konfigurasi server ubuntu dari setup network, update dan upgrade, konfigurasi proxy, mengatur penyimpanan dan memory, dan membuat user dan password
```
berikut gambaran hasil pembuatan ubuntu server:
1. melakukan konfigurasi pada bagian Network untuk membuat IP Static lalu mengisi subnet dengan IP utama dengan prefix /24, kemudian pada bagian addres diisi dengan IP yang akan digunakan, dan di bagian gateway diisi dengan IP yang menjadi titik akses untuk Network lokal dan Network Eksternal.  

![Screenshot from 2023-11-22 08-52-38](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7ce41924-def4-4f2a-b1c3-34a3e64c47d7)
![Screenshot from 2023-11-22 08-53-02](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4dc53020-2f57-440a-a180-b21a6c6247bc)
![Screenshot from 2023-11-22 08-52-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/d25e86af-73a6-4300-955a-1b4e37dd0a29)

2. melakukan konfigurasi update pada ubuntu untuk package yang diperlukan

![Screenshot from 2023-11-22 08-55-04](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f1b9b39c-1d76-4295-badb-2c25dd3edc21)

3. konfigurasi pada bagian storage dengan mengkostumnya dalam menjadi tiga partisi yaitu partisi pertama untuk BIOS 1MB, partisi kedua untuk storage cadangan 2GB, dan partisi ketiga untuk ROOT atau storage utama 7,9GB.

![Screenshot from 2023-11-22 08-56-42](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/807f198e-62ab-4ef3-9cf7-10e8e019d08f)
![Screenshot from 2023-11-22 08-57-15](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6239ddfa-53b4-4b07-b584-316358a03bcf)
![Screenshot from 2023-11-22 08-57-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/beeb5e9b-d534-486e-8e15-7de7cce28883)
![Screenshot from 2023-11-22 08-58-05](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1a50ed07-7a65-4236-a3fe-e2f22b587f62)
![Screenshot from 2023-11-22 08-59-50](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/092591a6-5620-4837-bb07-ff0c70967b34)
![Screenshot from 2023-11-22 09-00-20](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/9f553298-c172-49a1-85ce-2c8040431615)

4.  konfigurasi untuk profile yang diisi dari nama, nama server, nama pengguna, dan password sesuai yang diinginkan.

![Screenshot from 2023-11-22 09-04-39](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/06396d60-893e-477a-b809-e0e56d92b23c)
![Screenshot from 2023-11-22 09-16-38](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/65ab0a2e-f6e7-4f39-bcc3-863ecac3bd4c)

5. melakukan pilihan apakah ingin menginstall ssh untuk melakukan remote pada ubuntu server atau tidak yang mana pada bagian ini memilih untuk menginstall ssh server

![Screenshot from 2023-11-22 09-18-18](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/0e4d86f2-d6dd-4548-92a4-da94f82926ac)
![Screenshot from 2023-11-22 14-08-23](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8ab2c7c3-be87-4923-9df1-0fc80b58e540)
![Screenshot from 2023-11-22 14-14-04](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/bdb0d81e-bfbf-4477-bccd-b67a02f1d24b)
![Screenshot from 2023-11-22 14-20-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/40fcd6d6-083d-43bb-8384-5daee2ceef21)
![Screenshot from 2023-11-22 14-20-55](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/d806fe5a-ecc2-432a-801d-010bfa06c4dc)
![Screenshot from 2023-11-22 14-21-14](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/60753677-49f2-415b-b8f8-962787cac044)


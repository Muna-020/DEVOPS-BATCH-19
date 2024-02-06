#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Task 4

## Text Editor & Text Manipulation & Implementation Firewall use UFW

+ Teks editor adalah program yang digunakan untuk membuat, mengedit, dan mengelola berkas teks. Beberapa teks editor yang umum digunakan di lingkungan Unix/Linux termasuk Vim, Emacs, dan  Nano. 

+ Teks manipulasi merujuk pada proses memanipulasi atau mengubah teks dalam berkas. Dalam konteks Unix/Linux, serangkaian perintah dan alat seperti sed (stream editor), echo, dan cat 

+ Firewall adalah sistem keamanan yang dirancang untuk melindungi jaringan komputer dari akses yang tidak sah dan serangan berbahaya. Firewall dapat berupa perangkat keras atau perangkat   lunak yang memantau, mengontrol, dan memfilter lalu lintas jaringan berdasarkan aturan keamanan tertentu. UFW adalah antarmuka pengguna untuk iptables, sistem firewall bawaan di Linux.   UFW dirancang untuk membuat pengaturan firewall menjadi lebih mudah dan ramah pengguna, terutama bagi pengguna yang mungkin tidak memiliki pengalaman mendalam dengan konfigurasi          iptables. Dengan UFW, pengguna dapat dengan mudah menentukan aturan firewall untuk mengizinkan atau memblokir lalu lintas, engamankan sistem, dan mengelola akses jaringan.

Berikut penggunaan teks editor, manipulasi teks dan implementasi firewall ufw:

1. pada ketiga gambar ini untuk membuka file dengan file1 menggunakan perintah `nano file1` kemudian mengisi sebuah data atau kata dalam file tersebut setelah itu melakukan save untuk menyimpan data atau kata tersebut.

![Screenshot from 2023-11-28 08-25-54](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/25bb3c97-d7d9-4d21-9a49-d2e256d9e215)
![Screenshot from 2023-11-28 08-26-48](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/802f3e26-824b-452c-aba6-434bed9ae9f2)
![Screenshot from 2023-11-28 08-26-59](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/70d674f0-7f0c-40af-86ed-5aa98d48dca8)

2. pada kedua gambar ini untuk melakukan sebuah copy kata pada nano yaitu terlebih dahulu melakukan block set dengan `alt-a` pada kata yang akan di copy lalu untuk paste kata dengan `alt-6`.

![Screenshot from 2023-11-28 08-29-12](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/93a3afe1-edb7-4fdf-a023-f5b350d9e851)
![Screenshot from 2023-11-28 08-30-33](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7e85e33d-0261-4a42-9e4d-46c0a8db1255)

3. pada ketiga gambar ini untuk mencari sebuah kata menggunakan nano dengan `ctrl-w` kemudian akan tampil sebuah inputan untuk mencari kata yang diinginkan berdasarkan regular expression 
dengan `alt-r` lalu akan terlihat dengan blok warna kuning kata yang telah dicari.

![Screenshot from 2023-11-28 08-34-31](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7b5a2ab0-6c86-4eb8-b237-e0d58888c188)
![Screenshot from 2023-11-28 08-36-40](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ab34d4ac-490e-440c-820e-e93d93e5a55c)
![Screenshot from 2023-11-28 08-36-44](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/860c9237-28df-452f-a3fd-8996d9bee19a)


4. pada gambar ini untuk penggunaan perintah `cat >> file2` agar dapat menambahkan sebuah kata atau kalimat pada file2

![Screenshot from 2023-11-28 09-12-24](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6d407b7d-015b-4a41-9530-7c2608deb38f)

5 perintah pada gambar ini untuk melakukan manipulasi data dengan merubah dari suatu file dengan perintah `sed -i 's/ini/itu/g' file3` dari perintah itu melakukan pencarian dari kata 's/' kemudian mencari kata 'ini' untuk diubah menjadi 'itu' seluruh kata 'ini'.

![Screenshot from 2023-11-28 09-15-20](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ecbff695-7089-43e3-9c8d-19d2e3077d90)

6. pada gambar ini untuk mencari dan menghitung jumlah kata `file3` pada sebuah file yaitu file3

![Screenshot from 2023-11-28 12-39-00](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/bb9cac12-52ce-4c2e-b88c-f3fa01fbd16b)


7. pada ketiga gambar ini untuk mengimplementasikan sebuah firewall bawaan dari ubuntu yaitu ufw yang dalam pengguanaan ufw tersebut untuk memberi keamanan pada suatu aplikasi atau server dalam mengaksesnya menggunakan port.

![Screenshot from 2023-11-28 13-17-54](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/cfa2bd1e-59d9-47c2-8767-8440061e2bc1)
![Screenshot from 2023-11-28 13-26-43](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b24afdd1-89be-4211-9b25-3ad473c49b97)
![Screenshot from 2023-11-28 13-28-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/82bfcf6d-497e-4214-8ded-dabba45faaf5)



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

2. 

![Screenshot from 2023-11-28 08-29-12](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/93a3afe1-edb7-4fdf-a023-f5b350d9e851)
![Screenshot from 2023-11-28 08-30-33](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7e85e33d-0261-4a42-9e4d-46c0a8db1255)
![Screenshot from 2023-11-28 08-31-12](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/d142d866-0e4f-41aa-bdad-6512bb9bb500)
![Screenshot from 2023-11-28 08-31-30](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6e9a4f09-d7ab-480e-9405-34cf8e62fba3)
![Screenshot from 2023-11-28 08-33-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/0b0de231-1d0e-438f-a6e4-fd38ad77dce4)
![Screenshot from 2023-11-28 08-33-50](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ddf13315-b1df-412e-a01f-7f432ecd9ead)
![Screenshot from 2023-11-28 08-34-31](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7b5a2ab0-6c86-4eb8-b237-e0d58888c188)
![Screenshot from 2023-11-28 08-36-40](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ab34d4ac-490e-440c-820e-e93d93e5a55c)
![Screenshot from 2023-11-28 08-36-44](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/860c9237-28df-452f-a3fd-8996d9bee19a)
![Screenshot from 2023-11-28 08-36-56](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5fc0f5f0-2001-46b1-92d9-43fbb4059e7a)
![Screenshot from 2023-11-28 08-40-05](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/efec82c7-9a1f-458b-84b2-8057af2d6ec9)
![Screenshot from 2023-11-28 08-40-18](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7ebdbc39-c36c-43a8-b4cd-51501b3d4621)
![Screenshot from 2023-11-28 08-40-27](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/03c48086-488f-4bf5-b1d0-0d61266a6583)
![Screenshot from 2023-11-28 08-42-10](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/072b038b-f4a6-4037-adfd-f0c10631b8de)
![Screenshot from 2023-11-28 08-42-19](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e760c62a-7b77-4efb-9538-33ffdf17f497)
![Screenshot from 2023-11-28 08-42-25](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ba04e759-8e16-4b68-a1b4-d5d098f10f68)
![Screenshot from 2023-11-28 08-42-36](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/39277576-095f-4295-bc35-486eb1a4679b)
![Screenshot from 2023-11-28 08-45-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/88cb1506-98c3-4371-a8f3-c2e4e4294f8f)
![Screenshot from 2023-11-28 08-45-35](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6cd51a63-4674-486e-bf00-718765350fcf)
![Screenshot from 2023-11-28 08-45-46](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/25ce388a-b076-444b-b304-4ce1d934395f)
![Screenshot from 2023-11-28 08-45-58](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7721ced1-a940-4ab7-a242-b994ecee44d4)
![Screenshot from 2023-11-28 09-12-24](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6d407b7d-015b-4a41-9530-7c2608deb38f)
![Screenshot from 2023-11-28 09-13-25](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4637aff9-7065-4208-8061-a3ec992ef8f7)
![Screenshot from 2023-11-28 09-15-10](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5097b2d2-c64c-4a4e-874f-908b745984ae)
![Screenshot from 2023-11-28 09-15-20](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ecbff695-7089-43e3-9c8d-19d2e3077d90)
![Screenshot from 2023-11-28 09-25-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/562f571f-ebc2-4c88-bc3e-dd23c169096f)
![Screenshot from 2023-11-28 12-39-00](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/bb9cac12-52ce-4c2e-b88c-f3fa01fbd16b)
![Screenshot from 2023-11-28 12-43-24](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/407b0479-eab7-4596-a807-df41aaf14b35)
![Screenshot from 2023-11-28 12-43-27](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f00e5f28-4e94-402d-a3f6-de43703df17d)
![Screenshot from 2023-11-28 12-49-03](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/d856d17c-0300-495d-944c-cc7ab70fd07c)
![Screenshot from 2023-11-28 12-54-34](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/44486747-55bc-4c52-9bc5-11bb80039c9c)
![Screenshot from 2023-11-28 13-07-47](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/712caca4-05ff-4379-ab69-993d3350c091)
![Screenshot from 2023-11-28 13-08-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/3eb73502-a7c0-44e0-b86c-a5fd98c0d433)
![Screenshot from 2023-11-28 13-09-50](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b5b7c948-19ee-4e73-86fd-a3300bce0d5f)
![Screenshot from 2023-11-28 13-17-54](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/cfa2bd1e-59d9-47c2-8767-8440061e2bc1)
![Screenshot from 2023-11-28 13-26-43](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b24afdd1-89be-4211-9b25-3ad473c49b97)
![Screenshot from 2023-11-28 13-28-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/82bfcf6d-497e-4214-8ded-dabba45faaf5)



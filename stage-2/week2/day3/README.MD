# Docker

```
Docker adalah platform perangkat lunak yang memungkinkan developer untuk mengemas aplikasi beserta
dependensinya ke dalam kontainer yang dapat dijalankan di berbagai lingkungan. Docker Container mencakup 
semua yang diperlukan untuk menjalankan aplikasi, termasuk kode, runtime, sistem perpustakaan, dan pengaturan.
Docker membantu dalam memastikan konsistensi lingkungan dan memudahkan pengiriman aplikasi di berbagai
lingkungan, seperti pengembangan lokal, uji, dan produksi.

ringkasan tahapan pengerjaan untuk Docker:
- melakukan rebuild pada VM menjadi OS ubuntu 22 serta konfigurasi SSH-Password Only
- instalasi Docker menggunakan Bash Script 
- mempersiapkan seluruh aplikasi untuk melakukan deploy menggunakan Docker Compose
- Setup Docker Container agar seluruh Aplikasi dapat deploy dengan Docker Compose  
- menjalankan Docker Compose lalu mengakses aplikasi di web browser dengan domain yang sudah dibuat
- terakhir melakukan pull image untuk menyimpan image Docker seluruh aplikasi ke Docker registry. 
```

## Rebuild VM menggunakan OS ubuntu 22 dan menerapkan ssh Password only :

+ Pada keenam gambar ini untuk melakukan pembuatan ulang atau rebuild VM server agar VM server dapat digunakan ulang tanpa terdapat  data yang tersisa didalam VM Server tersebut. lalu melakukan konfigurasi file ssh untuk penggunaan autentikasi ssh dengan password `PasswordAuthentication yes`.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/57e1444a-0e61-4077-9570-293c86c76740)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/3dc12490-51dc-4984-9520-970dff82b151)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/99c5705e-27de-4deb-9385-0be86d1ae5b8)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/7b822ea1-8def-4645-8c9a-c86b539f604c)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/291856ec-a7ff-4721-912e-b7eccb03942a)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/f99eebf3-7673-4380-8569-b38a41fb0316)

## Bash Script Instalasi Docker

+ Pada gambar ini untuk penggunaan sebuah Bash script untuk melakukan perintah instalasi Docker secara automasi tanpa melakukan perintah satu persatu.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/07e4f8c3-2328-4b58-8f8a-716cf8ca6b97)

## Deploy aplikasi Web Server, Frontend, Backend, serta Database on top `docker compose` :

+ Pada kesebelas gambar ini untuk pembuatan docker container yang akan menjalankan Aplikasi Frontend dan Backend serta Database mysql yang berjalan pada docker compose dengan terlebih dahulu melakukan clone repository dari github baik frontend dan backend serta konfigurasi frontend untuk api dan backend untuk persiapan migrasi data ke database mysql untuk kedua aplikasi. lalu melakukan pembuatan Dockerized atau persiapan buat image docker dengan nama `Dockerfile` pada frontend dan backend. kemudian membuat file `docker-compose.yaml` yang berisi konfigurasi untuk seluruh aplikasi dan database yang berjalan pada docker compose.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/c82ebf81-6699-434d-9253-b913018910a2)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/94d7767d-9f76-4a6c-83df-268c951c0829)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/64b87ce3-d554-4dd5-8579-b99e095ce651)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/6712fe91-9e77-416a-879f-9d52ca385e99)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/664d7db2-1f98-46db-ab12-37aa1d549347)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/a2828c52-473e-4f8a-b793-8cb4b1d62057)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/574edb3f-5764-43b2-93c8-7b32b8f21db1)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/186f4c0e-3110-444e-99c5-549a8a47f80f)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/e400d68b-f02c-4a02-ad32-6749ed37fe0a)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/4710bda2-8efe-4477-91ec-b3a949ebe6d0)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/a4a1d738-2d06-4d49-b10f-33efd5d5a1ac)


![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/817926d8-b6ce-4984-9e64-025ec01505ea)

## Pembuatan SSL Cerbot dan Domain dengan Cloudflare untuk kedua Aplikasi on top 'docker compose' :

+ Pada kelimabelas gambar ini untuk pembuatan SSL menggunakan cerbot dengan menggunakan domain yang dibuat pada Cloudflare lalu setelah mendapatkan sertifikat dari cerbot menambahkan pada konfigurasi docker compose untuk mengkaitkan volume penyimpanan dari cerbot yang ada di vm server ke dalam docker container nginx yang akan berjalan sebagai reverse proxy agar bisa menggunakan sertifikat pada aplikasi. setelah itu menjalankan seluruh service dari docker container yang dibuat lalu mengakses di web browser untuk aplikasi frontend dan backend. terakhir mencoba melakukan register yang saat register sukses maka data akan terkirim ke database mysql. terakhir melakukan push image seluruh image dari docker ke docker hub registry yang sudah dibuatkan akun.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/99092f44-b5ed-4158-9114-d0565602cccc)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/fb4492a2-f6e5-4ac3-a921-29281e859b3b)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/1de6eada-0db3-4e87-addd-9825df30ab79)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/ed091704-3740-462f-935c-d918c9e6b3f7)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/466876a2-ee0e-47f6-aaf2-8e5f143506e1)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/eea92ae4-f0d8-4db4-a0cb-f55ae096ab5f)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/798286dd-dcc4-4d70-b1a4-8d4a502b7efb)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/ed1fa23f-3e0a-412f-8b4b-5b90a3abf283)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/b56b9ef4-6350-4cbe-8644-9f44c2549c40)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/953629c3-2e53-4408-8c3f-8263b279c1cb)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/bfbeb4d1-37d7-4c09-a452-8cf073868b81)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/e0eaf4ea-4ece-4d90-bfb2-fd082bbf4667)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/a341fc79-25cc-44bc-af5f-46efdb7c3a09)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/7a4cce2e-872d-4f75-8fc0-675af026a46c)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/1b60f125-bb9a-48e3-85bc-00569f773045)



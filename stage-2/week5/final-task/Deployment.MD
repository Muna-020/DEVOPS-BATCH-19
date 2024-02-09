## 4. Deployment
   
+ Pada tahap ini melakukan persiapan dalam mendeploy aplikasi di masing-masing direktori frontend dan backend, terlebih dahulu membuat Dockerfile untuk Dockerized dalam membuat image aplikasi frontend dan backend. 
+ Setelah itu melakukan penambahan script untuk database postgresql serta aplikasi frontend dan backend agar berjalan di docker pada file docker compose.
+ Selanjutnya, membuat file .env yang berisi variabel dalam persiapan membuat database postgresql dan kedua aplikasi.
+ Menjalankan service database untuk melakukan persiapan migrasi data dari backend ke database.
+ Membuat sebuah image pada frontend dan backend “docker build -t flomad0411/dumbmerch-”fe/be”:1.0" 
+ Menjalankan seluruh services dari docker lalu melakukan push image ke docker hub
+ Berikut gambaran tahap pengerjaan Deployment:
![dcfilebe](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/eb40bd34-61ff-44d0-a9e7-44bfe50b2762)
![dcfilefe](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/683e6145-24e8-4b70-9bb1-fa56042a971b)
![Screenshot from 2024-01-29 05-27-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6ae2b24f-b657-4fd6-99df-c369956c42d7)
![plusapp](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7b9047a3-ab97-4399-ae76-397019cb4225)
![Screenshot from 2024-01-30 13-12-18](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ba717b24-12dd-4606-8757-36adbb73c6c9)
![Screenshot from 2024-01-28 19-45-14](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4a8ca559-f2bc-4b3e-90d2-7f65e415627e)

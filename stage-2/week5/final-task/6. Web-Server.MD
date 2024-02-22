## 6.  Web Server
   
+ Di tahap ini, melakukan konfigurasi serta penggunaan SSL pada file reverse proxy untuk bisa mengakses kedua aplikasi dengan domain yang aman 
+ Menambahkan dua buah script pada docker compose yaitu service nginx untuk load balancing  
+ Melakukan penambahan DNS pada cloudflare untuk domain seluruh aplikasi.
+ Menjalankan services webserver untuk nginx yang berjalan di docker compose .
+ Melakukan testing akses serta register akun aplikasi frontend dan backend dumbmerch.
+ lalu mengecek pada database postgresql untuk melihat hasil register yang berhasil dibuat.
+ Kemudian membuat sebuah bash script untuk melakukan pembaruan certificate secara automasi
+ Berikut gambaran tahap pengerjaan Monitoring:
![nginxfix](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/fa0cb142-1e6a-40f6-b6d6-c770cc36ed64)
![lbdc](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/767b4857-2f43-43b5-8f73-ba8350612c30)
![conf-fe](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/0cfdac44-83a4-4023-b86e-7141b17ee9b4)
![lb-be](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8f48cab0-704d-4c71-906f-be2d9821a985)
![Screenshot from 2024-01-28 18-06-49](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/a5fd8256-d139-42ff-b9b5-91aef18a69b2)
![Screenshot from 2024-01-28 18-06-45](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6fa44a0d-9829-4e82-9114-22358a8f24af)
![Screenshot from 2024-01-25 02-09-38](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/090ec199-9e71-447b-8024-655b6d0ffd96)
![Screenshot from 2024-01-24 09-08-53](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/18f45e51-b67a-40e9-b12a-b2d3c624ec2e)
![Screenshot from 2024-01-24 09-05-43](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/227bdeb7-0557-484b-82bd-8b78fb234336)
![Screenshot from 2024-01-24 09-07-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/15cbcfd3-d9df-4225-a0f6-01874c0c8265)
![Screenshot from 2024-01-24 09-08-31](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ddadb69b-ac7e-419a-9747-9a426e8b4dd0)
![Screenshot from 2024-01-24 09-09-02](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f510acb2-ffa6-45d7-a076-6b859f14f1b8)
![Screenshot from 2024-01-24 09-03-35](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f23c69d8-2d6e-433f-be29-a86aff7adcb3)
![renew](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/156d7795-4e62-481c-b05f-f5ebfe127d37)

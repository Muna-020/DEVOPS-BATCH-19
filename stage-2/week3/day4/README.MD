# Jenkins


```
Jenkins adalah alat otomatisasi open-source yang digunakan untuk memfasilitasi proses pengembangan perangkat lunak. 
Jenkins membantu dalam membangun, menguji, dan mendeploy perangkat lunak secara otomatis. Dengan menggunakan Jenkins,
tim pengembang dapat mengotomatiskan berbagai tugas, mengurangi human-error, dan mempercepat siklus pengembangan perangkat lunak.

ringkasan tahapan pengerjaan untuk Jenkins:
- melakukan rebuild pada VM menjadi OS ubuntu 22 serta konfigurasi SSH-Password Only
- pembuatan service jenkins dan nginx dengan reverse proxy dengan menggunakan docker
- membuat sebuah Jenkinsfile untuk pembuatan script agar dapat melakukan CI/CD 
- konfigurasi di jenkins untuk menjalankan CI/CD dengan metode Pipeline dengan SCM
- melihat hasil CI/CD yang sudah dijalankan sudah berhasil pada notifikasi di discord
- membuat sebuah auto trigger pada saat membuat perubahan pada file aplikasi di github repo
- terakhir, CI/CD telah berjalan secara otomatis ketika terdapat perubahan pada file di repo.
```

# Pembuatan Jenkins dan Nginx untuk reverse proxy on top Docker :

+ Pada keempat gambar ini untuk pembuatan sebuah docker container untuk bisa menggunakan jenkins yang berjalan di docker compose, setelah menjalankan jenkins serta melakukan konfigurasi di jenkins untuk persiapan cicd kemudian membuat sebuah file dengan nama `Jenkinsfile` yang berisi seluruh script untuk melakukan cicd pada aplikasi yang akan di deploy. pada script cicd tersebut terdapat tahapan yang dilakukan yaitu melakukan pull seluruh repository pada frontend dan backend, kemudian membuat image docker untuk kedua aplikasi, melakukan testing pada aplikasi, setelah itu melakukan deploy setelah aplikasi berhasil testing dan aman, terakhir melakukan push image ke docker hub dan setelah cicd selesai maka sebuah notifikasi akan diberikan di discord. 

![photo_6107268411026423830_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/4e0136ea-4f26-41b0-b8b3-27d88efbe1cf)

![photo_6107268411026423923_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/34e5ce89-6a2e-49b2-881d-4882585197d5)

![photo_6107268411026423924_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/e4bc4a61-3443-4d87-aa28-88e915707592)

![photo_6107268411026423925_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/40daca90-5cc1-4950-a4a3-545e363404c4)


# Penggunanan metode Pipeline with SCM dalam menjalankan CI/CD

+ Pada ketujuh gambar ini untuk memulai dalam menjalan cicd dengan jenkins yang mana menggunakan metode SCM `Source Code Management` yaitu metode menggunakan sebuah Jenkinsfile yang tersimpan pada github yang akan mengambil file tersebut untuk melakukan cicd. setelah cicd berjalan dan berhasil dilakukan akan terdapat notifikasi pada discord bahwa cicd berhasil.

![photo_6107268411026423920_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/e918004a-bf33-4122-bdbb-0d4397ebb3c9)

![photo_6107268411026423921_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/d690db03-ffcf-4c76-9e2c-5f684fcf6e46)

![photo_6107268411026423916_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/f91ba2c1-1643-427f-9826-c93c0eb9279c)

![Screenshot from 2024-01-07 10-44-35](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/74352384/d7220bcf-a818-46f4-86e7-81ead4b043af)

![photo_6107268411026423922_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/ba0ab13b-80f8-4461-9a61-5c5f194b2787)

![photo_6107268411026423917_x](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/80da7dab-612c-4210-b9a6-b4b72c3a2c30)

![photo_6107268411026423918_y](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/9d67588e-59d6-48f9-8fef-68aa136c81c1)








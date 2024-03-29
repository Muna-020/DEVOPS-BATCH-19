# GitlabCI


```
GitLab CI (Continuous Integration) adalah bagian dari platform GitLab yang menyediakan layanan otomatisasi CI/CD terintegrasi
langsung ke dalam sistem manajemen repositori GitLab. GitLab CI memungkinkan tim pengembang untuk mengotomatiskan proses pengujian,
pembangunan, dan penyebaran perangkat lunak secara terus-menerus.

ringkasan tahapan pengerjaan untuk Gitlab CI:
- melakukan pembuatan akun pada GItlab
- menyimpan publickey ke gitlab untuk koneksikan gitlba dengan server local
- membuat sebuah repository untuk menyimpan seluruh aplikasi frontend and backend
- konfigurasi di Gitlab untuk melakukan koneksi agar membuat notifikasi discord 
- membuat file .gitlab-ci.yml yang berisi script untuk menjalankan CI/CD 
- terakhir, ketika CI/CD berhasil dilakukan akan terlihat pada notifikasi discord CI/CD berhasil
```

# Pembuatan akun Gitlab CI dan melakukan Setup ssh key untuk Gitlab CI :

+ Pada keempat gambar ini untuk pembuatan sebuah akun Gitlab CI untuk persiapan dalam melakukan CICD menggunak Gitlab CI serta menambahkan sebuah SSH-Key untuk bisa melakukan push repository dari VM server ke repository gitlab CI.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/a36814be-40c6-4ef2-b4f8-7028085de3fb)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/71738897-c288-443b-83c4-916590dcf5da)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/318c4427-f901-4526-b1b4-721ac5bc9710)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/87039370-4e74-4494-8eca-f8567b3f0efc)


# Pembuatan Repository untuk menyimpan data Aplikasi Backend dan Frontend di gitlab 

+ Pada kedelapan gambar ini untuk membuat sebuah repository  dari seluruh aplikasi yang akan digunakan dalam CICD.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/0c1f5089-54ea-4015-b4bb-9191f032871e)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/f573ff26-3097-4991-a9d6-33ef2730d7d1)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/0551cf7b-99ce-4478-bf57-df8e22089fc1)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/52391615-bead-4eb2-bc06-d0cda32a3faa)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/ac84d8e1-dc37-4f0e-a32a-8d4c8822aaa0)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/98a7cbc2-c382-4470-a0c3-f91f92b4d56e)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/d4910475-1418-43c2-8968-798afdb3abe5)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/58b66d30-380e-4d0c-832a-950bb0b3881b)


# Pembuatan file .gitlab-ci.yml dalam melakukan CI/CD pada aplikasi dumbflix untuk Backend dan Frontend

+ Pada kesembilan gambar ini untuk pembuatan sebuah file untuk melakukan CICD di Gitlab CI yaitu `.gitlab-ci.yml` yang berisi script tahapan CICD yaitu melakukan pull seluruh repository pada frontend dan backend, kemudian membuat image docker untuk kedua aplikasi, melakukan testing pada aplikasi, setelah itu melakukan deploy setelah aplikasi berhasil testing dan aman, terakhir melakukan push image ke docker hub. dalam melakukan CICD di Gitlab CI terdapat sebuah fitur untuk melakukan editor pada script CICD yang mana ketika selesai membuat perubahan pada script maka akan secara otomatis CICD berjalan di Gitlab CI.

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/c07dfbe0-75f5-45e6-a49b-53504ca13aa7)

![Screenshot (28)](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/7b14feec-46f2-4717-85eb-760db46d2032)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/dcb6cde1-8440-4879-a876-71595e469b1f)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/0e79e1c9-4169-497f-88df-62b38e24e838)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/5891accf-a8bb-4094-a372-98daef9536f6)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/3b5b3de1-1aed-49ff-ad01-86dcf0b38ff6)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/fb708fd9-661b-46b4-9b03-a476dd26766a)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/207231af-c7a4-4973-b481-f77e50ec6ab0)

![image](https://github.com/irwanpanai/devops19-dumbways-irwanpanai/assets/89429810/d8cb0928-0808-4499-8bd0-c3d7cbacaa2b)









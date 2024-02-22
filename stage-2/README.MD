# STAGE 2 DEVOPS BATCH 19
## [WEEK 1](https://github.com/Muna-020/DEVOPS-BATCH-19/tree/master/stage-2/week1)
### [1. Deploy Application Frontend](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week1/day1/Task1.MD)
+ membuat sebuah VM di biznetGio dengan spesifikasi 1 CPU, 1 GB RAM, 60 GB STORAGE
+ Penggunaan Server VM yang telah dibuat untuk membuat user baru dan melakukan SSH-Key untuk mengakses secara remote ke VM
+ persiapan untuk clone Repo aplikasi frontend lalu melakukan deploy menggunakan PM2 
+ terakhir melakukan konfigurasi reverse proxy dan pembuatan domain melalui cloudflare

### [2. Deploy Application Backend](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week1/day2/Task2.MD)
- membuat sebuah VM di biznetGio dengan spesifikasi 2 CPU, 2 GB RAM, 60 GB STORAGE dengan nama appserver
- Penggunaan Server VM yang telah dibuat untuk membuat user baru membuat SSH-Key untuk remote dari local ke VM
- melakukan pembuatan database dengan penggunaan database mysql
- konfigurasi aplikasi backend untuk migrasi data ke database mysql di VM appserver
- serta konfigurasi API pada aplikasi frontend pada VM gateway
- konfigurasi reverse proxy dan domain pada frontend dan backend serta pembuatan certifitcate untuk SSL pada kedua domain
- mengakses seluruh frontend dan backend pada web browser dengan domain yang sudah dibuat 
- terakhir melakukan register pada aplikasi dan mengecek di database data register sudah tersimpan. 

## [WEEK 2](https://github.com/Muna-020/DEVOPS-BATCH-19/tree/master/stage-2/week2/day3)
### [1. Docker & Docker Compose](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week2/day3/Task3.MD)
- melakukan rebuild pada VM menjadi OS ubuntu 22 serta konfigurasi SSH-Password Only
- instalasi Docker menggunakan Bash Script 
- mempersiapkan seluruh aplikasi untuk melakukan deploy menggunakan Docker Compose
- Setup Docker Container agar seluruh Aplikasi dapat deploy dengan Docker Compose  
- menjalankan Docker Compose lalu mengakses aplikasi di web browser dengan domain yang sudah dibuat
- terakhir melakukan pull image untuk menyimpan image Docker seluruh aplikasi ke Docker registry

## [WEEK 3](https://github.com/Muna-020/DEVOPS-BATCH-19/tree/master/stage-2/week3)
### [1. Jenkins](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week3/day4/Task4.MD)
- melakukan rebuild pada VM menjadi OS ubuntu 22 serta konfigurasi SSH-Password Only
- pembuatan service jenkins dan nginx dengan reverse proxy dengan menggunakan docker
- membuat sebuah Jenkinsfile untuk pembuatan script agar dapat melakukan CI/CD 
- konfigurasi di jenkins untuk menjalankan CI/CD dengan metode Pipeline dengan SCM
- melihat hasil CI/CD yang sudah dijalankan sudah berhasil pada notifikasi di discord
- membuat sebuah auto trigger pada saat membuat perubahan pada file aplikasi di github repo
- terakhir, CI/CD telah berjalan secara otomatis ketika terdapat perubahan pada file di repo.

### [2. GitlabCI](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week3/day5/Task5.MD)
- melakukan pembuatan akun pada GItlab
- menyimpan publickey ke gitlab untuk koneksikan gitlba dengan server local
- membuat sebuah repository untuk menyimpan seluruh aplikasi frontend and backend
- konfigurasi di Gitlab untuk melakukan koneksi agar membuat notifikasi discord 
- membuat file .gitlab-ci.yml yang berisi script untuk menjalankan CI/CD 
- terakhir, ketika CI/CD berhasil dilakukan akan terlihat pada notifikasi discord CI/CD berhasil

## [WEEK 4](https://github.com/Muna-020/DEVOPS-BATCH-19/tree/master/stage-2/week4)
### [1. Monitoring](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week4/day6/Task6.MD)
- setup Container untuk membuat service Node Exporter, Prometheus, dan Grafana dan dijalankan pada setiap server yang ingin dimonitor.
- menjaalankan Prometheus untuk menyaring metrik dari Node Exporter dan menyimpannya dalam penyimpanan time series internal.
- Pembuatan Dashboard dengan menggunakan Grafana untuk memonitoring di seluruh server baik dari CPU, RAM, dan Penggunaan Disk
- konfigurasi pembuatan alerting notifikasi pada seluruh server apabila terdapat masalah.
- terakhir, melihat hasil notifikasi alert yang terkirim di discord.

### [2. Ansible & Ansible-playbook](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week4/day7/Task7.MD)
- menginstall docker serta menyiapkan aplikasi frontend
- menyiapkan VM untuk dipergunakan dalam melakukan ansible
- membuat seluruh script yang ingin kita gunakan dalam ansible

### [3. Kubernetes k3s](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week4/day8/Task8.MD)
- install k3s untuk membuat cluster dengan 2 node sebagai master dan node-1
- instalasi ingress untuk nginx 
- deploy aplikasi nginx dengan menggunakan ingress untuk dijalankan pada web browser
- setup untuk membuat persistent volume claim pada konfigurasi k3s
- deploy aplikasi database dengan mongodb menggunakan statefulset dan implementasi penggunaan PVC
- pembuatan database pada mongodb serta mengisi dummy data di dalamnya 

## [WEEK 5 FINAL-TASK](https://github.com/Muna-020/DEVOPS-BATCH-19/tree/master/stage-2/week5/final-task)
- Melakukan Persiapan untuk Deploy aplikasi pada seluruh server dengan penggunaan ansible {[Provisioning](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/1.Provisioning.MD)}
- Membuat repository baru di akun github untuk frontend dan backend yang sudah diclone dengan branch baru yaitu “staging” dan “production” (untuk mendukung pembuatan cicd) {[Repository](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/2.Repository.MD)}
- Melakukan konfigurasi pada penggunaan firewall di kedua server untuk mengizinkan port-port yang dapat dipakai dalam mengakses suatu aplikasi maupun server {[Server Management](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/3.Server-Management.MD)}
- Melakukan persiapan dalam mendeploy aplikasi di masing-masing direktori frontend dan backend, terlebih dahulu membuat Dockerfile untuk Dockerized dalam membuat image aplikasi frontend dan backend. {[Deployment](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/4.Deployment.MD)}
- Melakukan CICD pada aplikasi frontend dan backend yaitu dengan menggunakan GitlabCI {[CICD](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/5.CICD.MD)}
- Melakukan konfigurasi serta penggunaan SSL pada file reverse proxy untuk bisa mengakses kedua aplikasi dengan domain yang aman {[Web Server](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/6.Web-Server.MD)}
- melakukan beberapa konfigurasi pada prometheus untuk membuat koneksi agar dapat melakukan monitoring serta membuat sebuah basic auth pada file reverse proxy untuk promethus agar lebih aman. {[Monitoring](https://github.com/Muna-020/DEVOPS-BATCH-19/blob/master/stage-2/week5/final-task/7. Monitoring.MD)}

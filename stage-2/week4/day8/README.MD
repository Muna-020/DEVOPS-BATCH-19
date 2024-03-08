# Terraform
```
alat Infrastruktur sebagai Kode (IaC) yang digunakan developer untuk secara otomatis membuat, menyediakan, dan mengelola sumber daya IT cloud.Terraform dapat mengelola komponen tingkat rendah seperti sumber daya komputasi, penyimpanan, dan jaringan, serta komponen tingkat tinggi seperti entri DNS dan fitur SaaS.

Tahap ringkas dalam pengunaan k3s:
1. install k3s untuk membuat cluster dengan 2 node sebagai master dan node-1
2. instalasi ingress untuk nginx 
3. deploy aplikasi nginx dengan menggunakan ingress untuk dijalankan pada web browser
4. setup untuk membuat persistent volume claim pada konfigurasi k3s
5. deploy aplikasi database dengan mongodb menggunakan statefulset dan implementasi penggunaan PVC
6. pembuatan database pada mongodb serta mengisi dummy data di dalamnya 

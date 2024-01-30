#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Final Task


# DEPLOY APPLICATION DUMBMERCH

## 1. PROVISIONING
+ Melakukan Persiapan untuk segala pekerjaan dengan penggunaan ansible sebagai berikut: 
```
Requirements: 
+ ansible
+ Server BiznetGio:
     Appserver: 2GB RAM, 2 CPU
     Gateway: 1GB RAM, 1 CPU
     Registry-ahmad : 1GB RAM, 1 CPU
```

+ Pada tahap ini terlebih dahulu menyiapkan dua buah server yaitu server Gateway dan App-server.
+ memilih sebuah tools ansible sebagai untuk melakukan automation agar bisa menyediakan sarana yang dibutuhkan dalam pengerjaan deploy aplikasi
+ setelah menyiapkan script yang dibutuhkan seperti membuat user baru dan konfigurasi otentikasi ssh, instalasi docker, instalasi cerbot dan  generate SSL, kemudian mengclone repository dari github yaitu repository untuk backend dan             frontend, membuat script untuk monitoring yang berjalan di docker compose, serta konfigurasi reverse proxy dengan nginx menggunakan docker compose.
Provisiong menggunakan script ansible untuk :

+ Script Pembuatan User dan konfigurasi SSH pada ketiga server

```yaml
- hosts: biznet
  become: yes

  tasks:

    - name: Create user 'registry-ahmad' # finaltask-ahmad
      user:
        name: registry-ahmad 
        password: "{{ 'ahmad123' | password_hash('sha512') }}"
        shell: /bin/bash
        groups: sudo
        state: present
        system: true
        createhome: yes

    - name: Setup Auth Pubkey sshd_config
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PubkeyAuthentication no'
        line: 'PubkeyAuthentication yes'
      notify: Restart SSH Service

    - name: Setup File Cloud-Init sshd_config
      lineinfile:
        path: /etc/ssh/sshd_config.d/50-cloud-init.conf
        line: 'PubkeyAuthentication yes'
        backup: yes
      notify: Restart SSH Service

    - name: Make directory .SSH
      file:
        path: /home/registry-ahmad/.ssh
        state: directory
        owner: registry-ahmad
        group: registry-ahmad
        mode: "0700"

    - name: Make file pubkey
      file:
        path: /home/registry-ahmad/.ssh/authorized_keys
        state: touch
        owner: registry-ahmad
        group: registry-ahmad
        mode: "0600"

    - name: Add Pubkey SSH
      lineinfile:
        path: /home/registry-ahmad/.ssh/authorized_keys
        line: "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQD4QcMn2TC3eDoz0KSRo9O6TcC2kCZ2PnYtXk3Y2X3FSYPRDDEoLOP3FpKddfLVtbDu+FzyHf4Z6S8BjnFqAtjN3ZxDHMB7/gNhoV1R5w4AUoGfurlyoMMMA+VDWZPgMDpC8K4APzdUOLTeQ3yCDOu1nNEh7f89AmlJrNRSkUYagTfUkK2wmjxonwqg1O3Czo8r2jk1bZPHZeTqqNfjuP+FXHJ/legNCtlwkeYC4i0B6107tf1yZn7aJAKHeZzUrZx4iKXog305MRwpJrMhF0PONLhRd0nfqHl2Fq9oXSfWrtEECQpaSmlCUj+Mpv9lwvmz3m9HHpDoyk9aAHXGUHvteJVLrqi26gXc14ZB8C1imoZAilTZjeUFpUFDVZSNZCgJgqdKAWc67zz8LSolzzZNYIpoF4MwGcQp1yuGZjuP3UHIS1bNvMLJpnotGYH8vY3GCVPc6ZdEJVGYwUVmzTNZj7HFDbOF30ecsU16vmSSR2DGdIgKGWOMSY+yE40Eubs= flomad23@FloLup"

  handlers:
    - name: Restart SSH Service
      service:
        name: ssh
        state: restarted      

```

+ Script penginstalan docker untuk ketiga server

```yaml
- name: Install Docker
  hosts: biznet
  become: true
  tasks:
    - name: Update apt package cache and install dependencies
      apt:
        name: "{{ packages }}"
        state: present
        update_cache: yes
      vars:
        packages:
          - apt-transport-https
          - ca-certificates
          - curl
          - gnupg
          - lsb-release
    - name: Add Docker's official GPG key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker repository
      apt_repository:
        repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_lsb.codename }} stable"
        state: present

    - name: Install Docker and Docker Compose
      apt:
        name: 
          - docker-ce
          - docker-ce-cli
          - containerd.io
        state: present

    - name: Start and enable Docker service
      service:
        name: docker
        state: started
        enabled: yes

```
+ Script untuk melakukan generate cerbot certifate pada server Gateway dan Registry

```yaml

- name: Generate Certbot for SSL
  hosts: biznet
  become: true
  
  tasks:
    - name: Install Certbot via snap
      become: true
      become_user: root
      shell: |
       sudo snap install --classic certbot &&
       sudo ln -s /snap/bin/certbot /usr/bin/certbot &&
       sudo snap set certbot trust-plugin-with-root=ok &&
       sudo snap install certbot-dns-cloudflare
      register: certbot_install_result
      changed_when: "certbot_install_result.rc == 0"

    - name: Create Certbot configuration directory
      file:
          path: "/home/ahmad/.secrets"
          state: directory

    - name: Create Certbot Cloudflare credentials file
      template:
          src: ./credential/cloudflare.ini.j2  
          dest: "/home/ahmad/.secrets/cloudflare.ini"
          mode: 0400

    - name: Run Certbot to obtain certificates
      command: >
        certbot certonly
        --dns-cloudflare
        --dns-cloudflare-credentials /home/ahmad/.secrets/cloudflare.ini
        --agree-tos
        --non-interactive
        --email ahmad.munazar18@gmail.com
        --domains *.ahmad.studentdumbways.my.id # *.studentdumbways.my.id "Registry Server" 
      become: true
      become_user: root

```
```j2
# Cloudflare API credentials used by Certbot
dns_cloudflare_email= "ahmad.munazar18@gmail.com"
dns_cloudflare_api_key= "59c9d37614ceb06075f20e1cf30877d39a2dc"
```

+ Script persiapan untuk aplikasi frontend dan backend dumbmerch

```yaml
- name: Prepare Application Frontend
  hosts: 103.175.216.25
  become: true
  tasks:

    - name: Clone Git FE Repository
      git:
        repo: https://github.com/demo-dumbways/fe-dumbmerch.git
        dest: /home/finaltask-ahmad/fe-dumbmerch/
      become: true

    - name: Clone Git BE Repository
      git:
        repo: https://github.com/demo-dumbways/be-dumbmerch.git
        dest: /home/finaltask-ahmad/be-dumbmerch/
      become: true      
```

+ Script pembuatan Container untuk monitoring di server Appserver

```yaml

- name: Deploy Monitoring Stack
  hosts: 103.150.191.16
  tasks:

    - name: Create file Docker Compose
      template:
        src: ./credential/docker-compose.yaml.j2
        dest: /home/finaltask-ahmad/docker-compose.yaml
       
    - name: Run Docker Compose
      shell: docker compose up -d
      args:
        chdir: /home/finaltask-ahmad/      

```
```yaml

version: '3.8'

volumes:
  prometheus_data: {}

services:

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    ports:
      - 9100:9100
    networks:
      - ahmad

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
    ports:
      - 9090:9090
    networks:
      - ahmad

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: unless-stopped
    ports:
      - 3000:3000
    user: root
    volumes:
      - ./monitoring/grafana/provisioning/datasources:/etc/grafana/provisioning/datasources
      - ./monitoring/grafana/data:/var/lib/grafana
    networks:
      - ahmad

networks:
  ahmad:
    driver: bridge

```

```j2

global:
  scrape_interval: 10s
scrape_configs:
 - job_name: 'prometheus_metrics'
   scrape_interval: 5s
   static_configs:
     - targets: ['103.175.216.25:9090']
 - job_name: 'node_exporter_metrics'
   scrape_interval: 5s
   static_configs:
     - targets: ['103.150.191.16:9100', '103.175.216.25:9100']

```


+ Script membuat konfigurasi reverse proxy untuk persiapan container application dan monitoring di server gateway

```yaml

- name: Configure Nginx Reverse Proxy
  hosts: 103.150.191.16
  become: true
  tasks:
    - name: Create Nginx directory
      file:
        path: "/home/ahmad/nginxRproxy"
        state: directory

    - name: Create Nginx configuration for Reverseproxy
      template:
        src: ./credential/rProxy.conf.j2
        dest: /home/ahmad/nginxRproxy/rProxy.conf
```

```j2
server {
	listen 80;
	listen 443 ssl;
	server_name ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;
	
	location / {
		proxy_pass http://103.175.216.25:3000;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;       

	}
	
}

server {
	listen 80;
	listen 443 ssl;
	server_name api.ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;
	
	location / {
		proxy_pass http://103.175.216.25:3000;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;       

	}
	
}

server {
        listen 443 ssl;
        server_name exporter-gateway.ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://exporter-gateway:9100;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}

server {
	listen 443 ssl;
	server_name grafana.ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;
	
	location / {
		proxy_pass http://103.175.216.25:3000;
		proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
	}
	
}

server {
        listen 443 ssl;
        server_name prometheus.ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://103.175.216.25:9090;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}

server {
        listen 443 ssl;
        server_name exporter-app.ahmad.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://103.175.216.25:9100;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}


```
+ Script pembuatan Container Nginx untuk reverse proxy dan node-exporter pada server gateway

```
version: '3.8'
services:
 

  webserver:
    container_name: nginx
    restart: always
    image: nginx:latest
    user: root
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginxRproxy:/etc/nginx/conf.d
      - /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem:/etc/letsencrypt/live/ahmad.studentdumbways.my.id/fullchain.pem
      - /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem:/etc/letsencrypt/live/ahmad.studentdumbways.my.id/privkey.pem
    networks:
      local:  
  
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    ports:
      - 9100:9100
    networks:
      local:

networks:
  local:

```

```yaml

---
---
- name: Deploy Webserver Stack
  hosts: 103.150.191.16
  tasks:

    - name: Create file Docker Compose
      template:
        src: ./credential/exporter-service.j2
        dest: /home/finaltask-ahmad/docker-compose.yaml
       
    - name: Run Docker Compose
      shell: docker compose up -d
      args:
        chdir: /home/finaltask-ahmad/       
```
 ## 2. Repository
   
+ Setelah melakukan clone repository dengan automation dari ansible, dilanjutkan dengan mengakses tiap direktori backend dan frontend dumbmerch untuk melakukan konfigurasi file .env lalu membuat repository baru di akun github untuk frontend dan backend. Kemudian membuat sebuah branch baru dengan nama “staging” dan “production” (untuk mendukung pembuatan cicd)
+ setelah melakukan tahap diatas, kemudian melakukan push repository frontend dan backend dari app-server ke repository akun github.
Berikut gambaran tahap pengerjaan Repository:
![Screenshot from 2024-01-30 13-03-19](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/432197aa-8879-4e12-9d92-f6161f543bb4)
![Screenshot from 2024-01-28 16-15-32](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e4d3e33b-308d-4063-b74b-033214c3b7f6)
![Screenshot from 2024-01-28 16-15-46](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/399a0c0f-8e0a-4377-bd97-870045ae5583)
![Screenshot from 2024-01-28 16-16-06](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/a751a887-91c5-440e-b836-049dff28f659)
![Screenshot from 2024-01-28 16-16-17](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/210f8339-735b-47a6-8a8d-41db2b6976a4)
#
## 3. Server Management
  
+ Pada tahap ini terlebih dahulu membuat sebuah file untuk konfigurasi ssh di local-server dengan nama file “config” 
+ kemudian,melakukan konfigurasi pada penggunaan firewall di kedua server untuk mengizinkan port-port yang dapat dipakai dalam mengakses suatu aplikasi maupun server.
+ Selanjutnya, mengubah konfigurasi file sshd_config pada bagian port menjadi port 1234 lalu melakukan restart ssh service.
Berikut gambaran tahap pengerjaan Server Management:
![Screenshot from 2024-01-25 02-08-12](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e3111823-1d54-4213-97ba-651e9ba9f7a8)
![Screenshot from 2024-01-25 02-09-38](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/2591cc47-603d-472c-9bcc-1943c7ac9b1b)
![Screenshot from 2024-01-28 18-08-33](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8614389f-05f5-4767-af16-ea10a69a394f)
![Screenshot from 2024-01-29 00-52-47](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7d691bf2-5f9f-409a-bb65-fc54b510a9ad)
#
## 4. Deployment
   
+ Pada tahap ini melakukan persiapan dalam mendeploy aplikasi di masing-masing direktori frontend dan backend, terlebih dahulu membuat Dockerfile untuk Dockerized dalam membuat image aplikasi frontend dan backend. 
+ Setelah itu melakukan penambahan script untuk database postgresql serta aplikasi frontend dan backend agar berjalan di docker pada file docker compose.
+ Selanjutnya, membuat file .env yang berisi variabel dalam persiapan membuat database postgresql dan kedua aplikasi.
+ Menjalankan service database untuk melakukan persiapan migrasi data dari backend ke database.
+ Membuat sebuah image pada frontend dan backend “docker build -t flomad0411/dumbmerch-”fe/be”:1.0" 
+ Menjalankan seluruh services dari docker lalu melakukan push image ke docker hub
Berikut gambaran tahap pengerjaan Deployment:
![dcfilebe](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/eb40bd34-61ff-44d0-a9e7-44bfe50b2762)
![dcfilefe](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/683e6145-24e8-4b70-9bb1-fa56042a971b)
![Screenshot from 2024-01-29 05-27-09](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6ae2b24f-b657-4fd6-99df-c369956c42d7)
![plusapp](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7b9047a3-ab97-4399-ae76-397019cb4225)
![Screenshot from 2024-01-30 13-12-18](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/ba717b24-12dd-4606-8757-36adbb73c6c9)
![Screenshot from 2024-01-28 19-45-14](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4a8ca559-f2bc-4b3e-90d2-7f65e415627e)
#
## 5. CICD
   
+ Pada tahap ini dalam melakukan CICD pada aplikasi frontend dan backend yaitu dengan menggunakan GitlabCI.  
+ Selanjutnya, membuat sebuah repository di GitlabCI untuk menyiapkan sebuah file “.gitlab-ci.yml” agar bisa digunakan untuk CICD
+ Setelah itu, membuat sebuah script  agar melakukan CICD dari tahapan melakukan pull image di kedua branch yaitu “staging” dan “production pada kedua aplikasi, melakukan build image, melakukan test aplikasi, lalu deploy aplikasi dan melakukan push image ke docker hub 
Berikut gambaran tahap pengerjaan CICD:
![cicdstage](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/1f006437-ec60-4af3-b1ed-a21f0b35e542)
![cicdproduct](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/824bf07b-51f6-4492-891a-21fc57d7eb2c)
![Screenshot from 2024-01-29 08-01-32](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/363fbbcf-8746-41c9-a1cb-08f372bf161d)
![Screenshot from 2024-01-29 05-17-06](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/03661f4f-31e8-430c-adfd-ad02d91e00fc)
#
## 6.  Web Server
   
+ Di tahap ini, melakukan konfigurasi serta penggunaan SSL pada file reverse proxy untuk bisa mengakses kedua aplikasi dengan domain yang aman 
+ Menambahkan dua buah script pada docker compose yaitu service nginx untuk load balancing  
+ Melakukan penambahan DNS pada cloudflare untuk domain seluruh aplikasi.
+ Menjalankan services webserver untuk nginx yang berjalan di docker compose .
+ Melakukan testing akses serta register akun aplikasi frontend dan backend dumbmerch.
+ lalu mengecek pada database postgresql untuk melihat hasil register yang berhasil dibuat.
+ Kemudian membuat sebuah bash script untuk melakukan pembaruan certificate secara automasi
Berikut gambaran tahap pengerjaan Monitoring:
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

#
## 7.  Monitoring
   
+ Tahap selanjutnya ini, melakukan beberapa konfigurasi pada prometheus untuk membuat koneksi agar dapat melakukan monitoring serta membuat sebuah basic auth pada file reverse proxy untuk promethus agar lebih aman.  
+ Menjalankan grafana kemudian membuat Dashboard untuk monitoring seluruh server dengan query dari promQL.
+ Membuat sebuah konfigurasi untuk alerting atau peringatan pada suatu server yang di monitoring serta membuat koneksi dengan telegram untuk memberi notifikasi alert dari grafana
Berikut gambaran tahap pengerjaan Monitoring: 
![baprom](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/308cbe36-fc97-46b7-8898-7d37659ab9a6)
![promfix](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/4b229577-dca1-4314-b38b-909635b238e8)
![Screenshot from 2024-01-24 11-05-30](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8c09aece-3538-44a3-a2f3-2a380c0e530b)
![Screenshot from 2024-01-28 19-37-49](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/5fa73593-e880-49b1-b19b-6ec280fb2de3)
![Screenshot from 2024-01-28 19-38-04](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/fee75af4-a4b9-4ffd-ae51-9c4159801272)
![Screenshot from 2024-01-28 16-09-11](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/3156be50-5827-4676-873a-8c84273e1e5a)
![Screenshot from 2024-01-29 06-56-53](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/52562811-837c-4d70-9710-649fa966b79a)
![Screenshot from 2024-01-28 19-44-38](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/7f66a566-f6a3-452e-8a17-7b7bbd93a3b7)
![Screenshot from 2024-01-28 19-43-48](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/213bd746-c3a7-49fd-bce4-9a3a1771e6ed)
![Screenshot from 2024-01-24 20-25-16](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/83b0e5ea-a440-41ec-b922-4873d2122f22)



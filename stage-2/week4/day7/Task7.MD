# Ansible & Ansible-Playbook

```
Ansible adalah platform otomatisasi open-source yang digunakan untuk mengotomatiskan tugas-tugas konfigurasi, penyebaran, dan manajemen sistem. Ansible dirancang untuk memberikan cara yang sederhana dan efisien untuk mengelola infrastruktur IT, termasuk server fisik, mesin virtual, dan lingkungan cloud.
Ansible Playbook adalah skrip yang ditulis dalam format YAML yang berisi serangkaian langkah-langkah atau tugas yang harus dijalankan oleh Ansible pada host tertentu. Playbook memungkinkan Anda untuk mendefinisikan konfigurasi infrastruktur secara terstruktur dan dapat diulang.

Ringkasan tahapan pengerjaan untuk Ansible dan Ansible-Playbook:
- menginstall docker serta menyiapkan aplikasi frontend
- menyiapkan VM untuk dipergunakan dalam melakukan ansible
- membuat seluruh script yang ingin kita gunakan dalam ansible
```

#### 1. Membuat User baru untuk server gateway dan app-server

```yaml
- hosts: biznet
  become: yes

  tasks:
    - name: Create user 'ahmad'
      user:
        name: ahmad
        password: "{{ 'ahmad123' | password_hash('sha512') }}"
        shell: /bin/bash
        groups: sudo
        state: present
        system: true
        createhome: yes
        
    - name: Setup sshd_config
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PasswordAuthentication'
        line: 'PasswordAuthentication yes'
        backup: yes
      notify: Restart SSH Service

  handlers:
    - name: Restart SSH Service
      service:
        name: sshd
        state: restarted   
```

#### 2. Melakukan instalasi docker untuk kedua server
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
   
    - name: Add user to Docker group
      user:
        name: ahmad
        groups: docker
        append: yes
```

#### 3. melakukan generate SSL untuk kedua server menggunakan Certbot Let's Encrypt
```yaml
---
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
        --domains *.studentdumbways.my.id
      become: true
      become_user: root
```
```j2
# Cloudflare API credentials used by Certbot
dns_cloudflare_email= "ahmad.munazar18@gmail.com"
dns_cloudflare_api_key= "59c9d37614ceb06075f20e1cf30877d39a2dc"
```
#### 4. membuat konfigurasi reverse proxy untuk persiapan container monitoring di server gateway
```j2
server {
	listen 443 ssl;
	server_name grafana-ahmadmun.studentdumbways.my.id;

	ssl_certificate /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem;
	
	location / {
		proxy_pass http://grafana:3000;
		proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
	}
	
}

server {
        listen 443 ssl;
        server_name prometheus-ahmadmun.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://prometheus:9090;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}

server {
        listen 443 ssl;
        server_name exporter-ahmadmun.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://node-exporter:9100;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}

```
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

####  5. melakukan setup pembuatan container untuk monitoring server di gateway 
```j2
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
      - monitoring

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
      - monitoring

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
      - monitoring

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
      - /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem:/etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem
      - /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem:/etc/letsencrypt/live/studentdumbways.my.id/privkey.pem
    networks:
      monitoring:

networks:
  monitoring:
    driver: bridge
```
```yaml
- name: Deploy Monitoring Stack
  hosts: 103.150.191.16
  become: true
  tasks:

    - name: Create Monitoring directory
      file:
        path: "/home/ahmad/monitoring"
        state: directory

    - name: Create file Docker Compose
      template:
        src: ./credential/docker-compose.yaml.j2
        dest: /home/ahmad/docker-compose.yaml

    - name: Create file Prometheus
      template:
        src: ./credential/prometheus.yml.j2
        dest: /home/ahmad/monitoring/prometheus.yml        

    - name: Create and start services
      become: yes
      shell: docker compose up -d
      args:
        chdir: /home/ahmad
```

#### 6. melakukan persiapan untuk aplikasi froontend di server app-server
```j2
FROM node:10.23.0-alpine

WORKDIR apps

COPY . .

RUN npm install

RUN npm install pm2 -g

EXPOSE 3000

CMD ["npm", "start"]

```
```yaml
- name: Prepare Application Frontend
  hosts: 103.175.216.25
  become: true
  tasks:

    - name: Clone Git Repository
      git:
        repo: https://github.com/dumbwaysdev/dumbflix-frontend.git
        dest: /home/ahmad/dumbflix-frontend/
      become: true

    - name: Update cache
      apt:
        update_cache: yes

    - name: Create file Dockerfile
      template:
        src: ./credential/Dockerfile-fe.j2
        dest: /home/ahmad/dumbflix-frontend/Dockerfile     

    - name: Setup Config frontend
      lineinfile:
        path: /home/ahmad/dumbflix-frontend/src/config/api.js
        regexp: "baseURL: 'http://localhost:5000/api/v1'"
        line: "baseURL: 'https://api-moonflo.studentdumbways.my.id/api/v1'"
        backup: yes
```

#### 7. membuat konfigurasi reverse proxy untuk persiapan container aplikasi frontend di server app-server
```j2
server {
	listen 80;
	listen 443 ssl;
	server_name flomoon.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem;
	
	location / {
		proxy_pass http://frontend:3000;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;       

	}
	
}

server {
        listen 443 ssl;
        server_name exporter-flomoon.studentdumbways.my.id;

        ssl_certificate /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem;

        location / {
                proxy_pass http://node-exporter:9100;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-Host $host;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        }

}

```
```yaml
- name: Configure Nginx Reverse Proxy
  hosts: 103.175.216.25
  become: true
  tasks:
    - name: Create Nginx directory
      file:
        path: "/home/ahmad/nginxRproxy"
        state: directory

    - name: Create Nginx configuration for Reverseproxy
      template:
        src: ./credential/rProxy-app.conf.j2
        dest: /home/ahmad/nginxRproxy/rProxy.conf
```

#### 8.  melakukan setup container untuk deploy aplikasi frontend di app-server 
```j2
version: '3.8'
services:
 
  frontend: 
    container_name: fe
    image: flomad0411/frontend:1.0
    ports:
      - "3000:3000"
    networks:
      local:

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
      - /etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem:/etc/letsencrypt/live/studentdumbways.my.id/fullchain.pem
      - /etc/letsencrypt/live/studentdumbways.my.id/privkey.pem:/etc/letsencrypt/live/studentdumbways.my.id/privkey.pem
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

- name: Deploy Frontend Stack
  hosts: 103.175.216.25
  become: true
  tasks:

    - name: Create file Docker Compose
      template:
        src: ./credential/frontend-service.j2
        dest: /home/ahmad/docker-compose.yaml
   
    - name: Create and start services
      become: yes
      shell: docker compose up -d
      args:
        chdir: /home/ahmad

```


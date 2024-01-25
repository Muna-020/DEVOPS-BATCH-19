#### Nama : Ahmad Munazar
#### Kelas : DevOps Batch 19
#### Final Task


# DEPLOY APPLICATION DUMBMERCH

 ##### Melakukan Persiapan untuk segala pekerjaan dengan penggunaan ansible sebagai berikut: 
```
Requirements: 
+ ansible
+ Server BiznetGio:
     Appserver: 2GB RAM, 2 CPU
     Gateway: 1GB RAM, 1 CPU
     Registry-ahmad : 1GB RAM, 1 CPU
```
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
        regexp: '^#?Port 22'
        line: 'Port 1234'
      notify: Restart SSH Service

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

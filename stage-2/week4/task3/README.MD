# Kubernetes k3s 

### Membuat Script dengan ansible untuk automation user baru, install docker, instalasi monitoring server, setup reverse proxy, deploy app-frontend dengan docker

#### -
```yaml

apiVersion: v1
kind: Namespace
metadata:
  name: nginx-ingress

---
 
apiVersion: helm.cattle.io/v1
kind: HelmChart
metadata:
  name: ingress-nginx
  namespace: nginx-ingress
spec:
  repo: https://kubernetes.github.io/ingress-nginx
  chart: ingress-nginx
  targetNamespace: nginx-ingress
  valuesContent: |-
    controller:
      image:
        tag: "v1.8.1"
      service:
        type: LoadBalancer
```
#### 2. Melakukan instalasi docker untuk kedua server
```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-app
  namespace: devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: webserver
        image: nginx:alpine
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-app-service
  namespace: devops
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
  type: NodePort

---

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-app-ingress
  annotations:
    kubernetes.io/ingress.class: "nginx"
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: munazar.studentdumbways.my.id
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: nginx-app-service
            port: 
              number: 80
```
```shell
$ ~/.kube$ kubectl get all -n devops
NAME                             READY   STATUS    RESTARTS   AGE
pod/nginx-app-64dd5dc9db-x46cw   1/1     Running   0          7h32m
pod/test-volume                  1/1     Running   0          5h54m

NAME                        TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE
service/nginx-app-service   NodePort   10.43.243.200   <none>        80:31217/TCP      7h32m

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-app   1/1     1            1           7h32m

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-app-64dd5dc9db   1         1         1       7h32m

```
#### 3. melakukan generate SSL untuk kedua server menggunakan Certbot Let's Encrypt
```yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: local-path-pvc
  namespace: devops
spec:
  storageClassName: local-path
  resources:
    requests:
      storage: 2Gi
  accessModes:
    - ReadWriteOnce

```
```shell

$ kubectl get pvc 
NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
local-path-pvc   Bound    pvc-1757bf74-513f-4a6b-93d6-67b509e5e70f   2Gi        RWO            local-path     7h13m

```
#### Script implementasi PVC

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: test-volume
  namespace: devops
spec:
  containers:
  - name: test-volume
    image: nginx:alpine
    imagePullPolicy: Always
    volumeMounts:
    - name: vol 
      mountPath: /data
    ports:
      - containerPort: 80
  volumes:
  - name: vol
    persistentVolumeClaim:
      claimName: local-path-pvc

```

####  5. melakukan setup pembuatan container untuk monitoring server di gateway 
![Screenshot from 2024-01-14 12-23-53](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/b762d5ea-a597-4676-9b3d-4a23871249e5)
![Screenshot from 2024-01-14 12-24-03](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e3e885f5-af9f-4ce7-9a1d-00e82a47d495)
![Screenshot from 2024-01-14 12-24-27](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/3d29fec6-b996-42ef-a674-43ab6c2d3a20)
![Screenshot from 2024-01-14 12-23-29](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/79baca03-01d7-4189-9cbe-f10f32a76978)

#### 6. melakukan persiapan untuk aplikasi froontend di server app-server
![Screenshot from 2024-01-14 12-43-34](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/fd31ddda-37ca-4295-9cb3-b885b1c970b2)
![Screenshot from 2024-01-14 12-40-44](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/f6534b21-48be-400f-9c4c-87a46081a16a)

#### 7. membuat konfigurasi reverse proxy untuk persiapan container aplikasi frontend di server app-server
![Screenshot from 2024-01-14 12-48-15](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/8047f49b-3f00-4473-bf37-69f7f9349f77)
![Screenshot from 2024-01-14 12-44-51](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/e9482222-c778-41df-8c67-110d8ac5f345)

#### 8.  melakukan setup container untuk deploy aplikasi frontend di app-server 
![Screenshot from 2024-01-14 12-55-12](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6e3a66c5-3d6d-48cd-8c10-47479fce62e1)
![Screenshot from 2024-01-14 12-54-24](https://github.com/Muna-020/DEVOPS-BATCH-19/assets/74352384/6047aaac-6ad3-4f17-9795-365448c90208)

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


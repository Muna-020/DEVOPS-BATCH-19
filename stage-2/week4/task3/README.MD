# Kubernetes k3s 

### Membuat Script dengan ansible untuk automation user baru, install docker, instalasi monitoring server, setup reverse proxy, deploy app-frontend dengan docker

#### Instalasi ingress nginx

```shell
/var/lib/rancher/k3s/server/manifests# ls
ccm.yaml  coredns.yaml  local-storage.yaml  metrics-server  nginx-ingress.yaml  rolebindings.yaml  runtimes.yaml
```
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
#### - Deploy nginx app dengan ingress nginx
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

NAME                        TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE
service/nginx-app-service   NodePort   10.43.243.200   <none>        80:31217/TCP      7h32m

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-app   1/1     1            1           7h32m

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-app-64dd5dc9db   1         1         1       7h32m

```
#### Make PVC with default local path
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
#### Script for bounding PVC

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

```shell
$ ~/.kube$ kubectl get pods -n devops
NAME                             READY   STATUS    RESTARTS   AGE
pod/nginx-app-64dd5dc9db-x46cw   1/1     Running   0          7h32m
pod/test-volume                  1/1     Running   0          5h54m

```

####  Deploy mongodb app use stateful.set and PVC
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque
data:
  MONGO_INITDB_ROOT_USERNAME: YWhtYWQ=
  MONGO_INITDB_ROOT_PASSWORD: YWhtYWQxMjM=
  MONGO_INITDB_DATABASE: YXBwZGI=

---

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mongodb
spec:
  serviceName: "mongodb"
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
        - name: mongodb
          image: mongo:4.4
          envFrom:
             - secretRef:
                 name: mongodb-secret
                 optional: false
          volumeMounts:
            - name: mongodb-storage
              mountPath: /data/db
      volumes:
      - name: mongodb-storage
        persistentVolumeClaim:
          claimName: local-path-pvc

---

apiVersion: v1
kind: Service
metadata:
  name: mongodb
spec:
  selector:
    app: mongodb
  type: NodePort
  ports:
    - name: port
      port: 27017
      targetPort: 27017
  
```

```shell

$ /mnt/disk1/pvc-1757bf74-513f-4a6b-93d6-67b509e5e70f_devops_local-path-pvc# ls
WiredTiger         collection-0--5415748615189943430.wt  diagnostic.data                  index-6--5415748615189943430.wt
WiredTiger.lock    collection-0--844076755098378161.wt   index-1--5415748615189943430.wt  index-8--5415748615189943430.wt
WiredTiger.turtle  collection-2--5415748615189943430.wt  index-1--844076755098378161.wt   index-9--5415748615189943430.wt
WiredTiger.wt      collection-2--844076755098378161.wt   index-3--5415748615189943430.wt  journal
WiredTigerHS.wt    collection-4--5415748615189943430.wt  index-3--844076755098378161.wt   mongod.lock
_mdb_catalog.wt    collection-4--844076755098378161.wt   index-5--5415748615189943430.wt  sizeStorer.wt
ahmad              collection-7--5415748615189943430.wt  index-5--844076755098378161.wt   storage.bson


```
```mongo

root@mongodb-0:/# mongo -u ahmad -p ahmad123 --authenticationDatabase admin
MongoDB shell version v4.4.27
connecting to: mongodb://127.0.0.1:27017/?authSource=admin&compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("df54ed42-e98b-4c22-af5a-f155059d27a8") }
MongoDB server version: 4.4.27
---
The server generated these startup warnings when booting: 
        2024-01-18T10:02:14.763+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
---
> use appdb
switched to db appdb
> show dbs
admin   0.000GB
appdb   0.000GB
config  0.000GB
local   0.000GB

```



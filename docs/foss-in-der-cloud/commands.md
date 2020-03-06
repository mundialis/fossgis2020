```

✔ ~/repos/myproject/actinia-build [master {origin/master}|✔]
11:02 $ ls -lah
-rw-r--r-- 1 user user 1,2K Mär  6 11:36 actinia.cfg
-rw-r--r-- 1 user user 1,4K Mär  6 11:02 Dockerfile
-rw-r--r-- 1 user user   19 Mär  6 11:02 ESA_credentials.txt
drwxr-xr-x 8 user user 4,0K Mär  6 11:02 .git
-rw-r--r-- 1 user user  491 Mär  6 11:02 .gitlab-ci.yml
drwxr-xr-x 3 user user 4,0K Mär  6 11:02 pc_templates
-rw-r--r-- 1 user user 4,2K Mär  6 11:02 README.md


FROM mundialis/actinia-core:g78-latest-alpine

COPY actinia.cfg /etc/default/actinia
COPY ESA_credentials.txt ESA_credentials.txt
COPY pc_templates /etc/default/actinia_pc_templates

RUN grass --tmp-location EPSG:4326 --exec g.extension -s extension=i.sentinel



```
```
✔ ~/repos/myproject/actinia-build [master {origin/master}|✔]
11:02 $ ls -lah
-rw-r--r-- 1 user user 1,4K Mär  6 11:02 Dockerfile
drwxr-xr-x 8 user user 4,0K Mär  6 11:02 .git
-rw-r--r-- 1 user user  491 Mär  6 11:02 .gitlab-ci.yml
-rw-r--r-- 1 user user 4,2K Mär  6 11:02 README.md


FROM mundialis/actinia-core:g78-latest-alpine

RUN grass --tmp-location EPSG:4326 --exec g.extension -s extension=i.sentinel


```
```



12:12 $ helm create actinia
Creating actinia

12:12 $ tree actinia
actinia
├── charts
├── Chart.yaml
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml



```
```
12:12 $ helm create actinia
Creating actinia

12:12 $ tree actinia
actinia
├── charts
├── Chart.yaml
├── templates
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── ingress.yaml
│   ├── secret.yaml
│   ├── NOTES.txt
│   └── service.yaml
├── values.yaml
├── values-dev.yaml
├── values-int.yaml
└── values-prod.yaml
```
```


apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ include "actinia.fullname" . }}
  labels:
{{ include "actinia.labels" . | indent 4 }}
data:
  actinia-config: |
    [GRASS]
    grass_gis_start_script = /usr/local/bin/grass
    grass_database = /actinia_core/grassdb
    grass_user_database = /actinia_core/userdata

    [API]
    plugins = ["actinia_gdi"]

    [LIMITS]
    max_cell_limit = 2000000
    process_time_limt = 60
    process_num_limit = 20
    number_of_workers = 3

```
```


apiVersion: apps/v1
kind: Deployment
spec:
  replicas: {{ .Values.replicaCount }}
  template:
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          command: ['sh']
          args: ['/src/start/start.sh']
          volumeMounts:
          - name: config
            mountPath: /etc/default/actinia-config
          - name: secret
            mountPath: /etc/default/actinia-secret
          - name: pctemplates
            mountPath: /etc/default/actinia_pc_templates
          - name: grassdb
            mountPath: /actinia_core/grassdb/
          env:
          - name: DEFAULT_CONFIG_PATH
            value: /etc/default/actinia-config/actinia.cfg
      volumes:
        - name: config
          configMap:
            name: {{ include "actinia.fullname" . }}
            items:
            - key: actinia-core-config
              path: actinia.cfg
        - name: secret
          secret:
            secretName: {{ include "actinia.fullname" . }}
            items:
            - key: ESA_credentials.txt
              path: ESA_credentials.txt
            - key: .grass7
              path: .grass7
        - name: pctemplates
          configMap:
            name: {{ include "actinia.fullname" . }}-pc-templates
        - name: grassdb
          persistentVolumeClaim:
            claimName: {{ include "actinia.fullname" . }}-grassdb


```
```

kubectl config use-context gke_hermosa-abcdefghi

helm lint actinia
helm template actinia
helm install actinia

```
```
09:17 $ kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/dev-actinia-0                        1/1     Running   0          14h
pod/dev-geoserver-7cc754556-9vcv9        1/1     Running   0          14h
pod/dev-landing-page-bf54476cd-6t5ql     1/1     Running   0          15h
pod/dev-nfs-server-7fbf6cdcf9-fz4lg      1/1     Running   0          15h
pod/dev-postgis-0                        1/1     Running   0          14h
pod/dev-redis-master-0                   1/1     Running   0          15h
pod/dev-shogun-hermosa-c7f5fcc94-zxpc8   1/1     Running   0          14h

NAME                                TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE
service/cm-acme-http-solver-ncf6v   NodePort    10.36.4.43     <none>        8089:30203/TCP               77d
service/dev-actinia                 NodePort    10.36.10.234   <none>        8088:31571/TCP               16d
service/dev-geoserver               NodePort    10.36.1.139    <none>        8080:30435/TCP               86d
service/dev-landing-page            NodePort    10.36.4.201    <none>        80:30368/TCP                 79d
service/dev-nfs-server              ClusterIP   10.36.10.227   <none>        2049/TCP,20048/TCP,111/TCP   113d
service/dev-postgis                 ClusterIP   10.36.7.213    <none>        5432/TCP                     118d
service/dev-redis-headless          ClusterIP   None           <none>        6379/TCP                     118d
service/dev-redis-master            ClusterIP   10.36.12.217   <none>        6379/TCP                     118d
service/dev-shogun-hermosa          NodePort    10.36.15.40    <none>        8080:31167/TCP               22h

NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/dev-geoserver        1/1     1            1           86d
deployment.apps/dev-landing-page     1/1     1            1           79d
deployment.apps/dev-nfs-server       1/1     1            1           113d
deployment.apps/dev-shogun-hermosa   1/1     1            1           22h

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/dev-geoserver-7cc754556        1         1         1       86d
replicaset.apps/dev-landing-page-bf54476cd     1         1         1       79d
replicaset.apps/dev-nfs-server-7fbf6cdcf9      1         1         1       113d
replicaset.apps/dev-shogun-hermosa-c7f5fcc94   1         1         1       22h

NAME                                READY   AGE
statefulset.apps/dev-actinia        1/1     16d
statefulset.apps/dev-postgis        1/1     118d
statefulset.apps/dev-redis-master   1/1     118d
```

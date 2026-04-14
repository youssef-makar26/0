u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl get pods -n banking -w
NAME                                 READY   STATUS              RESTARTS   AGE
banking-api-7f8b49695-drmbl          1/1     Running             0          11m
banking-api-7f8b49695-vktj4          1/1     Running             0          11m
banking-dashboard-564595d7b5-8kbm9   1/1     Running             0          11m
postgres-db-0                        1/1     Running             0          104s
postgres-db-1                        0/1     ContainerCreating   0          2s
postgres-db-1                        0/1     Running             0          2s
postgres-db-1                        0/1     Running             0          7s
postgres-db-1                        1/1     Running             0          18s
^Cu1@ubuntu-desktop1:~/project k8s/k8skubectl get pods -n bankingng
kubectl get statefulset postgres-db -n banking
NAME                                 READY   STATUS    RESTARTS   AGE
banking-api-7f8b49695-drmbl          1/1     Running   0          11m
banking-api-7f8b49695-vktj4          1/1     Running   0          11m
banking-dashboard-564595d7b5-8kbm9   1/1     Running   0          11m
postgres-db-0                        1/1     Running   0          2m21s
postgres-db-1                        1/1     Running   0          39s
NAME          READY   AGE
postgres-db   2/2     2m21s
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl logs -n banking deployment/banking-api
Found 2 pods, using pod/banking-api-7f8b49695-drmbl

> banking-api@1.0.0 start
> node app.js

Banking API vv1.1 listening on :3000
DB_HOST=postgres-db-0.postgres-db.banking.svc.cluster.local, LOG_LEVEL=info
DB init failed: getaddrinfo ENOTFOUND postgres-db-0.postgres-db.banking.svc.cluster.local
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl get pods -n banking
NAME                                 READY   STATUS    RESTARTS   AGE
banking-api-7f8b49695-drmbl          1/1     Running   0          12m
banking-api-7f8b49695-vktj4          1/1     Running   0          12m
banking-dashboard-564595d7b5-8kbm9   1/1     Running   0          12m
postgres-db-0                        1/1     Running   0          2m31s
postgres-db-1                        1/1     Running   0          49s
u1@ubuntu-desktop1:~/project k8s/k8s$ 


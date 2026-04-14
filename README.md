# 0
0
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl get pods -n banking
NAME                                 READY   STATUS    RESTARTS   AGE
banking-api-7f8b49695-drmbl          0/1     Running   0          41s
banking-api-7f8b49695-vktj4          0/1     Running   0          41s
banking-dashboard-564595d7b5-8kbm9   0/1     Running   0          41s
postgres-db-0                        0/1     Pending   0          42s
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl describe pod postgres-db-0 -n banking
kubectl describe pod banking-api-7f8b49695-fb2g7 -n banking
kubectl describe pod banking-dashboard-564595d7b5-k8tz4 -n banking
Name:             postgres-db-0
Namespace:        banking
Priority:         0
Service Account:  default
Node:             <none>
Labels:           app=postgres-db
                  apps.kubernetes.io/pod-index=0
                  controller-revision-hash=postgres-db-5545bdb455
                  statefulset.kubernetes.io/pod-name=postgres-db-0
Annotations:      <none>
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    StatefulSet/postgres-db
Containers:
  postgres:
    Image:      postgres:15-alpine
    Port:       5432/TCP
    Host Port:  0/TCP
    Liveness:   exec [sh -c pg_isready -U $POSTGRES_USER -d $POSTGRES_DB] delay=30s timeout=1s period=30s #success=1 #failure=3
    Readiness:  exec [sh -c pg_isready -U $POSTGRES_USER -d $POSTGRES_DB] delay=10s timeout=1s period=10s #success=1 #failure=3
    Startup:    exec [sh -c pg_isready -U $POSTGRES_USER -d $POSTGRES_DB] delay=0s timeout=1s period=5s #success=1 #failure=20
    Environment:
      POSTGRES_DB:        <set to the key 'DB_NAME' of config map 'banking-config'>  Optional: false
      POSTGRES_USER:      <set to the key 'DB_USER' of config map 'banking-config'>  Optional: false
      POSTGRES_PASSWORD:  <set to the key 'DB_PASSWORD' in secret 'banking-secret'>  Optional: false
      PGDATA:             /var/lib/postgresql/data/pgdata
    Mounts:
      /var/lib/postgresql/data from postgres-data (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-bh68x (ro)
Conditions:
  Type           Status
  PodScheduled   False 
Volumes:
  postgres-data:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  postgres-data-postgres-db-0
    ReadOnly:   false
  kube-api-access-bh68x:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 database-only=true:NoSchedule
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason            Age                From               Message
  ----     ------            ----               ----               -------
  Warning  FailedScheduling  43s (x5 over 48s)  default-scheduler  0/3 nodes are available: pod has unbound immediate PersistentVolumeClaims. not found
  Warning  FailedScheduling  43s (x2 over 43s)  default-scheduler  0/3 nodes are available: 1 node(s) didn't match PersistentVolume's node affinity, 2 node(s) didn't match Pod's node affinity/selector. no new claims to deallocate, preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.
Error from server (NotFound): pods "banking-api-7f8b49695-fb2g7" not found
Error from server (NotFound): pods "banking-dashboard-564595d7b5-k8tz4" not found
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl get pods -n banking -w
NAME                                 READY   STATUS    RESTARTS   AGE
banking-api-7f8b49695-drmbl          0/1     Running   0          53s
banking-api-7f8b49695-vktj4          0/1     Running   0          53s
banking-dashboard-564595d7b5-8kbm9   1/1     Running   0          53s
postgres-db-0                        0/1     Pending   0          54s
kubectl get statefulset postgres-db -n banking
^Cu1@ubuntu-desktop1:~/project k8s/k8s$ ^[[200~kubectl get statefulset postgres-db -n banking~
kubectl: command not found
u1@ubuntu-desktop1:~/project k8s/k8s$ kubectl get statefulset postgres-db -n banking
NAME          READY   AGE
postgres-db   0/2     78s
u1@ubuntu-desktop1:~/project k8s/k8s$ 

## Deploy Deployment on Openshift/k8s

### 1. Create new project deployment
```bash
D:\CodeWorkspace\learn-openshift\9.deployment>oc new-project deployment
Now using project "deployment" on server "https://2886795278-8443-cykoria05.environments.katacoda.com:443".
```

### 2. Create  deployment
```bash
D:\CodeWorkspace\learn-openshift\9.deployment>oc apply -f deployment.yml
deployment.apps/nginx created
service/nginx unchanged
```

### 3. Get Pod
```bash
D:\CodeWorkspace\learn-openshift\9.deployment>oc get pods
NAME                     READY   STATUS              RESTARTS   AGE
nginx-7dc5879c84-7ft4q   0/1     ContainerCreating   0          5s
nginx-7dc5879c84-ch6rj   0/1     ContainerCreating   0          5s

D:\CodeWorkspace\learn-openshift\9.deployment>oc get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-7dc5879c84-7ft4q   1/1     Running   0          30s
nginx-7dc5879c84-ch6rj   1/1     Running   0          30s
```

### 4. Get deployment
```bash
D:\CodeWorkspace\learn-openshift\9.deployment>oc get deployment
NAME    DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
nginx   2         2         2            2           55s

```

### 5. Get all
```bash
D:\CodeWorkspace\learn-openshift\9.deployment>oc get all
NAME                         READY   STATUS    RESTARTS   AGE
pod/nginx-58f688455d-6nw9d   1/1     Running   0          11s
pod/nginx-58f688455d-dwgb5   1/1     Running   0          11s

NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
service/nginx   ClusterIP   172.30.72.13   <none>        8080/TCP   10s

NAME                    DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx   2         2         2            2           14s

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-58f688455d   2         2         2       14s
```
## Deploy replication-controller on Openshift/k8s

### 1. Create new project replication-controller
```bash
$oc new-project replication-controller
```
### 2. Get replication-controller Object
```bash
$ oc get rc
NAME       DESIRED   CURRENT   READY   AGE
hello-rc   3         3         1       1m
```
### 3. check 3 pods are running
```bash
$ oc get pods -o wide
NAME             READY   STATUS    RESTARTS   AGE   IP            NODE     NOMINATED NODE
hello-rc-ds5gn   1/1     Running   0          1m    10.128.0.44   master   <none>
hello-rc-jbtjm   1/1     Running   0          18s   10.128.0.46   master   <none>
hello-rc-nfdxh   1/1     Running   0          18s   10.128.0.45   master   <none>
```
### 4. delete one pod
```bash
$ oc delete pod hello-rc-ds5gn
pod "hello-rc-ds5gn" deleted
```
### 5. Get Pods - Observe that new pod created automatically
```bash
$ oc get pods -w
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-6rhb9   1/1     Running   0          9s
hello-rc-jbtjm   1/1     Running   0          47s
hello-rc-nfdxh   1/1     Running   0          47s
```
### 6. Increase replica to 5
```bash
$ oc scale rc hello-rc --replicas=5
replicationcontroller/hello-rc scaled
```

### 7. Get Pods - Observer 2 new pods are created
```bash
$ oc get pods
NAME             READY   STATUS              RESTARTS   AGE
hello-rc-6rhb9   1/1     Running             0          2m
hello-rc-9f4wh   0/1     ContainerCreating   0          5s
hello-rc-jbtjm   1/1     Running             0          2m
hello-rc-nfdxh   1/1     Running             0          2m
hello-rc-zw6wp   0/1     ContainerCreating   0          5s

$ oc get pods
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-6rhb9   1/1     Running   0          2m
hello-rc-9f4wh   1/1     Running   0          10s
hello-rc-jbtjm   1/1     Running   0          2m
hello-rc-nfdxh   1/1     Running   0          2m
hello-rc-zw6wp   1/1     Running   0          10s
```

### 8. Scale donw application to 0
```bash
$ oc scale rc hello-rc --replicas=0
replicationcontroller/hello-rc scaled

$ oc get pods
NAME             READY   STATUS        RESTARTS   AGE
hello-rc-6rhb9   0/1     Terminating   0          2m
hello-rc-9f4wh   0/1     Terminating   0          23s
hello-rc-jbtjm   0/1     Terminating   0          3m
hello-rc-zw6wp   0/1     Terminating   0          23s

$ oc get pods
No resources found in replication-control namespace.
```

### 9. Start one replica
```bash
$ oc scale rc hello-rc --replicas=1
replicationcontroller/hello-rc scaled

$ oc get pods
NAME             READY   STATUS              RESTARTS   AGE
hello-rc-jghxq   0/1     ContainerCreating   0          5s


$ oc get pods
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-jghxq   1/1     Running   0          22s
```

oc delete rc hello-rc
replicationcontroller "hello-rc" deleted

oc get all
No resources found in replication-control namespace.
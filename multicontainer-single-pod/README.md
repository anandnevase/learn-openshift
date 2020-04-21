## Deploy multicontainer single pod on Openshift/k8s

### 1. Create new project single-pod
```bash
$ oc new-project multicontainer-pod
```
### 2. Create pod using manifest file 
```bash
$ oc create -f multicontainer-single-pod.yml
pod/multicontainer-single-app created
```
### 3. Get Pod
```bash
$ oc get pods
NAME                        READY   STATUS    RESTARTS   AGE
multicontainer-single-app   4/4     Running   0          1m
```
### 4. Describe POD
```bash
$ oc describe pod hello-app
```
### 5. Check counter container logs 
  
```bash
$ oc logs multicontainer-single-app -c counter
Incrementing counter by 5 ...
Incrementing counter by 2 ...
Incrementing counter by 10 ...
Incrementing counter by 9 ...
Incrementing counter by 9 ...
Incrementing counter by 5 ...
Incrementing counter by 10 ...
Incrementing counter by 10 ...
```

### 6. Check counter container logs 
  
```bash
$ oc logs multicontainer-single-app -c poller
Current counter: 35
Current counter: 50
Current counter: 65
Current counter: 82
Current counter: 97
Current counter: 108
Current counter: 115
```

### 7. Delete Pod
```bash
$ oc delete -f multicontainer-single-pod.yml
pod "hello-app" deleted
```
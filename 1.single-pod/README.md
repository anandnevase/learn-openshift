## Deploy single pod on Openshift/k8s

### 1. Create new project single-pod
```bash
$ oc new-project single-pod
```
### 2. Create pod using manifest file 
```bash
$ oc create -f single-pod.yml
pod/hello-app created
```
### 3. Get Pod
```bash
$ oc get pods
NAME        READY   STATUS    RESTARTS   AGE
hello-app   1/1     Running   0          32s
```
### 4. Describe POD
```bash
$ oc describe pod hello-app
```
### 5. To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
Hello Openshift
```

### 6. Delete Pod
```bash
$ oc delete -f single-pod.yml
pod "hello-app" deleted
```
## Deploy single pod on Openshift/k8s using oc run

### 1. login to cluster
```bash
# Use Katacode playgroud
# https://www.katacoda.com/openshift/courses/playgrounds/openshift311 
$ oc login -u developer -p developer  2886795277-8443-host18nc.environments.katacoda.com
```

### 2. Create new project single-pod
```bash
$ oc new-project single-pod
```

### 3. Create nginx pod using oc run command
```bash
$ oc run hello --image=nginx --restart=Never
```
### 4. Check nginx POD created
```bash
$ oc get pod
NAME    READY   STATUS              RESTARTS   AGE
nginx   0/1     ContainerCreating   0          4s

$ oc get pod  
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          7s
```
### 5. Describe POD
```bash
$ oc describe pod hello-app
```
### 6. To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
Nginx Html page
```

### 7. Delete Pod
```bash
$ oc delete pod nginx
pod "nginx" deleted
```

## Deploy single pod on Openshift/k8s using Manifest

### 1. Create new project single-pod
```bash
$ oc new-project single-pod
```
### 2. Create pod using manifest file 
```bash
# generate pod menifest 
$ oc run hello-app --image=openshift/hello-openshift --restart=Never --dry-run -o yaml > single-pod.yaml

# create pod
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
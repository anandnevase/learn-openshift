## Deploy LoadBalancer Service on Openshift/k8s

### Create new project load-balance
```bash
$ oc new-project load-balance 
```
### Create pod and service
```
$ oc create -f .
pod/hello-pod created
service/hello-load-balance created
```
### Get all Object
```
$ oc get all
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-pod   1/1     Running   0          23s

NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)          AGE
service/hello-load-balance   LoadBalancer   172.30.101.122   172.29.92.247,172.29.92.247   8080:31747/TCP   23s
```
### Create Route
```
$ oc expose service hello-load-balance                                                                              route.route.openshift.io/hello-load-balance exposed
```
### Get get Route
```
$ oc get routes
NAME                 HOST/PORT                                                                         PATH   SERVICES             PORT   TERMINATION   WILDCARD
hello-load-balance   hello-load-balance-load-balance.2886795282-80-kitek03.environments.katacoda.com          hello-load-balance   8080                 None
```

### Access app using route url
```
$ curl hello-load-balance-load-balance.2886795282-80-kitek03.environments.katacoda.com
Hello OpenShift!
```

### Describe Route
```
$ oc describe route   
Name:                   hello-load-balance
Namespace:              load-balance
Created:                Less than a second ago
Labels:                 <none>
Annotations:            openshift.io/host.generated=true
Requested Host:         hello-load-balance-load-balance.2886795282-80-kitek03.environments.katacoda.com
                          exposed on router router less than a second ago
Path:                   <none>
TLS Termination:        <none>
Insecure Policy:        <none>
Endpoint Port:          8080

Service:        hello-load-balance
Weight:         100 (100%)
Endpoints:      10.128.0.29:8080
```
## Deploy LoadBalancer Service on Openshift/k8s

### Create new project node-prot
```bash
$ oc new-project node-port  
```
### Create pod and service
```
$ oc create -f .\app.yml
pod/hello-pod created
service/hello-nodeport created
```
### Get all object
```
$ oc get all 
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-pod   1/1     Running   0          42s

NAME                     TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/hello-nodeport   NodePort   172.30.92.114   <none>        9090:32402/TCP   42s
```

### Access application using nodeIP and port (32402 port create by cluster in previous command)
```
$ curl https://2886795282-32402-kitek03.environments.katacoda.com
Hello OpenShift!
```
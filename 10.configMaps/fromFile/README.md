## Deploy Pod using config-map-from-file on Openshift/k8s

### 1. Create new project config-map-from-file
```bash
$ oc new-project config-map-from-file
Now using project "config-map-from-file" on server "https://2886795320-8443-cykoria05.environments.katacoda.com:443".
```

### 2. Create new project config-map from file
```bash
$ oc create configmap color-config-map-file --from-file=testfile.txt
configmap/color-config-map-file created
```

### 3. Get configMap config-map-from-file
```bash
$ oc get configmap
NAME                    DATA   AGE
color-config-map-file   1      16s
```

### 4. Describe config-map-from-file
```bash
$ oc describe configmap color-config-map-file
Name:         color-config-map-file
Namespace:    config-map-from-file
Labels:       <none>
Annotations:  <none>

Data
====
testfile.txt:
----
Hello  - ConfigMap from File
Events:  <none>
```

### 5. Create POD
```bash
$ oc create -f pod.yml
pod/color-app created
```

### 6. Get POD
```bash
$ oc get pods
NAME        READY   STATUS    RESTARTS   AGE
color-app   1/1     Running   0          8s
```

### 7. Describe POD
```bash
$ oc describe pod color-app
Name:         color-app
Namespace:    config-map-from-file
Priority:     0
Node:         master/172.17.0.12
Start Time:   Thu, 07 May 2020 08:38:17 +0530
Labels:       app=color-app
Annotations:  openshift.io/scc: anyuid
Status:       Running
IP:           10.128.0.25
IPs:          <none>
Containers:
  color-app:
    Container ID:   docker://25090a196c1ad94cdb640d5a2574fc6cb18bf7048f2e471fafb0517074ad6f7c
    Image:          anandnevase/color-app
    Image ID:       docker-pullable://docker.io/anandnevase/color-app@sha256:2e47fba350492f8d3c2417190cfcb4f9cac4b0e1733eafdd98d67a9ae52fe3cb
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 07 May 2020 08:38:22 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /data from config (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-x8n26 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      color-config-map-file
    Optional:  false
  default-token-x8n26:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-x8n26
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  node-role.kubernetes.io/compute=true
Tolerations:     <none>
Events:
  Type    Reason     Age        From               Message
  ----    ------     ----       ----               -------
  Normal  Scheduled  <invalid>  default-scheduler  Successfully assigned config-map-from-file/color-app to master
  Normal  Pulling    <invalid>  kubelet, master    pulling image "anandnevase/color-app"
  Normal  Pulled     <invalid>  kubelet, master    Successfully pulled image "anandnevase/color-app"
  Normal  Created    <invalid>  kubelet, master    Created container
  Normal  Started    <invalid>  kubelet, master    Started container
```

### 8. create service
```bash
$ oc expose pod/color-app
service/color-app exposed
```
### 9. Create Route
```bash
  $ oc expose svc color-app
route.route.openshift.io/color-app exposed
```

### 10. Get route
```bash
$ oc get route
NAME        HOST/PORT                                                                         PATH   SERVICES    PORT   TERMINATION   WILDCARD
color-app   color-app-config-map-from-file.2886795276-80-host18nc.environments.katacoda.com          color-app   8080                 None
```

### 11. Access route url browser
Access following url, You will observer you can able to see file which is store in configMap
http://color-app-config-map-from-file.2886795276-80-host18nc.environments.katacoda.com/read_file
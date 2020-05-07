## Deploy Pod using config-map-from-literals on Openshift/k8s

### 1. Create new project config-map-from-literals
```bash
$ oc new-project config-map-from-literals
Now using project "config-map-from-literals" on server "https://2886795320-8443-cykoria05.environments.katacoda.com:443".
```

### 2. create config-map from literals
```bash
$ oc apply -f pod.yml
error: error parsing pod.yml: error converting YAML to JSON: yaml: line 9: mapping values are not allowed in this context

$ oc create configmap color-config-map --from-literal=APP_COLOR=red
configmap/color-config-map created

$ oc get configmap
NAME               DATA   AGE
color-config-map   1      5s

$ oc describe configmap color-config-map
Name:         color-config-map
Namespace:    config-map-from-literals
Labels:       <none>
Annotations:  <none>

Data
====
APP_COLOR:
----
red
Events:  <none>
```

### 3. create POD
```bash
$ oc apply -f pod.yml
pod/color-app created
```

### 4. create service
```bash
$ oc expose pod/color-app
service/color-app exposed
```

### 5. create route
```bash
$ oc expose service/color-app
route.route.openshift.io/color-app exposed
```

### 6. Get route URL
```bash
$ oc get route
NAME        HOST/PORT                                                                              PATH   SERVICES    PORT   TERMINATION   WILDCARD
color-app   color-app-config-map-from-literals.2886795320-80-cykoria05.environments.katacoda.com          color-app   8080                 None
```

###  7. Accees application
- using URL : color-app-config-map-from-literals.2886795320-80-cykoria05.environments.katacoda 
  HTML RED color Page, because in config map value of APP_COLOR is RED





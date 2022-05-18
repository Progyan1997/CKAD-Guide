# Deployment

Provides a declarative resource to manage Pods and Replicas, instead of imperatively operating on them.

## Setup a Namespace

```sh
$ kubectl create ns app-ns
namespace/app-ns created
```

## Create Resouces

```sh
$ kubectl create -f 1.5-Deployment.yml -n app-ns
deployment.apps/app-deployment created
service/app-service created
```

## Check Resouces

### Deployment

```sh
$ kubectl get deploy -n app-ns
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
app-deployment   2/2     2            2           45s
```

### Service

```sh
$ kubectl get svc -n app-ns
NAME          TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
app-service   NodePort   10.104.99.199   <none>        80:31793/TCP   12s
```

### Pods

```sh
$ kubectl get po -n app-ns
NAME                              READY   STATUS    RESTARTS   AGE
app-deployment-598fbd58c8-pmtdp   1/1     Running   0          34s
app-deployment-598fbd58c8-srl4f   1/1     Running   0          34s
```

## Check Network Connection

```sh
$ kubectl describe svc -n app-ns app-service
Name:                     app-service
Namespace:                app-ns
Labels:                   <none>
Annotations:              <none>
Selector:                 app=app-1.5
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.104.99.199
IPs:                      10.104.99.199
LoadBalancer Ingress:     localhost
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  31793/TCP
Endpoints:                10.1.0.31:80,10.1.0.32:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

## All at once

```sh
$ curl localhost:31793
```

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

## Bonus: Scale Down Replicas

### Declare Replica Count to be 1

```sh
$ kubectl scale --replicas=1 -n app-ns deployment/app-deployment
deployment.apps/app-deployment scaled
```

### Validate Pods

```sh
$ kubectl get po -n app-ns
NAME                              READY   STATUS    RESTARTS   AGE
app-deployment-598fbd58c8-pmtdp   1/1     Running   0          15m
```

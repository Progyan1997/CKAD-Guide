# Namespace

Namespace provides a way to isolate resources based on their application and access control.

## Create a Namespace

```sh
$ kubectl create ns app-ns
```

## Create Resources in a Namespace

```sh
$ kubectl create -f 1.4-Namespace/1.4-Namespace.yml -n app-ns
```

## View Resources in a Namespace

### Pod

```sh
$ kubectl get pods -n app-ns
```

### Service

```sh
$ kubectl get svc -n app-ns
```

## Delete a Namespace

```sh
$ kubectl delete ns app-ns
```

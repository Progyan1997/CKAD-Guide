# Quality of Services

A metadata in Pod resource that implies how confident Kubernetes is about stability and performance of the application within it.

## Burstable
### Commands

- Create Pod in our Kubernetes Cluster by executing the following:

  ```sh
  $ kubectl create -f 1.2-Burstable.yml
  ```

- Check if the Containers in the Pod is up and running:

  ```sh
  $ kubectl get pods
  ```

- To get more details on the Pod:

  ```sh
  $ kubectl describe pod app-1.2-burstable
  ```

### Note

On response of `describe` command you will see the following line:

```
QoS Class:                   Burstable
```

This is because we did not specify how much CPU resource is needed for this Pod despite mentioning a memory limit and hence Kubernetes pro-actively decides what is best for it and can evict if required.

## Guaranteed
### Commands

- Create Pod in our Kubernetes Cluster by executing the following:

  ```sh
  $ kubectl create -f 1.2-Guaranteed.yml
  ```

- Check if the Containers in the Pod is up and running:

  ```sh
  $ kubectl get pods
  ```

- To get more details on the Pod:

  ```sh
  $ kubectl describe pod app-1.2-guaranteed
  ```

### Note

On response of `describe` command you will see the following line:

```
QoS Class:                   Guaranteed
```

This is because we did specify how much CPU and Memory resource is needed for this Pod and hence Kubernetes is convicted on it's resource allocation.

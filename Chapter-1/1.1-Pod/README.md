# Pod

## Commands

- Create Pod in our Kubernetes Cluster by executing the following:

  ```sh
  $ kubectl create -f 1.1-Pod.yml
  ```

- Check if the Containers in the Pod is up and running:

  ```sh
  $ kubectl get pods
  ```

- To get more details on the Pod:

  ```sh
  $ kubectl describe pod app-1.1
  ```

## Interesting Note

On response of `describe` command you will see the following line:

```
QoS Class:                   BestEffort
```

This is because we did not specify how much resource is needed for this Pod and hence Kubernetes pro-actively decides what is best for it.
More on this in following sections.

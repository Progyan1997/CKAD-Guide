# Service

Pod in Kubernetes is a non-permanent resource, i.e., it is rapidly created and destroyed to match desirable state of the application. But it could be case for an application, there are multiple pods transfering data amongst them. To maintain consistency for this communication we need Static IP to route those network.

## Cluster IP

Cluster IP is the default way of creating a service. This creates a Static IP entry into Kubernetes DNS and is accessible from any pod living in the same Cluster. The service needs to be provided with valid selector to get endpoints that can handle those requests.

  - Run the following command to create respective Pod and Service:
  ```sh
  $ kubectl create -f 1.3-ClusterIP.yml
  ```

  - Validate if they have been created:
  ```sh
  $ kubectl get pods
  NAME      READY   STATUS    RESTARTS   AGE
  app-1.3   1/1     Running   0          21s

  $ kubectl get services
  NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
  ip-service   ClusterIP   10.107.178.137   <none>        80/TCP    3s
  kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP   3d13h
  ```

  - SSH into a Pod and see if the Cluster IP is accessible from it:
  ```sh
  $ kubectl exec app-1.3 -- curl 10.107.178.137
  ```

  - This should render default HTML page of Nginx into the terminal.
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

## Node Port

Cluster IP might not always solve the problem. Sometime it might be required to access endpoints of a Pod from completely outside of a Cluster. This is when Node Port comes in rescue.

  - Run the following command to create respective Pod and Service:
  ```sh
  $ kubectl create -f 1.3-NodePort.yml
  ```

  - Validate if they have been created:
  ```sh
  $ kubectl get pods
  NAME      READY   STATUS    RESTARTS   AGE
  app-1.3   1/1     Running   0          16s

  $ kubectl get services
  NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
  kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP        3d13h
  node-service   NodePort    10.108.179.34   <none>        80:31945/TCP   51s
  ```

  - Curl loopback IP on given Port to see if the Pod is accessible:
  ```sh
  $ curl localhost:31945
  ```

  - This should render default HTML page of Nginx into the terminal.
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

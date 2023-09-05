---
title: "Deploying next js application using  deployments and services in Kubernetes. 📜⚙️"
seoTitle: "Deploying nextjs app on k8s"
datePublished: Tue Sep 05 2023 04:20:08 GMT+0000 (Coordinated Universal Time)
cuid: clm5sy3gb000i0amobwadarai
slug: deploying-next-js-application-using-deployments-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693887532722/d29a76c0-5fdd-46b2-bd4a-5cf9ca71fb20.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693887596815/3c27adc3-9dfa-4f9d-8e98-0b93ac07ba07.png
tags: deployment, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## 📍 Introduction:

Hello readers, in today's blog we will be working with services, we will learn about different types of services that Kubernetes has to offer like ClusterIP, NodePort and Load Balancer.

## ✔️ Cluster IP

A Cluster IP creates a cluster of nodes that match the given selector and provides them with a virtual IP address through which the pods can communicate with each other even if they are on different nodes.

The virtual IP created is exposed and is accessible only within a cluster. And is an excellent way to allow communication between pods running our microservices.

When a cluster IP is created it is assigned a static IP address is assigned to it. And when traffic is sent to this static IP it is re-routed to the selected pods. It always load-balances the requests.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693708316220/198e8c19-3ccf-411c-b1eb-674edd4dcc58.png align="center")

### 🔸 Manifest file for creating cluster IP

```yaml
apiVersion: v1
kind: Service
metadata:
  name: cluster-ip-service
spec:
  selector:
    app: todo-app # selector for pods
  type: ClusterIP
  ports:
    - protocol: TCP
      port: 8080 # port on which the service will listen
      targetPort: 3000 # port on the pods where the traffic will be redirected to
```

## ✔️ Node Port

Expose your application to the outside world using this service. With the NodePort service, we designate the port on the machine to which our service will listen. When traffic is received on that port, the service forwards it to the pods based on the selector.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693714173559/dbfb8b0f-038e-4683-b7f4-2d76e7fc1f89.png align="center")

This uses a cluster IP-like service and exposes a port on it to accept traffic when traffic is received on the port of service it is redirected to the pods according to the provided selector.

### 🔸 Manifest file for creating node port

```yaml
apiVersion: v1
kind: Service
metadata:
  name: cluster-ip-service
spec:
  selector:
    app: todo-app # selector for pods
  type: NodePort
  ports:
    - protocol: TCP
      port: 8080 # port on which the service will listen
      targetPort: 3000 # port on the pods where the traffic will be redirected to
      nodePort: 32000 # port on which the worker node will listen for requests
```

## ✔️ Load Balancer

A load balancer service is another way to expose your application to the outside world. This works with the help of a cloud-controller-manager because it interacts with the underlying cloud provider like AWS, GCP or Azure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693714384356/e18b07bf-6dd9-4c8d-b859-4e8a1aef05f0.png align="center")

When we create a load balancer service k8s will:

* detect the computing platform on which the cluster is running.
    
* creates a load balancer in the infrastructure of the cloud provider.
    
* load balancer will have its unique IP which users can use to access the application.
    

## ✔️ Using a service object to serve your application

Create a deployment file for the application and database

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: discord-clone-db
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:latest
          ports:
            - containerPort: 3306
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: password
            - name: MYSQL_DATABASE
              value: mydb
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: discord-clone-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: discord-clone
  template:
    metadata:
      labels:
        app: discord-clone
    spec:
      containers:
        - name: web-app
          image: yash6370/discord-clone
          ports:
            - containerPort: 3000
          env:
            - name: NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY
              value: ""
            - name: CLERK_SECRET_KEY
              value: ""
            - name: NEXT_PUBLIC_CLERK_SIGN_IN_URL
              value: "/sign-in"
            - name: NEXT_PUBLIC_CLERK_SIGN_UP_URL
              value: "/sign-up"
            - name: NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL
              value: "/"
            - name: NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL
              value: "/"
            - name: DATABASE_URL
              value: "mysql://root:password@10.105.152.220:3306/mydb"
            - name: UPLOADTHING_SECRET
              value: ""
            - name: UPLOADTHING_APP_ID
              value: ""
            - name: LIVEKIT_API_KEY
              value: ""
            - name: LIVEKIT_API_SECRET
              value: ""
            - name: NEXT_PUBLIC_LIVEKIT_URL
              value: ""
            - name: NEXT_PUBLIC_SITE_URL
              value: "http://discord-clone"
```

Create a service manifest file for web application and database.

```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
  namespace: discord-clone
spec:
  type: ClusterIP
  selector:
    app: mysql
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
---
apiVersion: v1
kind: Service
metadata:
  name: discord-clone-service
  namespace: discord-clone
spec:
  type: NodePort
  selector:
    app: discord-clone
  ports:
    - protocol: TCP
      port: 3000
      targetPort: 3000
      nodePort: 32000
```

## 📍 Conclusion

In conclusion, Kubernetes offers various service types like ClusterIP, NodePort, and Load Balancer to efficiently manage and expose your applications. ClusterIP is ideal for internal communication, while NodePort and Load Balancer services are suitable for exposing applications to external users. By understanding and utilizing these services, you can enhance the communication, scalability, and accessibility of your applications within a Kubernetes cluster.
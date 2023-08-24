---
title: "⚙️Deploying application using the deployment object in k8s.📦📦"
seoTitle: "⚙️Deploying application using the deployment object in k8s.📦📦"
datePublished: Thu Aug 24 2023 17:19:17 GMT+0000 (Coordinated Universal Time)
cuid: cllpfhvm4000009igectw4d10
slug: deploying-application-using-the-deployment-object-in-k8s
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692897487840/e7d6cedf-d98c-43db-88b6-936ae867ef83.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692897539067/822d7ba4-a7fe-467d-a41e-c7feeb560030.png
tags: kubernetes, devops, 90daysofdevops, trainwithshubham, deployment-objects

---

## 📍 Introduction:

Hey there, fantastic readers! 🎉 Get ready for an exhilarating adventure in today's blog! We're diving deep into the deployment objects, the ultimate tool for running our applications in production environments within pods! 🚀 And guess what? They make sure our apps run flawlessly 24/7! How awesome is that? 😃

## ✔️ What is a deployment object? 🤔

In Kubernetes, a Deployment is a high-level resource that offers declarative updates for applications. It is primarily used to manage the deployment and scaling of containerized applications. Under the hood, the deployment creates and manages Replica Sets. A Replica Set is responsible for ensuring that a specified number of replica Pods are running at any given time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692847074721/19741979-6733-4219-97f5-d276ebb8a23c.png align="center")

The main objective of a Deployment is to ensure that the desired number of instances for a specific application are running and that any changes to the application's configuration or code are implemented seamlessly. The deployment controller is responsible for making all these changes happen.

### 🔸 Features of Deployment:

* **Production deployment:** The deployment object is used to deploy applications in production environments where multiple pods must run simultaneously to ensure high availability.
    
* **Seamless Updates:** Deployment supports two types of update strategies: recreate and rolling update, with the latter being more widely used. With the rolling update option, you can even specify the number of pods to take down for an update. This ensures that our application is deployed incrementally, resulting in zero downtime.
    
* **Rollbacks:** In the event of errors or issues with a new version, Deployments enable you to effortlessly revert to a previously functioning version, ensuring your application's stability.
    

## ✔️ Manifest file for deployment 📜

Let's understand the different fields in a manifest file for deployment.

1. `apiVersion:` Specifies the API version being used for the deployment object.
    
2. `kind:` declares the type of object, Deployment in our case.
    
3. `metadata:` specifies metadata about the deployment. This has the following fields name, namespace, labels, and annotations in key-value pair format
    
4. `spec:` In this field, we specify the desired specification of the deployment object. It has the following fields:
    
    * `replicas:` the desired number of replica pods to maintain at all times.
        
    * `selector:` Using this field we can specify the labels to select the pod for deployment.
        
        * `matchLabels:` we can select a group of objects that have certain labels applied to them to create deployment
            
    * `template:` With this field, we can describe the template for creating replica pods. Within the template key, we specify the data for the creation of pods.
        
        * `metadata:` metadata for the pod template.
            
            * `labels:` labels for Pods created from this template. Should be similar to what is defined in the selector.
                
        * `spec:` Specification for the Pods.
            
            * `containers:` defining the created containers
                
                * `name:` Name of the container.
                    
                * `image:` Container image to run.
                    
                * `ports:` Array of ports to expose on the container.
                    
5. `strategy:` specifies the update strategy for the deployment.
    
    * `type:` type of update strategy (i.e rolling update or recreate - which is default).
        
    * `rolling update:` Configuration for rolling update.
        
        * `maxUnavailable:` The maximum number of unavailable Pods during an update.
            
        * `maxSurge:` The maximum number of new Pods that can be created during an update.
            

With these fields in mind let's create a deployment object now.

## ✔️ Let's deploy an application using deployment object ⚙️

Take a look at the following manifest file for deployment, and copy the following contents into a deployment.yaml file in your system.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app
  labels:
    app: todo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: todo
  template:
    metadata:
      labels:
        app: todo
    spec:
      containers:
      - name: todo
        image: rishikeshops/todo-app
        ports:
        - containerPort: 3000
```

Now let's create a service object with the type NodePort so that we can access the services of the port. Copy the following contents into a file named services.yaml.

```yaml
apiVersion: v1
kind: Service
metadata:
    name: todo-app-service
spec:
    selector:
        app: todo
    type: NodePort
    ports:
        - protocol: TCP
          port: 80
          targetPort: 3000
          nodePort: 31000      
```

Now you will have two files, i.e. deployments.yaml and services.yaml execute the following command `kubectl create -f deployment.yaml -f service.yaml`

This will create both the deployment and service within your cluster, allowing you to access the application using the public IP address of your worker node. Since we specified 31000 in the nodePort field, you can the application through that port.

Here is the deployed application:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692896910800/6320da28-b5d4-47d3-89aa-eb674fbec708.png align="center")

## 📍 Conclusion:

Upon reaching this stage, you should have gained a comprehensive understanding of the deployment object. Should you have any questions or concerns, please do not hesitate to leave a comment.

If you found this article informative and valuable, kindly consider expressing your appreciation by liking it. In upcoming blog posts, I will cover various other objects, so stay tuned and keep learning.
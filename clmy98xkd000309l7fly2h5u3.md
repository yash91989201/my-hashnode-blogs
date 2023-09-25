---
title: "👨‍🏫 Understanding persistent volumes in k8s: persisting data in pods 📁"
seoTitle: "👨‍🏫 Understanding persistent volumes in k8s: persisting data in pods"
datePublished: Mon Sep 25 2023 02:14:00 GMT+0000 (Coordinated Universal Time)
cuid: clmy98xkd000309l7fly2h5u3
slug: understanding-persistent-volumes-in-k8s-persisting-data-in-pods
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695607693733/842ded8b-6dc3-49bb-9e0e-e7090d6f3267.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695607771107/27a654c4-f52e-4fbc-b410-425c3be84eee.png
tags: kubernetes, devops, 90daysofdevops, kubernetes-persistent-volumes, trainwithshubham

---

## 📍 Introduction

Whenever we create a deployment, it's important to remember that pods are ephemeral, meaning that once a pod is destroyed, the data within it is lost. While this doesn't pose a problem for stateless applications, it can be a serious issue for stateful ones.

In today's blog, we'll explore how to persist data in pods using persistent volumes and persistent volume claims. Let's get started.

## ✔️ Volumes in k8s

Volumes in k8s are attached to pods and have a lifecycle same as the pod, it is attached to pods and shared among containers, also the data in a volume is preserved between container restarts.

The storage medium and its contents are determined by the volume type.

## ✔️ Types of volumes in k8s

This decides the properties of the directory like size, content etc. Examples of volume types are:

* node-local type which are empty dir and host path
    
* file sharing type such as nfs
    
* cloud-provider-specific types such as AWS EBS or EFS.
    

### 🔸 Empty dir

* This type of volume is known as an empty directory because its contents are removed whenever it is deleted.
    
* In this case, the volume is created and connected to the pod, making it accessible for a container to utilize. Consequently, if a container restarts, the data remains preserved.
    
* If a pod is deleted, the volume is also removed. Upon the pod's restart, a new, empty volume is created.
    

### 🔸 Host path

* A host path volume differs from an empty directory volume. When a host path volume is created, it mounts a directory from the node's file system into the pod.
    
* The lifecycle of a host path volume exists independently of a pod.
    
* Even if a pod is deleted, the data within the pod remains preserved and will be accessible to the pod when it restarts.
    

## ✔️ Persistent volumes in Kubernetes

A Persistent Volume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource.

PVs are volume plugins like volumes but have a lifecycle independent of any individual Pod that uses the PV.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: <pv_name>
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: ""
  appVolume:
    volumeID: "<volume_id>"
```

## ✔️ Persistent volume claim

After creating a persistent volume to use it we first need to claim it for our applications, so that we can assign them to our pods as volumes.

To use a pv we need to claim it first using a persistent volume claim.

The PVC requests a pv with the desired specifications like size, access modes, speed etc. from k8s once a suitable pv is found it is bound to PVC.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

## ✔️ Using PVC for app deployments

Now let's create a PVC for a deployment for an app.

1. Creating a persistent volume
    
    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-todo-app
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      hostPath:
        path: "/tmp/data"
    ```
    
2. Creating a persistent volume claim
    
    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-todo-app
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 500Mi
    ```
    
3. Using PVC in a deployment
    
    ```yaml
    piVersion: apps/v1
    kind: Deployment
    metadata:
      name: todo-app-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: todo-app
      template:
        metadata:
          labels:
            app: todo-app
        spec:
          containers:
            - name: todo-app
              image: rishikeshops/todo-app
              ports:
                - containerPort: 8000
              volumeMounts:
                - name: todo-app-data
                  mountPath: /app
          volumes:
            - name: todo-app-data
              persistentVolumeClaim:
                claimName: pvc-todo-app
    ```
    

Now apply the following spec files one by one to create a deployment with persistent volumes.

## 📍 Conclusion

In conclusion, k8s persistent volumes provide a robust solution for preserving data between pod restarts. By understanding different volume types and their lifecycles, you can effectively manage your stateful applications and ensure data durability in your Kubernetes deployments.

🎉 Woohoo! I hope you discovered some amazing insights today! If this blog post was super helpful for you, don't forget to smash that like button and share your thoughts in the comments! I'm always eager to improve and make your learning experience even more fantastic! 🚀

Let's connect on LinkedIn : [linkedin.com/in/yashraj-jaiswal-91989201s/](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/)
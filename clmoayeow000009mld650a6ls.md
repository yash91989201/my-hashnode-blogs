---
title: "🛡️ Mastering Config maps and Secrets in Kubernetes🔒🔑"
seoTitle: "Mastering Config maps and Secrets in Kubernetes"
datePublished: Mon Sep 18 2023 03:04:07 GMT+0000 (Coordinated Universal Time)
cuid: clmoayeow000009mld650a6ls
slug: mastering-config-maps-and-secrets-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695006186270/bbad0817-bd6e-465d-be78-b3ac01c97747.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695006230872/ec1e5d64-cf6f-4173-8cc9-47ee0a45b640.png
tags: kubernetes, devops, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hello readers, in today's blog we will be learning about config maps and secretes in Kubernetes and how to use them when deploying pods.

## ✔️ Config Maps

Config maps are useful for storing and sharing non-sensitive, unencrypted configuration information required by our application to run.

We can create config maps in two ways,

* Create and attach a volume to our pod, from which our application will get the configuration file.
    
* Define the configurations as environment variables, from which the data will be read directly and made available to the container during runtime.
    

By abstracting the configurations, we can utilize our applications in a modular manner across various environments, such as development, UAT, or production.

### 🔸 Creating a config map

Here is a syntax to create a config map `kubectl create configmap <map-name> <data-source>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695005288488/fbf0c09d-e29b-443c-84ae-1041dadc142a.png align="center")

## ✔️ Secrets

The secrets object in Kubernetes provides us with a mechanism to store and use sensitive information like database URLs, passwords and things like API keys safely and reliably.

The secrets object in Kubernetes works similarly to the config map; instead, it is used when there is a requirement to store sensitive information that should not be seen by anyone, like a database URL, user, or password of any kind.

When a secret is created, we cannot see its content. And just like a config map, the contents of a secret are injected into the container's environment.

### 🔸 Creating a secret object

```bash
kubectl create secret opaque db-user-pass \
  --from-file=./username.txt \
  --from-file=./password.txt
```

## ✔️ Using config maps and sections in a deployment

In a pod we can use the config map and secrets as follows:

```yaml
# using config map
apiVersion: v1
kind: Pod
metadata:
  name: myenvconfig
spec:
  containers:
  - name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; do echo Technical-Guftgu; sleep 5 ; done"]
    env:
    - name: MYENV         # env name in which value of the key is stored
      valueFrom:
        configMapKeyRef:
          name: mymap      # name of the config created
          key: .env 
     volumeMounts:
      - name: testsecret
        mountPath: "/tmp/mysecrets"   # the secret files will be mounted as ReadOnly by default here
 volumes:
 - name: testsecret
     secret:
       secretName: mysecret
```

## 📍 Conclusion

In conclusion, mastering config maps and secrets in Kubernetes is essential for managing both non-sensitive and sensitive information within your applications. By effectively utilizing these tools, you can create a more modular and secure environment for your applications across various stages of development.
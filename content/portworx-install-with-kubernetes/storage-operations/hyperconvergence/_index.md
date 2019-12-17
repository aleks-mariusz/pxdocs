---
title: Run Hyper Converged
weight: 2
keywords: portworx, container, Kubernetes, storage, Docker, k8s, pv, persistent disk
description: Learn how to run your applications hyperconverged with their data
noicon: true
series: k8s-storage
---

### Hyper-convergence {#hyper-convergence}

When a pod runs on the same host as its volume, it is known as convergence or hyper-convergence. Because this configuration reduces the network overhead of an application, performance is typically better.

### Using scheduler convergence {#using-scheduler-convergence}

The recommended method to run your pods hyperconverged is to use [Stork](/portworx-install-with-kubernetes/storage-operations/stork).

Once you have installed Stork, all you need to do is add `schedulerName: stork` in your application specs. Stork will then ensure that the nodes with data for a volume get prioritized when pods are being scheduled.

For example, this is how you would specify the scheduler name in a MySQL deployment:

```text
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  selector:
    matchLabels:
      app: mysql
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  replicas: 1
  template:
    metadata:
      labels:
        app: mysql
        version: "1"
    spec:
      schedulerName: stork
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: password
        ports:
        - containerPort: 3306
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-data
```


### Initializer (Experimental feature in Stork v1.1)

If you are not able to update the schedulerName for you applications to use
stork, you can enable the app-initializer feature. This uses the Kubernetes
[AdmissionController Initializer](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#initializers)
feature to automatically update the scheduler to stork if your application
(deployment or statefulset) is using volumes backed by Portworx.

To enable the Initializer you need to:
* [Enable the Intializer feature in your Kubernetes cluster](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#enable-initializers-alpha-feature) since it is an alpha feature in Kubernetes.
* Add "--app-initializer=true" option in the stork deployment
* Add the [stork-initializer spec](https://raw.githubusercontent.com/libopenstorage/stork/master/specs/stork-initializer.yaml) to your Kubernetes cluster using `kubectl apply -f stork-initializer.yaml`

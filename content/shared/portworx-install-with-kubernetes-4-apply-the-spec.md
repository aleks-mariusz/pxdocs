---
title: Shared content for install Portworx with Kubernetes - apply the specs
hidden: true
description: Shared content for install Portworx with Kubernetes - apply the specs
keywords: Install, apply the specs, kubernetes, k8s
---

### Apply the specs

Apply the generated specs to your cluster.

```text
kubectl apply -f px-spec.yaml
```

#####  Monitor the Portworx pods

Wait till all Portworx pods show as ready in the below output:

```text
kubectl get pods -o wide -n kube-system -l name=portworx
```

#####  Monitor Portworx cluster status

```text
PX_POD=$(kubectl get pods -l name=portworx -n kube-system -o jsonpath='{.items[0].metadata.name}')
kubectl exec $PX_POD -n kube-system -- /opt/pwx/bin/pxctl status
```

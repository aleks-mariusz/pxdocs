---
title: 2. Deploy Portworx on AKS
keywords: portworx, container, Kubernetes, storage, Docker, k8s, pv, persistent disk, aks, Azure
description: Learn about applying the spec with Portwork on Azure Kubernetes Service.
weight: 2
---

## Install

### Create a secret to give Portworx access to Azure APIs

Update `<AZURE_TENANT_ID>`, `<AZURE_CLIENT_ID>` and `<AZURE_CLIENT_SECRET>` in below command and create a secret called _px-azure_.

```text
kubectl create secret generic -n kube-system px-azure --from-literal=AZURE_TENANT_ID=<AZURE_TENANT_ID> \
                                                      --from-literal=AZURE_CLIENT_ID=<AZURE_CLIENT_ID> \
                                                      --from-literal=AZURE_CLIENT_SECRET=<AZURE_CLIENT_SECRET>
```
```output
secret/px-azure created
```

When you generate the spec in the next step, the Portworx pod will fetch the Azure environment variables from this secret.

{{% content "shared/portworx-install-with-kubernetes-shared-1-generate-the-spec-footer.md" %}}

{{% content "shared/portworx-install-with-kubernetes-4-apply-the-spec.md" %}}

{{% content "shared/portworx-install-with-kubernetes-post-install.md" %}}

---
title: 2. Deploy Portworx
keywords: portworx, container, kubernetes, storage, docker, k8s, pv, persistent disk, openshift
description: Find out how to apply the spec for Portworx within a OpenShift cluster and have Portworx provide highly available volumes to any application deployed via Kubernetes.
weight: 2
---

{{<info>}}
If you are generating the DaemonSet spec via the GUI wizard, select **OpenShift** under the **Customize** page.
{{</info>}}

{{% content "portworx-install-with-kubernetes/shared/1-generate-the-spec-footer.md" %}}

{{% content "portworx-install-with-kubernetes/on-premise/openshift/shared/apply-the-spec-oc.md" %}}

{{% content "portworx-install-with-kubernetes/shared/post-install.md" %}}

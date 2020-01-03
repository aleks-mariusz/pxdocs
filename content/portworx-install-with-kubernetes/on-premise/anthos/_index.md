---
title: Portworx on Anthos
linkTitle: Anthos
weight: 4
hidden: true
keywords: portworx, container, kubernetes, storage, docker, k8s, pv, persistent disk, anthos
description: How to install Portworx on Anthos
---

This topic explains how to install Portworx with Kubernetes on Anthos. Follow the steps in this topic in order.

## Architecture

{{% content "shared/cloud-references-auto-disk-provisioning-vsphere-vsphere-shared-arch.md" %}}

## Installation

{{<info>}}Run these steps from the anthos admin station or any other machine which has kubectl access to your cluster.{{</info>}}

{{% content "shared/cloud-references-auto-disk-provisioning-vsphere-vsphere-px-install.md" %}}

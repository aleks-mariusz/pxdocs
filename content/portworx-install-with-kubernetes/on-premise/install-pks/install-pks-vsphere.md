---
layout: page
title: "Portworx install on PKS on vSphere"
keywords: portworx, container, Kubernetes, storage, Docker, k8s, flexvol, pv, persistent disk
meta-description: "Find out how to install Portworx in a PKS Kubernetes cluster on vSphere and have Portworx provide highly available volumes to any application deployed via Kubernetes."
hidden: true
disableprevnext: true
---

## Pre-requisites

* vSphere 6.5u1 or above.
* PKS 1.1 or above.
* Shared ESXi datastore

## Installing Portworx

Based on your ESXi datastore type, proceed to one of the following pages.

If you have **shared** datastores, proceed to [Portworx install on PKS on vSphere using shared datastores](/portworx-install-with-kubernetes/on-premise/install-pks/install-pks-vsphere-shared).

<!-- If you have **local** datastores, proceed to [Portworx install on PKS on vSphere using local datastores](/portworx-install-with-kubernetes/on-premise/install-pks/install-pks-vsphere-local). -->
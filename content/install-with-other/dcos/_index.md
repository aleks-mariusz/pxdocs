---
title: DCOS
description: Documentation on using Portworx in Mesosphere DC/OS environments
keywords: portworx, PX-Developer, container, Mesos, Mesosphere, Marathon, storage, DCOS
weight: 1
hideSections: true
series: px-other
---

[Mesosphere DC/OS](https://d2iq.com/solutions/mesosphere) makes it easy to build and run modern distributed applications in production at scale, by pooling resources across an entire datacenter or
cloud.

While the DC/OS platform works great for stateless applications, many enterprises who have tried to use DC/OS for stateful applications at scale have stumbled when it comes to using the platform for services like databases, queues and key-value stores.

Portworx, which scales up to 1000 nodes per cluster and is used in production by DC/OS users like GE Digital, solves the operational and data management problems enterprises encounter when running stateful applications on DC/OS.

Unlike the default DC/OS volume driver, Portworx lets you:

* dynamically create volumes for tasks at run time, no more submitting tickets for storage provisioning
* dynamically and automatically resize volumes based on demand while task is running
* run tasks on the same hosts that your data is located on for optimum performance
* avoid pinning services to particular hosts, reducing the value of automated scheduling
* avoid fragile block device mount/unmount operations that block or delay failover operations
* encrypt data at rest and in flight at the container level

Read on for how to use Portworx to provide [persistent storage for Mesosphere DC/OS and marathon](https://portworx.com/use-case/persistent-storage-dcos/) and use it with [DC/OS Commons frameworks](https://docs.d2iq.com/mesosphere/dcos/services/) for some of the most popular stateful services.

## Installation

For documentation for installing Portworx on DCOS, continue below
{{< widelink url="/install-with-other/dcos/install" >}}Installing Portworx on DCOS
{{</widelink>}}

For documentation for installing Portworx on Kubernetes on DCOS, continue below
{{< widelink url="/install-with-other/dcos/install-dcos-k8s" >}}Install Portworx on Kubernetes on DCOS {{</widelink>}}

For documentation for installing Portworx on DCOS on Azure (ACS), continue below
{{< widelink url="/install-with-other/dcos/install-azure" >}}Install Portworx on DCOS on Azure {{</widelink>}}

## Post-installation

For documentation for installing various stateful applications on DCOS with Portworx, continue below
{{< widelink url="/install-with-other/dcos/application-installs" >}}Install Stateful applications on DCOS{{</widelink>}}

For documentation on operating and maintaining your Mesoshere/DCOS installation, continue below
{{< widelink url="/install-with-other/dcos/operate-and-maintain" >}}Operate and Maintain{{</widelink>}}

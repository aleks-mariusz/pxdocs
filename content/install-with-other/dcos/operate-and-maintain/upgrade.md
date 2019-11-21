---
title: Upgrade Portworx on DCOS (Deprecated)
keywords: portworx, container, dcos, storage, Docker, mesos
description: Updating Portworx version on your DCOS cluster is simple. Follow this guide to find out how.
hidden: true
---

{{<info>}}
This document presents the **DC/OS** method of upgrading Portworx. Please refer to the [Upgrade Portworx on Kubernetes](/portworx-install-with-kubernetes/operate-and-maintain-on-kubernetes/upgrade/) page if you are running Portworx on Kubernetes.
{{</info>}}

This guide walks through upgrading Portworx deployed on DCOS through the framework available in the DCOS catalog.

### Update the Portworx image in the framework config

The Portworx image to be used on each node is specified by the framework variable PORTWORX_IMAGE_NAME.
To upgrade to a newer version of Portworx you need to point this to the desired version.
For example, if you want to upgrade to v1.2.11 you would set this to "portworx/px-enterprise:1.2.11"

![Portworx image option](/img/dcos-px-image-option.png)

### Restart the Portworx update task

Once the image name has been updated, the service file for Portworx needs to be updated on each node and the Portworx service needs to be restarted on all the nodes to pick up the new image name. This can be done by force restarting the update-portworx plan through the dcos cli. This step will perform a rolling restart of Portworx so as not to cause an
outage:

```text
dcos portworx plan force-restart update-portworx
```

```output
"update-portworx" plan has been restarted.
```

Now, wait for the tasks to go to COMPLETE state on all the agents:

```text
dcos portworx plan status update-portworx
```

```output
update-portworx (COMPLETE)
├─ update-service (COMPLETE)
│  ├─ portworx-0:[install] (COMPLETE)
│  ├─ portworx-1:[install] (COMPLETE)
│  ├─ portworx-2:[install] (COMPLETE)
│  ├─ portworx-3:[install] (COMPLETE)
│  └─ portworx-4:[install] (COMPLETE)
└─ restart-service (COMPLETE)
   ├─ portworx-0:[restart] (COMPLETE)
   ├─ portworx-1:[restart] (COMPLETE)
   ├─ portworx-2:[restart] (COMPLETE)
   ├─ portworx-3:[restart] (COMPLETE)
   └─ portworx-4:[restart] (COMPLETE)
```

At this point your Portworx cluster should be upgraded to the specified version.

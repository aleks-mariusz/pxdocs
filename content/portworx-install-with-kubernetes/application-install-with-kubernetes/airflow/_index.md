---

title: Airflow on Kubernetes with Portworx
linkTitle: Apache Airflow
keywords: portworx, container, Kubernetes, airflow, storage, Docker, k8s, pvc
description: See how Airflow can be deployed on Kubernetes using Portworx volumes.
weight: 2
noicon: true

---

## Introduction

[Apache Airflow](https://airflow.apache.org/) is an open-source workflow management platform. It started at Airbnb in October 2014 as a solution to manage the company's increasing complex workflows. Using Airflow allows companies to programmatically author and schedule their workflows and monitor them via the built-in Airflow user interface.

In this reference architecture document, we will explore setting up Airflow in its own namespace, to leverage dynamically provisioning storage that can be consumed by different Airflow designed workflows, providing a reliable persistent storage facility.

## Architecture

Airflow consists of a two parts - web UI component, and a scheduler.  Although these two systems are stateless, they however heavily rely on having a stateful data-tier to store workflow metadata and history of executions.  This usually takes the form of a PostgreSQL or MySQL database.  Portworx easily handles the persistent storage requirements for this database.

Additionally, because the two components can scale independently, Portworx also provides the ability to have multiple replicas of any scaled components access another PersistentVolume that holds the workflow definitions (DAGs) and log files of executions (DAG-Runs).  These two volumes have accessMode as ReadWriteMany.

And with the [recent progress of Airflow development embracing the flexibility of the scheduler functionality of Kubernetes](https://kubernetes.io/blog/2018/06/28/airflow-on-kubernetes-part-1-a-different-kind-of-operator/), we can further benefit from Portworx as dynamically provisioning volumes for each dag-run with an on-demand basis.  We will conclude with an example workflow that does exactly this, to demonstrate how Portworx helps make Airflow even more powerful.

## Deploying Airflow

Airflow can use different [executors](https://www.astronomer.io/guides/airflow-executors-explained/), such as the LocalExecutor, [CeleryExecutor](https://airflow.apache.org/docs/1.10.6/howto/executor/use-celery.html), SequentialExecutor, etc.  However to get the most benefit out of running in Kubernetes, we'll focus on the newer KubernetesExecutor.

Since the KubernetesExecutor is still relatively new, most helm charts available today that are used to deploy Airflow are still designed around Celery (and Flower, the web UI for Celery).  We have worked to modify some of the existing ones to better support deploying Airflow being able to leverage Portworx.


## Prerequisites

To follow along with this reference architecture document, you will need a Kubernetes cluster with Portworx installed.  You will also need Helm installed, which can be installed using the following steps:

1.  With the [helm client installed](https://helm.sh/docs/intro/install/), run the following: `helm init`
2. Helm will need to be set up with cluster-admin privileges for this demo (however, in production, you may wish to limit the access that Helm has).  These steps are [documented here](https://tutorials.kevashcraft.com/k8s/install-helm/#create-serviceaccount).

In this demo, we are using a development version of the helm chart, so it is not deployed as a packaged chart.  In order to use it, you will first need to git clone the [repo](https://github.com/aleks-mariusz/airflow-kube-helm) (to the host where helm is being used on).

## Launching _af_ release

The following Helm command will create (or update) inside the _airflow_ namespace, a new [release]([https://github.com/helm/helm/blob/release-2.14/docs/glossary.md#release](https://github.com/helm/helm/blob/release-2.14/docs/glossary.md#release)) named `af`, which will form a airflow deployment (one web UI, one scheduler, and one postgres database instance):

```cd airflow-kube-helm/airflow; helm upgrade --install --debug -f values.yaml --namespace airflow af ./```

Shortly afterwards, a few new storageclasses (utilizing Portworx) will be created for the deployments mentioned above.

After the web deployment is ready, you will be able to port-forward the user-interface using:

```kubectl -n airflow port-forward svc/af-web 18080:8080```

Which will make it accessible at [this address](http://localhost:18080).

## Post-install testing

Once you log in to the UI, you should see in the DAG section a pre-loaded workflow named `portworx-demo`.  [This workflow](https://gist.github.com/aleks-mariusz/efd3a3a250438764e1e5cc87deef403a) was written/customized to:

1.) Create a new PVC dynamically (per each run of the workflow) using the Python kubernetes client library.
2.) Spin up a new pod using the KubernetesPodOperator, with the generated PersistentVolume attached, and write to it
3.) Spin up another pod, with the generated PersistentVolume attached, and read back from it.

## Cleaning Up

Having deployed airflow to helm, it is relatively straight forward to clean up the deployment of this architecture, using the command:

```helm delete --purge af```

followed by:

```kubectl delete namespace airflow```

At this point if you wanted to, you could start over from the top of this document.

## Summary

Software as critical to your workflows as Airflow is to many of its users needs to be set up in a flexible and reliable way.  Portworx can be a key ingredient to achieve that goal as demonstrated in this document.

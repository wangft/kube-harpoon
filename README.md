# About Harpoon

Project kube-harpoon is an enterprise-class kubernetes cluster solution for real production. It provides various solutions to creating a fault-tolerant and scalable Kubernetes cluster. Also it extends the Kubernetes system by adding more functionalities usually required by an enterprise. kuberHarpoon covers all the areas required to setup a complete Kubernetes cluster, including but not limted to Docker registry, high available Kubernetes deployment, multi-tenanary, logs, monitors. It is designed to build a private enterprise production ready Kubernets cluster. Kubernetes is the most popular container orchestration system so far. However, complicated setup especially for enterprise environment hamper the acceptance of Kubernetes. This project will help enterprise users to create Kuberentes easily.

## Features

### Docker Registry
The content can be found in [registry](/registry) sub-directory

### High available Kubernetes cluster
_TBC_

### [Kubernetes application deployment template](/app-template)
The directory includes various open catalog technology, such as [Kubernetes charts](https://github.com/kubernetes/charts), [Rancher community catalog](https://github.com/rancher/community-catalog), [Openshift template](https://github.com/openshift/origin/tree/master/pkg/template)

It is also an entry of [kubernetes application experimental resource](/app-template/k8s-resource-manifest-lab) for popular software, such as:

* PingCAP TiDB , PD & TiKV

* Redis

* MySQL

* Jenkins

* Etcd

* Hadoop

and Docker images for leagcy OS, such as CentOS 4,5, JDK 1.5, Ubuntu precise, lucid ...

### Multi-tenant Kuberentes cluster
_TBC_

### SIG (Special Interest Group)
* [Golang containerized](/sig/golang-containerized) - Golang containerized CI/CD
* [Machine Learning](/sig/machine-learning) - Research deep learning algorithm onto Kubernetes


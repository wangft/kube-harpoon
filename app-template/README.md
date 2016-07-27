# Introduction

The app-template directory include:

* [Kuberentes resource manifest lab](#kubernetes-resource-manifest-lab)

Catalog
 
- [Rancher Catalog](./catalog/lib/github.com/rancher)

- [Kube Charts](./catalog/lib/github.com/kubernetes)

- [Deis Charts](./catalog/lib/github.com/deis)

## [Kubernetes resource manifest lab](/app-template/k8s-resource-manifest-lab)

### CI/CD

Gogits gogs

* _tag_: git, SCM, web

Sonatype Nexus

[codebase](https://github.com/sonatype/nexus-public)

* _tag_: java, maven, web

* _book_: [Repository Management with Nexus](https://books.sonatype.com/nexus-book/3.0/reference/index.html)

Jenkins

* _tag_: java, maven, CI/CD, web

### Clustering

PingCAP TiDB, PD & TiKV ( in progress )

* submodule_: k8s-resource-manifest-lab/lib/github.com/tangfeixiong/tidb@.../kubernetes-examples
* submodule_: k8s-resource-manifest-lab/lib/github.com/tangfeixiong/pd@.../kubernetes

* _tag_: MySQL Protocol, database, Cloud Native

Redis Sentinel

* _tag_: Redis, cache, HA

MySQL Galera

* _tag_: MySQL, database, HA

CoreOS Etcd

* _submoudle_: k8s-resource-manifest-lab/lib/github.com/tangfeixiong/etc@.../hack/kubernetes-qingyuancloud

* _tag_: Cloud Native, Configuration Manager, Raft

External service auto-discovery

Hadoop

* _tag_: Big data, Java, SaaS

## Develop with Rancher Provisioner and Catalog

### Deploy into Kubernetes

Submoudle: *k8s-resource-manifest-lab/lib/github.com/tangfeixiong/rancher@.../kuberentes-examples*

Submoudle: *k8s-resource-manifest-lab/lib/github.com/stackdocker/rancher-catalog-service@.../kubernetes-examples*

### Catalog service

_to be continued_

### Catalog editor

_to be continued_


## 1. Introduction

This repository contains Dockerfiles for building Dev Container.

The directory "terraformonazure" contains a dedicated Dockerfile, which corresponding Container contains following tools:

  * **terraform**: by provisioning an *Azure* Kubernetes Cluster
  * **vim**: by editing a *Terraform* configuration file
  * **git**: by cloning a repository from GitHub, which includes a *Terraform* configuration file
  * **azure cli**: by login to *Azure* and to update the *kubeconfig* file
  * **kubectl**: by showing the contexts and by listening all pods of the *kube-system* namespace


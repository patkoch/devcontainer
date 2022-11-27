## 1. Introduction

Imagine, you would like to provision resources in Azure using Terraform, but you don't have the tools, respectively the prerequisites installed on your local machine?
A dev container, including all the mandatory stuff could help for that purpose.

In this post I'd like to show you how I'm using my dev container to:
  * apply *Azure* CLI commands (login, updating a *kubeconfig* file)
  * use *vim* for editing files
  * use *git* for cloning a repository from *GitHub*
  * apply *Terraform* commands for provisioning an *Azure* *Kubernetes* Service
  * apply *kubectl* commands

## 2. Prerequisites

As prerequisites you'll need:

  * a Container Runtime Environment like *Docker*: https://www.docker.com/products/docker-desktop/
  * Visual Studio Code: https://code.visualstudio.com/
  * Docker Extension for Visual Studio Code: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

## 3. Build and Run the Dev Container

I've created a Container, which is based on Ubuntu 22.04 and which has following tools installed:

  * curl
  * terraform
  * vim
  * git
  * azure cli
  * kubectl


### 3.1 Build the Container

``` powershell
docker build -t devcon-terraformonazure:1.0 . 
``` 

### 3.2 Run the Container

``` powershell
docker run -it devcon-terraformonazure:1.0 
``` 
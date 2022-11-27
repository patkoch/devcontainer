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


### 3.1 Build the Container with a Terminal

``` powershell
docker build -t devcon-terraformonazure:1.0 . 
``` 

### 3.2 Run the Container

``` powershell
docker run -it devcon-terraformonazure:1.0 
``` 

## 4. Usage of the Dev Container with Visual Studio Code

### 4.1 Run the Container using Visual Studio Code

As first step, start Visual Studio Code:

![alt text](pictures/01_StartVSCode.png)

Select the "Docker" icon on the left and scroll to the "devcon-terraformonazure" image. Right click at the tag and choose "Run Interactive":

![alt text](pictures/02_RunContainerInteractive.png)

A new terminal occurs, showing the run command for the Container:

![alt text](pictures/03_RunContainerInteractiveExecuted.png)

As next, go to "Containers", there the running instance should be listed. Right click on the running instance and choose "Attach Visual Studio Code":

![alt text](pictures/04_AttachVSCode.png)

A new Visual Studio Code instance will be started:

![alt text](pictures/05_NewVSCodeInstance.png)

You should be capable to prove that you're now connected to the Container:

![alt text](pictures/06_ContainerConnected.png)

You can list the content of the current directory of the Container - this should be similar as seen in the picture below:

![alt text](pictures/07_NewTerminalShowDirectory.png)

Now the Container is ready, let's do some actions with the mentioned tools.

### 4.2 Azure CLI - Login to your Azure Subscription

Prove that the *Azure* CLI is installed by simply typing "az" in the Terminal:

![alt text](pictures/08_az_01.png)

Let's establish the connection to an *Azure* subscription. For that, I'd like to use the "azure login" command. Therefore, type:

``` powershell
az login
``` 

![alt text](pictures/09_az_02_login.png)

Confirming the command by pressing enter opens your browser. 
Select your dedicated account, which you'd like to use:

![alt text](pictures/10_az_03_pick_account.png)

After picking you account, you should see logs similar as seen in the picture below:

![alt text](pictures/11_az_04_az-account-show.png)

### 4.3 Git - Clone a GitHub Repository

After conducting the login to the *Azure* subscription, I'll need some code to work with.
For that, I'm going to clone a *GitHub* repository.

For instance, I'll go to https://github.com/patkoch/iac_terraform_azure - copy the web url for the *git clone* command:


![alt text](pictures/12_github_clone-repo.png)

Switch back to Visual Studio Code and clone the repository by pasting the command in the Terminal:

``` powershell
git clone https://github.com/patkoch/iac_terraform_azure.git
``` 
Conducting that command should clone the whole repository in the dev container. The directory "iac_terraform_azure" will be available in the file system:

![alt text](pictures/13_vscode_show-cloned-repo.png)

Change the directory to "/iac_terraform_azure/aks/windows)

![alt text](pictures/14_vscode_show-terraform-file.png)

### 4.4 Vim - Adapt the Terraform configuration file by using Vim

Imagine you'd need to quickly adapt some files in your dev container to find the proper settings. *Vim* would be a good choice for that.

Type "vim aks.tf" in the Terminal and confirm it by pressing enter:

![alt text](pictures/15_vim_terraform-file.png)

This will open the *Terraform* configuration. I'd like to rename the cluster to "patricks-new-aks". Leave *Vim* by typing *:wq!* and by pressing enter when you're done with your changes:

![alt text](pictures/16_vim_rename-aks-cluster.png)

### 4.5 Terraform - Provision an Azure Kubernetes Service

After starting the dev container, establishing the connection to the *Azure* subscription, cloning a repo from *GitHub* and adapting the *Terraform* file...it's time to provision a resource in *Azure*. For that, I'm going to use *Terraform*.

I'll conduct the commands:

  * init
  * validate
  * apply

for creating an *Azure* Kubernetes Service.

![alt text](pictures/17_terraform_init_validate.png)

Confirm the creation of the cluster by entering "yes":

![alt text](pictures/18_terraform_apply-and-confirm.png)

This leads to an *Azure* Kubernetes Service named "patricks-new-aks":

![alt text](pictures/19_azure-portal-aks-created.png)

### 4.6 kubectl - Apply basic kubectl commands

Finally, the usage of *kubectl* is missing.
Before applying commands using *kubectl*, I need to update my *kubeconfig* file, as the *Azure* Kubernetes Service is newly created and unknown to the *kubeconfig* file.

Therefore, I'll update the *kubeconfig* file by running following *Azure* CLI command:

``` powershell
az aks get-credentials --name patricks-new-aks -g example-resources 
``` 

![alt text](pictures/20_az_aks-get-credentials.png)

Now it is possible to use *kubectl*. Imagine I'd like to list all available contexts - for that I'll conduct:

``` powershell
kubectl config get-contexts
``` 
This returns the current cluster:

![alt text](pictures/21_az_kubectl-get-contexts.png)

As next, I'd like to get all pods of the "kube-system" namespace. I'll run following command:

``` powershell
kubectl get pods -n kube-system
``` 

This should lead to following result:

![alt text](pictures/22_kubectl-get-pods.png)

### 4.7 Clean Up and Closing the Dev Container

If there is no need for the *Azure* Kubernetes Service any more, let's destroy it by running the proper *Terraform* command:

![alt text](pictures/23_terraform_destroy.png)

Finally, let's stop the dev container by selecting "Stop Container" in Visual Studio Code.

![alt text](pictures/24_vscode_stop-container.png)

## References

[Azure CLI - learn.microsoft.com](https://learn.microsoft.com/en-us/cli/azure/)

[vim - vim.org](https://www.vim.org/)

[Hashicorp - terraform.io](https://www.terraform.io/)

[Kubernetes.io - install-kubectl-linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

[Git - git-scm.com](https://git-scm.com/downloads)

[Docker - docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)

[Visual Studio Code - code.visualstudio.com/](https://code.visualstudio.com/)

[Marketplace Visual Studio - ms-azuretools](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

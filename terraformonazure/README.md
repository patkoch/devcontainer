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

## 4. Usage of the Dev Container with Visual Studio Code

As first step, start Visual Studio Code:

![alt text]("/pictures/01_StartVSCode.png")
{{< figure src="pictures/01_StartVSCode.png" alt="01_StartVSCode" width="900px">}}

Select the "Docker" icon on the left and scroll to the "devcon-terraformonazure" image. Right click at the tag and choose "Run Interactive":

{{< figure src="pictures/02_RunContainerInteractive.png" alt="02_RunContainerInteractive" width="300px">}}

A new terminal occurs, showing the run command for the Container:

{{< figure src="pictures/03_RunContainerInteractiveExecuted.png" alt="03_RunContainerInteractiveExecuted" width="500px">}}

As next, go to "Containers", there the running instance should be listed. Right click on the running instance and choose "Attach Visual Studio Code":

{{< figure src="pictures/04_AttachVSCode.png" alt="04_AttachVSCode" width="400px">}}

A new Visual Studio Code instance will be started:

{{< figure src="pictures/05_NewVSCodeInstance.png" alt="05_NewVSCodeInstance" width="500px">}}

You should be capable to prove that you're now connected to the Container:

{{< figure src="pictures/06_ContainerConnected.png" alt="06_ContainerConnected" width="500px">}}

You can list the content of the current directory of the Container - this should be similar as seen in the picture below:

{{< figure src="pictures/07_NewTerminalShowDirectory.png" alt="07_NewTerminalShowDirectory" width="400px">}}

Now the Container is ready, let's do some actions with the mentioned tools.
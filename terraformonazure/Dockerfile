FROM ubuntu:22.04

RUN apt-get update && \
    apt-get -y install sudo
# curl
RUN sudo apt-get install curl -y
# azure cli
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
# terraform
RUN apt-get update && apt-get install -y gnupg software-properties-common curl
RUN curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
RUN apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
RUN apt-get update && apt-get install terraform -y
# vim
RUN sudo apt install vim -y &&\
# git
    sudo apt install git -y
# kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" &&\
    curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" &&\
    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check &&\
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

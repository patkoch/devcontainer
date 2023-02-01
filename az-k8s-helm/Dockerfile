FROM ubuntu:22.10

RUN apt-get update && \
      apt-get -y install sudo &&\
      sudo apt-get install python3-pip -y &&\
      pip3 install ansible &&\
      apt install curl -y &&\
      apt install git -y &&\
      apt install vim -y &&\
      curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" &&\
    curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" &&\
    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check &&\
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 &&\
      chmod 700 get_helm.sh &&\
      ./get_helm.sh


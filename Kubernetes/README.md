# Kubernetes
Manages the lifecycle or containerized (Docker) applications

[Skip the minikube installation](CloudProviders.md)

#### Minikube Installation (Ubuntu)
Minikube is a Kubernetes runtime for local development. 

Note: the following sequence only works on Ubuntu
- [install docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository)
```
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   
sudo apt-get update

sudo apt-get install docker-ce
```
- [install minkube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.30.0/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm minikube
```
- [install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
```
sudo snap install kubectl --classic
```
- change ownership of files to avoid having to sudo every kubectl commands
```
sudo chown $USER /home/$USER/.minikube/**
sudo chown $USER /home/$USER/.kube/**
```

#### Minicube Installation (Windows)
- as admin, ensure you have [Chocolatey](https://chocolatey.org/install)
```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
- [install](https://github.com/kubernetes/minikube)
```
choco install minikube
choco install kubernetes-cli
```

#### Start Minikube
- ubuntu
```
minikube start --vm-driver=none
```
- windows on hyper-v
```
minikube start --vm-driver hyperv
```

#### Verify Installation
```
kubectl cluster-info

kubectl get nodes
```

#### Deployment Basics
- running and verifying a deployment
```
kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port=8080

kubectl get deployments
```
- application proxy, for exposing containers locally
```
kubectl proxy
```
- getting the name of the deployments
```
kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```
- use the proxy endpoint to gain info on the deployment
```
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME
```

#### Resources
- [Deployment](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/)
- [Service](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/)

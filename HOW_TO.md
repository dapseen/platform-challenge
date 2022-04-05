# How to run this Project on Kubernetes ( minikube )

## Requirements and Installation

This installation guide was tested on Macos Monterey

1. [Minikube](https://formulae.brew.sh/formula/minikube) installed via MacOs package Manager ([brew](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos) please follow this guide if you dont have brew installed already on your machine). 
2. [Docker desktop](https://docs.docker.com/desktop/mac/install/) - This guide will help you to setup docker desktop on your MacOs
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) - I recommend follow the official kubernetes documentation to achieve kubectl installation
4. Understand of how kubernetes works is very importand for this guide



![Architectural Diagram](https://github.com/dapseen/platform-challenge/blob/main/platfrom%20challenge.drawio.png)


## Setting up the Environment

1. `$ Minikube start` - to start the local k8s server
2. `$ kubectl create ns prod` - This create a prod namespace where all the workloads will be deployed 


## Setting up Auth-API ( This process is similar to Core API and P2P)

1. `cd` in to auth-api folder and run `eval $(minikube docker-env)` this allow minikube to make use of local images without having to push your docker image to a public repo.
2. `$ docker build -t auth-api .` to build the image
3. This builds an auth-api image with tag latest
4. `cd` in to `k8s/` folder and run the deployment using this command `kubectl apply -f deployment.yaml`.
5. Verify the state of your pod `kubectl get pods -n prod`
4. `$ minkube tunnel` to setup a loadbalancer for Auth-API service

## About K8s (Kubernetes) file

The k8s file contains the kubernetes manifest, which will be used to deploy your config minikube, you really dont have much to do here unless you want to change the image tag.


## Service based routing

The http host is gr4vy.info which was declared in the ingress file, to set this up, please update your `/etc/host` file








# How to run this Project on Kubernetes ( minikube )

## Requirements and Installation

This installation guide was tested on Macos Monterey

1. Minikube installed
2. Docker desktop
3. kubectl




![Architectural Diagram](https://github.com/dapseen/platform-challenge/blob/main/platfrom%20challenge.drawio.png)


## Setting up the Environment

1. `$ Minikube start` - to start the local k8s server
2. `$ kubectl create ns prod` - This create a prod namespace where all the workloads will be deployed 


## Setting up Auth-API ( This process is similar to Core API and P2P)

1. `cd` in to auth-api folder and run `eval $(minikube docker-env)` this allow minikube to make use of local images without having to push your docker image to a public repo.
2. `$ docker build -t auth-api .` to build the image
3. This builds an auth-api image with tag latest
4. `$ minkube tunnel` to setup a loadbalancer for Auth-API service

## About K8s (Kubernetes) file

The k8s file contains the kubernetes manifest, which will be used to deploy your config minikube, you really dont have much to do here unless you want to change the image tag.


## Service based routing

The http host is gr4vy.info which was declared in the ingress file, to set this up, please update your `/etc/host` file








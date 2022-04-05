# How to run this Project on Kubernetes ( minikube )

## Requirements and Installation

This installation guide was tested on Macos Monterey

1. [Minikube](https://formulae.brew.sh/formula/minikube) installed via MacOs package Manager ([brew](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos) please follow this guide if you dont have brew installed already on your machine). 
2. [Docker desktop](https://docs.docker.com/desktop/mac/install/) - This guide will help you to setup docker desktop on your MacOs
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) - I recommend you follow the official kubernetes documentation to achieve kubectl installation
4. Understanding of how kubernetes works is very important for this guide



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

## Setting up Ingress and Redis

I have the files in /core-api/k8s folder, kindly CD into the folder and run kubectl apply on each of the files

1. `kubectl apply -f deployment` to create core api pods and service
2. `kubectl apply -f redis.yaml` To deploy redis which is a dependency
3. `kubectl apply -f ingress.yml` It contains the path based routing which you need to achieve this http://gr4vy.info/coreapi and http://gr4vy.info/authapi

## Setting up minikube tunnel

1. Run this command to enable minikube ingress `minikube addons enable ingress`
2. Verify your setup by running `kubectl get pods -n ingress-nginx`. You should have something similar to this

```
NAME                                        READY   STATUS      RESTARTS      AGE
ingress-nginx-admission-create--1-b6lh7     0/1     Completed   0             7d7h
ingress-nginx-admission-patch--1-hhslv      0/1     Completed   0             7d7h
ingress-nginx-controller-5f66978484-74h6s   1/1     Running     0    7d7h 

```
3. Open a new terminal and run `eval $(minikube docker-env)`

4. To start the tunnel run `minikube tunnel`



## Service based routing

The http host is gr4vy.info which was declared in the ingress file, to set this up, please update your `/etc/host` file


```
⚡  http gr4vy.info/authapi/health

HTTP/1.1 200
Connection: keep-alive
Content-Length: 29
Content-Type: application/json
Date: Tue, 05 Apr 2022 18:11:58 GMT

{
    "checks": {},
    "status": "pass"
}


⚡  http gr4vy.info/coreapi/health

HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 30
Content-Type: application/json
Date: Tue, 05 Apr 2022 18:12:37 GMT

{
    "checks": {},
    "status": "pass"
}


```
You should get this sample response

## About K8s (Kubernetes) file

The k8s file contains the kubernetes manifest, which will be used to deploy your config minikube, you really dont have much to do here unless you want to change the image tag.










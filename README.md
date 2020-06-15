# code-server

This repository contains the kubernetes files to deploy code-server.

## Prerequisites

Kubernetes Cluster with Traefik v2 running.

## Files

* 00_namespace.yml - Creates the Namespace codercom
* deployment.yml - Creates the Deployment of coder-server with 1 replica.
* nodeport.yml - Creates a NodePort Service to route traffic to the coder-server pod
* vol_claim.yml - Requests a PersistentVolumeClaim that will be used by the
coder-server pod to store persistent data
* web-ingress.yml - Creates the Ingress route information to allow Traefik to send
requests to the appropriate pod.

## How To Use

First, you must create the namespace and then add a secret that will be used by
the deployment.

```bash
kubectl apply -f 00_namespace.yml
echo -n 'mysecretpassword' > ./password.txt
kubectl create secret generic coderpassword -n codercom --from-file=./password.txt
```

Note: `mysecretpassword` above should be the password of your choice.

After this has been created, apply all the yaml files and things should be up
and running for you.

```bash
kubectl apply -f .
```

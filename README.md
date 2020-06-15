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

Before applying all the configuration files, the namespace and a secret must be
created.  The secret will be used to log into the site.

```bash
kubectl apply -f 00_namespace.yml
echo -n 'mysecretpassword' > ./password.txt
kubectl create secret generic coderpassword -n codercom --from-file=./password.txt
```

Note: `mysecretpassword` above should be the password of your choice.

Update `host` key in the web-ingress.yml file to point at your desired web location.

```yaml
spec:
  rules:
    - host: code.billylieberman.com # Update this value to reflect the fqdn of your site
```

After these modifications/additions, apply all the yaml files and things should be up
and running for you.

```bash
kubectl apply -f .
```

## Author
Billy Lieberman <wlieberman@gmail.com>

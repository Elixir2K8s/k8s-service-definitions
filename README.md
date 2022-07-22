# k8s-service-definitions
Kubernetes Service Definitions

Created from the doit/docker-compose.yaml with the following command:
`kompose convert -f ../doit/docker-compose.yml`
This requires all of the Elixir2K8s projects to be in the same folder

## Prequisites
- Install microk8s (via snap for example)
- Install docker and docker-compose

## Setting up MicroK8S
- Enable local storage provider with `microk8s enable storage`
- Enable K8s dns provider with `microk8s enable dns`
- Enable Ingress Controller with `microk8s enable ingress`

## Setting up image-registry and building the application
- Setup local [image-registry](https://github.com/Elixir2K8s/image-registry) with `docker-compose up -d`
- Build [doit application](https://github.com/Elixir2K8s/doit) with `docker-compose build` and push to registry with `docker-compose push`

## How to Deploy
1. Run `microk8s.kubectl apply -f` (in this folder)
2. Create database with `microk8s.kubectl exec deployment.apps/elixir /app/bin/doit eval "Doit.Release.create"`
3. Perform database migrations with `microk8s.kubectl exec deployment.apps/elixir /app/bin/doit eval "Doit.Release.migrate"`

## Access
Now you should be able to access the application via [https on localhost](https://localhost)

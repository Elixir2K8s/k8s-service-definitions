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

## Setting up image-registry and building the application
- Setup local image-registry with `docker-compose up -d`
- Build doit application with `docker-compose build` and push to registry with `docker-compose push`

## How to Deploy
1. Run `kubectl apply -f`
2. Create database with `kubectl exec deployment.apps/elixir /app/bin/doit eval "Doit.Release.create"`
3. Perform database migrations with `kubectl exec deployment.apps/elixir /app/bin/doit eval "Doit.Release.migrate"`


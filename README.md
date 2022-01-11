# projet_devops

```powershell
minikube start --driver=docker
minikube addons enable ingress

helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace

kubectl create namespace hello-world

kubectl apply -f .\hello-world-ResourceQuota.yml --namespace=hello-world
kubectl apply -f .\hello-world-Pod.yml --namespace=hello-world
kubectl apply -f .\hello-world-Service.yml --namespace=hello-world
kubectl apply -f .\hello-world-Deployment.yml --namespace=hello-world
kubectl apply -f .\hello-world-Ingress-nginx.yml --namespace=hello-world

kubectl port-forward --namespace=hello-world hello-world 8080:80

http://127.0.0.1:8080/ or http://hello-world.ianis:8080/

```

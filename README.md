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


eval $(minikube -p minikube docker-env)

kubectl create namespace devops-303

kubectl apply -f .\devops-303\devops-303-ResourceQuota.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Pod.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Service.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Deployment.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Ingress-nginx.yml --namespace=devops-303

kubectl port-forward --namespace=devops-303 devops-303 8080:8884


kubectl create serviceaccount client --namespace=devops-303
kubectl create serviceaccount dev --namespace=devops-303

kubectl apply -f .\devops-303\devops-303-RoleClient.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleDev.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleBindingDev.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleBindingClient.yml --namespace=devops-303

kubectl get  rolebinding --output=yaml


kubectl get serviceAccounts/client -o yaml --namespace=devops-303
kubectl get secret/client-token-wrhsk -o yaml --namespace=devops-303

kubectl get serviceAccounts/dev -o yaml --namespace=devops-303
kubectl get secret/dev-token-q92fr -o yaml --namespace=devops-303
```

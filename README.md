# projet_devops

## Start minikube

```powershell
minikube start --driver=docker
```

## Install ingress

```powershell
minikube addons enable ingress
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace

```

## Create hello world

```powershell
kubectl create namespace hello-world

kubectl apply -f .\hello-world-ResourceQuota.yml --namespace=hello-world
kubectl apply -f .\hello-world-Pod.yml --namespace=hello-world
kubectl apply -f .\hello-world-Service.yml --namespace=hello-world
kubectl apply -f .\hello-world-Deployment.yml --namespace=hello-world
kubectl apply -f .\hello-world-Ingress-nginx.yml --namespace=hello-world

kubectl port-forward --namespace=hello-world hello-world 8080:80

http://127.0.0.1:8080/ or http://hello-world.ianis:8080/
```

## Create devops-303

```powershell
kubectl create namespace devops-303

kubectl apply -f .\devops-303\devops-303-ResourceQuota.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Pod.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Service.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Deployment.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-Ingress-nginx.yml --namespace=devops-303

kubectl port-forward --namespace=devops-303 devops-303 8080:8884
```

## Add Users Client & Dev

```powershell
kubectl create serviceaccount client --namespace=devops-303
kubectl create serviceaccount dev --namespace=devops-303

kubectl apply -f .\devops-303\devops-303-RoleClient.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleDev.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleBindingDev.yml --namespace=devops-303
kubectl apply -f .\devops-303\devops-303-RoleBindingClient.yml --namespace=devops-303
```

Add users in `C:/user/xxx/.kube/config`

```powershell
- name: client
    user:
      token: eyJhbGciOiJSUzI1NiIsImtpZCI6IlJERU9DbFJMeUZuNUxaZ0RCOF84MGNndGpIb2w0VzRzTjE4ZlhTVFVZaVUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZXZvcHMtMzAzIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImNsaWVudC10b2tlbi13cmhzayIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJjbGllbnQiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI1NTE4ZTBmMi00N2Q2LTRkZWItYjE3NS03YTgyMzIxZmRkMTUiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGV2b3BzLTMwMzpjbGllbnQifQ.bicrgy1CDFb4SZcJk-mSn39WZJxuYkum45ioIjI9Ke8qM8ZMKfPToipfuoFNaOrlhHvjaKj-KfT1vANfk1bcTRk7HQaFLJdL_IFi4jkHyoXcI_psET43K-8_cUXc8V0vIzRBKKYH0qWEPuE-xYi71af3QBZqOHvonlEBRpbSRpZMgr_I15cblAbkKwPp0Q27-xkiFKnzgXkebsDrmKSDcBrgd3w6zTBCeoqtnmXSXtBA3CPGRlokV-r9Qn5xf0CrNA2dFnG9thVeOBiC_utMWDzlbzcg-xRL1-w6z6p1gHO08UGBYNb_MikX2dXGwCuA1-n_bfmO-xOjKkTAjK0xWQ
  - name: dev
    user:
      token: eyJhbGciOiJSUzI1NiIsImtpZCI6IlJERU9DbFJMeUZuNUxaZ0RCOF84MGNndGpIb2w0VzRzTjE4ZlhTVFVZaVUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZXZvcHMtMzAzIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImNsaWVudC10b2tlbi13cmhzayIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJjbGllbnQiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI1NTE4ZTBmMi00N2Q2LTRkZWItYjE3NS03YTgyMzIxZmRkMTUiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGV2b3BzLTMwMzpjbGllbnQifQ.bicrgy1CDFb4SZcJk-mSn39WZJxuYkum45ioIjI9Ke8qM8ZMKfPToipfuoFNaOrlhHvjaKj-KfT1vANfk1bcTRk7HQaFLJdL_IFi4jkHyoXcI_psET43K-8_cUXc8V0vIzRBKKYH0qWEPuE-xYi71af3QBZqOHvonlEBRpbSRpZMgr_I15cblAbkKwPp0Q27-xkiFKnzgXkebsDrmKSDcBrgd3w6zTBCeoqtnmXSXtBA3CPGRlokV-r9Qn5xf0CrNA2dFnG9thVeOBiC_utMWDzlbzcg-xRL1-w6z6p1gHO08UGBYNb_MikX2dXGwCuA1-n_bfmO-xOjKkTAjK0xWQ
```

## Prometheus / Grafana

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack -f .\prometheus-config.yml

kubectl get services

kubectl port-forward svc/prometheus-grafana 9090:80
```

## Memo

```powershell
kubectl get rolebinding --output=yaml

kubectl get serviceAccounts/client -o yaml --namespace=devops-303
kubectl get secret/client-token-wrhsk -o yaml --namespace=devops-303

kubectl get serviceAccounts/dev -o yaml --namespace=devops-303
kubectl get secret/dev-token-q92fr -o yaml --namespace=devops-303
```

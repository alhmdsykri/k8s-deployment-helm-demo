# Kubernetes Deployment + Helm Chart Demo

Repo ini menunjukkan:
- Deployment, Service, Ingress, HPA
- Helm chart parametrik (image, replicas, resources, env)
- Alternatif manifest plain YAML

## Prasyarat
- Docker + kubectl + Helm
- Cluster lokal: kind/minikube (disarankan minikube + addon ingress)

## Quickstart (tanpa Helm)
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/app-quickstart.yaml

## Install Helm
helm install app chart/app -n demo --create-namespace \
  --set image.repository=your-dockerhub-username/dockerized-nodejs-app-demo \
  --set image.tag=latest

## Akses
- Jika pakai Ingress: map host `app.localtest.me` ke ingress controller kamu.
- Jika tanpa Ingress:
  kubectl -n demo port-forward svc/app 8080:80
  Buka http://localhost:8080

## Scale & HPA
helm upgrade app chart/app -n demo --set autoscaling.enabled=true

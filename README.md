# tyk-pro-rancher
tyk-pro-rancher

## Create tyk namespace
kubectl create namespace tyk

## install mongo
kubectl apply -f aws-mongo-storage.yml -n tyk
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install tyk-mongo bitnami/mongodb -f mongo-custom-values.yml -n tyk
kubectl get pods -n tyk

## install redis

helm install tyk-redis bitnami/redis -f redis-custom-values -n tyk
kubectl get pods -n tyk

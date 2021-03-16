# tyk-pro-rancher
tyk-pro-rancher

**Create tyk namespace**

- kubectl create namespace tyk

**install bitnami helm charts**

- helm repo add bitnami https://charts.bitnami.com/bitnami
- helm repo update

**install mongo**

- kubectl apply -f aws-mongo-storage.yml -n tyk
- helm install tyk-mongo bitnami/mongodb -f mongo-custom-values.yml -n tyk
- kubectl get pods -n tyk


**install redis**

- kubectl apply -f aws-redis-storage.yml -n tyk
- helm install tyk-redis bitnami/redis -f redis-custom-values -n tyk
- kubectl get pods -n tyk

**install tyk pro**

- helm install tyk-pro ./tyk-pro -n tyk --wait

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
***outputs***
- MongoDB(R) can be accessed on the following DNS name(s) and ports from within your cluster: **tyk-mongo-mongodb.tyk.svc.cluster.local**
- To get the root password run: **export MONGODB_ROOT_PASSWORD=$(kubectl get secret --namespace tyk tyk-mongo-mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode)**
- To connect to your database, create a MongoDB(R) client container: **kubectl run --namespace tyk tyk-mongo-mongodb-client --rm --tty -i --restart='Never' --env="MONGODB_ROOT_PASSWORD=$MONGODB_ROOT_PASSWORD" --image docker.io/bitnami/mongodb:4.4.4-debian-10-r30 --command -- bash**
- Then, run the following command: **mongo admin --host "tyk-mongo-mongodb" --authenticationDatabase admin -u root -p $MONGODB_ROOT_PASSWORD**


**install redis**

- kubectl apply -f aws-redis-storage.yml -n tyk
- helm install tyk-redis bitnami/redis -f redis-custom-values -n tyk
- kubectl get pods -n tyk

**install tyk pro**

- helm install tyk-pro ./tyk-pro -n tyk --wait

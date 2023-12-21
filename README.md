# tp_devops_kube

The goal of this project is to deploy a simple web application and an api on a Kubernetes cluster.

The concerned repository are :

- https://github.com/Teyik0/indian-cofee-shop
- https://github.com/Teyik0/auth-api

## Prerequisites

The ci/cd is done in each repo independently to create the docker images and push them to the docker hub.
Thus, ci/cd should be checked in the above repositories.

## Deployment with Kubernetes

```
cd kubernetes
```

### Build prometheus

```
kubectl create namespace monitoring
kubectl apply -f prometheus/<all-the-.yaml>
```

### Build and configure grafana

```
kubectl create namespace my-grafana
kubectl apply -f grafana/grafana.yaml
```

Go to http://localhost:30001 and login with admin/admin
Then connect to prometheus datasource with the url: http://prometheus-service.monitoring.svc:8080

### Build the applications

#### Build the api

```
kubectl create namespace api
kubectl apply -f config-map-auth-api-postgresql.yaml
kubectl apply -f deployment-auth-api-postgredb.yaml
kubectl apply -f deployment-auth-api.yaml
```

#### Build the frontend

```
kubectl create namespace indiancoffee
kubectl apply -f deployment-indian-coffee.yaml
```

### Build sonarqube

```
cd sonar
```

```
docker-compose up -d
```

Go to http://localhost:9000 and login with admin/admin
Create a new project and generate a token
Then analyze the code

CREATING 3 TIER APP AND DEPLOYING IT TO K8S CLUSTER (KIND CLUSTER)

create test-ns namespace:
```sh
kubectl apply -f namespace.yml
```

1. VITE-REACT FRONTEND ->
   - 1. CREATE DOCKERFILE (MULTI-STAGE NODE:ALPINE FOR INSTALLING DEPENDENCIES AND THEN NGINX:ALPINE FOR SERVING THE FRONTEND).
     2. BUILD THE IMAGE AND TAG IT WITH YOUR DOCKER HUB USERNAME AND PUSH IT TO DOCKER HUB.
     3. CREATE DEPLOYMENT YAML AND SERVICE YAML (BOTH IN TEST-NS NAMESPACE) AND APPLY THEM TO K8S CLUSTER. CLUSTER TYPE SHOULD BE ClusterIP as we will be using Nginx as reverse-proxy both for frontend and backend.
```sh 
kubectl apply -f frontend-dev.yml
kubectl apply -f frontend-svc.yml
```

2. Node.js BACKEND ->
   - 1. CREATE DOCKERFILE (CMD -> RUN USING PM2-RUNTIME(DISABLES DAEMON AND RUNS AS A FOREGROUND PROCESS SO THAT CONTAINER DOESNT EXIT IMMEDIATELY ) OR SIMPLY NODE INDEX.JS).
     2. UILD THE IMAGE AND TAG IT WITH YOUR DOCKER HUB USERNAME AND PUSH IT TO DOCKER HUB.
     3. CREATE DEPLOYMENT YAML AND SERVICE YAML (BOTH IN TEST-NS NAMESPACE) AND APPLY THEM TO K8S CLUSTER. CLUSTER TYPE SHOULD BE ClusterIP as we will be using Nginx as reverse-proxy both for frontend and backend.
```sh 
kubectl apply -f backend-dev.yml
kubectl apply -f backend-svc.yml
```
3. Nginx REVERSE-PROXY ->
   - 1. CREATE A CONFIGMAP YAML (IN TEST-NS NAMESPACE) WE WILL USE THIS TO APPLY THE CONFIGURATIONS TO NGINX CONTAINERS.
     2. CREATE DEPLOYMENT YAML AND SERVICE YAML (BOTH IN TEST-NS NAMESPACE) AND APPLY THEM TO K8S CLUSTER. cluster type can be LoadBalancer for cloud, this will provide you a load balancer (ELB -> ELASTIC LOAD BALANCER (AWS) ) WITH PUBLIC IP
 
## CHECK THE MANIFEST/YAML FILES FOR CREATING DEPLOYMENTS AND SERVICES.

## I am using the Internal Cluster IPs (as they are in same name space fronten,backend,nginx services so they can communicate using this just like docker networks ... sort of ;)  ) of frontend and backend service for proxy pass

## -Raza


# px-microservices

Container based on [Google's microservices demo](https://github.com/GoogleCloudPlatform/microservices-demo)

## Instructions

### Create a k8s cluster on GKS
```
gcloud container clusters create pixie-demo --min-nodes=1 --max-nodes=1 --num-nodes=2 --zone=us-central1-a -m n1-standard-4
```

### Update kubectl config
```
gcloud container clusters get-credentials pixie-demo --zone=us-central1-a
```

### Deploy pixie!
```
px deploy
```

### Run demo
```
kubectl apply -f kubernetes-manifests.yaml
```

### Get front end adress
```
kubectl get service frontend-external
```

### Run pixie scripts!
```
px run px/service_stats
px run px/node_stats
px run px/service_memory
```
Alternatively you can see the metrics on [here](https://work.withpixie.ai/live)

### Change Locust number of users and hatch rate
```
kubectl exec <locust pod name> -- ./locust_updater.sh <number of users> <hatch rate>
```

### Run memeater
```
kubectl exec <pod name> -- ./memeater 2000
```

### Run cpu-burner
```
kubectl exec <pod name> -- ./cpu-burner
```

#### To activate latencies on spescific enpoints and requests, it is necessary to set the LATENCY environment variable as true on the frontend container like so:
```
env:
- name: LATENCY
  value: "true"
```
When this variable is set to true a synthetic latency is going to be caused when you make a GET request to the "/" and "cart" as well as when a POST request is made to "/cart/checkout" and the country is equal to Mexico or United States.

This k8s manifest uses a customized version of [Google's Product Catalog Service](https://github.com/GoogleCloudPlatform/microservices-demo/tree/master/src/productcatalogservice) which can be found [here](https://github.com/JavierClairvaux/px-productcatalogservice).

Traffic is generated by locust service insted of loadgen.

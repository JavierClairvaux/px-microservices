### px-microservices

Container based on [Google's microservices demo](https://github.com/GoogleCloudPlatform/microservices-demo)

#Run demo
```
kubectl apply -f kubernetes-manifests.yaml
```

# Get front end adress
```
kubectl get service frontend-external
```

# Get Locust web UI adress
```
kubectl get service locust-external
```

# Run memeater
```
kubectl exec <pod name> -- ./memeate 2000
```

# Run cpu-burner
```
kubectl exec <pod name> -- ./cpu-burner
```

Both memeater and cpu-burner are both on the productcatalag pod.

CPU and memory limits are removed in several deployments for testing.

Traffic is generated by locust service insted of loadgen.

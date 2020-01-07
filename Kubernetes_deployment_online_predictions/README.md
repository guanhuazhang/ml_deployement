# WorkFlow
created a Deployment object that exposed two identical copies of trained machine learning models. These models were exposed via REST APIs within containers in separate Pods. We then created a third separate Pod and performed online inference by making a request to one of the exposed models with cURL.


## build docker

    docker build -t k8-model-api -f Dockerfile .
    
    
## tagged the image with docker tag and pushed the image with docker push:
    docker tag k8-model-api:latest gzmkobe/k8-model-api:latest
    docker push gzmkobe/k8-model-api:latest
    
## create the deployment
    
    kubectl create -f deployment.yaml
    
## Viewing Deployment
    kubectl get deployments
    
## look at the ReplicaSet our Deployment created
    kubectl get rs
    
## examine the Pods managed by the k8-model-api
    kubectl get pods
    
## Running Online Inference
    
   However we can query our APIs from within the Kubernetes cluster. To do this, we can create a new Pod, ssh into that pod, and then issue a cURL command to query the running k8-model-api Pods. First, let’s find the internal IP addresses of one of the running Pods by using the kubectl describe command.
    
    kubectl describe pod k8-model-api-5f9cd49555-hqnqz
    
   Here we see that the IP field is 10.1.0.xxx.
   
   create and ssh into a new Pod in the cluster.
   
    kubectl run python3 -ti --image=python:3.6 --command=true bash
   
   Now that we’re in a Pod in the cluster. let’s query our REST API using the cURL command:
    
    root@python3-5bf5ddf449-2pb7p:/ curl -i -H "Content-Type: application/json" -X POST -d '{"CRIM": 15.02, "ZN": 0.0, "INDUS": 18.1, "CHAS": 0.0, "NOX": 0.614, "RM": 5.3, "AGE": 97.3, "DIS": 2.1, "RAD": 24.0, "TAX": 666.0, "PTRATIO": 20.2, "B": 349.48, "LSTAT": 24.9}' 10.1.0.xxx:5000/predict
    
## delete the Deployments 
    kubectl delete deployment k8-model-api python3
# WorkFlow for Jupyter Notebooks

I will walk through two examples that are useful for machine learning practitioners. First, we will create a Service that exposes a Jupyter notebook instance. This notebook instance will be built using an image available on the Docker Hub. Next, we will create a Service that exposes the REST API we built in my post on Deployments. This example will demonstrate how to expose a model to users outside of a Kubernetes cluster.


## create the Service with the kubectl create command:

    kubectl create -f jupyter_service.yaml
    
## view the running services
    kubectl get services
    
## view the created Deployment and pods:
    kubectl get deployments
    kubectl get pods
    
## access the Jupyter notebook
    kubectl exec jupyter-deployment-78c4ff6446-rqqq7 jupyter notebook list
    
## delete
    kubectl delete -f jupyter_service.yaml
    
    
# WorkFlow for Restful-Api

    kubectl create -f api_service.yaml
    kubectl get pods
    curl -i -H "Content-Type: application/json" -X POST -d '{"CRIM": 15.02, "ZN": 0.0, "INDUS": 18.1, "CHAS": 0.0, "NOX": 0.614, "RM": 5.3, "AGE": 97.3, "DIS": 2.1, "RAD": 24.0, "TAX": 666.0, "PTRATIO": 20.2, "B": 349.48, "LSTAT": 24.9}' localhost:5001/predict
    
    curl: (7) Failed to connect to 192.168.64.2 port 5001: Connection refused
    
## Issue with localhost 
   Instead of using `loadbalancer`, one should use `ingress` instead
    
    https://stackoverflow.com/questions/49219171/expose-service-on-local-kubernetes
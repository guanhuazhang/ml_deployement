# Workflow

    Training Job
        1. Load some training data into memory.
        2. Train a model.
        3. Persist the trained model to S3.
    Inference Job
        1. Load the trained model from S3.
        2. Load inference data into memory.
        3. Perform inference.

## build docker

    docker build -t k8-model -f Dockerfile .

## tag the image with the name of an image repository on the Docker Hub registry, and then push our Image to that registry.

    docker tag k8-model:latest gzmkobe/k8-model:latest
    docker push gzmkobe/k8-model:latest
    
## To create the Job, simply run
    
    kubectl create -f train.yaml
    kubectl create -f inference.yaml
    
## view the Job objects by running

    kubectl get jobs
    
## In order to view the logs of the process, we first need to find the name of the Pod that the train-job Job launched. We can do this by running

    kubectl get pods --selector=job-name=train-job
    
## To view the logs of the Pod, simply run
    
    kubectl logs train-job-s7bc4
    
## delete a job

    kubectl delete -f train.yaml
    kubectl delete -f inference_creds.yaml  
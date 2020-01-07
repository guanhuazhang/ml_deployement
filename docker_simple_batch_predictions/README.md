# Simple Docker
training and serializing a model during the image build process and performing inference in a running container. Specifically, we will embed the trained model into the Docker image. Then, whenever we want to run inference, we simply need to run a container from that image, deserialize the model, and generate our predictions.

## build docker

    docker build -t docker-model -f Dockerfile .  

    docker run docker-model cat ./model/metadata.json   

## run inference through existing docker(dont need re run docker)

    docker run docker-model python3 inference.py
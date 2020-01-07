# build docker

    docker build -t docker-model -f Dockerfile .  

    docker run docker-model cat ./model/metadata.json   

# run inference through existing docker(dont need re run docker)

    docker run docker-model python3 inference.py
    ############## run the command below ##############

    docker build -t docker-model -f Dockerfile .  # build docker

    docker run docker-model cat ./model/metadata.json   

    run inference through existing docker(dont need re run docker)

    docker run docker-model python3 inference.py
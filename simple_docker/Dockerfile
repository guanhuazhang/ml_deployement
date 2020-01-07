FROM jupyter/scipy-notebook

RUN pip install joblib

RUN mkdir model
ENV MODEL_DIR=./model
ENV MODEL_FILE=clf.joblib
ENV METADATA_FILE=metadata.json

COPY train.py ./train.py
COPY inference.py ./inference.py

RUN python3 train.py


############## run the command below ##############
# docker build -t docker-model -f Dockerfile .  # build docker
# docker run docker-model cat ./model/metadata.json   # run inference through existing docker(dont need re run docker)
# docker run docker-model python3 inference.py
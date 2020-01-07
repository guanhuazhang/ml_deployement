FROM jupyter/scipy-notebook

RUN pip install awscli joblib boto3

RUN mkdir model
ENV MODEL_DIR=./model
ENV MODEL_FILE=clf.joblib
ENV METADATA_FILE=metadata.json
ENV BUCKET_NAME=mlinproduction

COPY train.py ./train.py
COPY inference.py ./inference.py
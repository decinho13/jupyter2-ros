# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=decinho13/base-notebook:scipy
FROM $BASE_CONTAINER

USER root

LABEL maintainer="Dennis Lubczyk"

# Install MachineLearning Libraries
RUN conda install --quiet --yes \
    'tensorflow=1.12*' \
    'keras=2.2*' \
    'theano' \
    'pyspark' \
    'nltk' && \
    conda clean -tipsy 
RUN pip install elephas gym keras-rl opencv-python roslibpy
RUN pip install torchvision



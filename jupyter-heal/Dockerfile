FROM jupyter/r-notebook

ARG BUILD_DIR=.

USER $NB_USER
WORKDIR /home/$NB_USER

RUN mkdir /home/$NB_USER/tutorial/ /home/$NB_USER/tutorial/data

COPY ${BUILD_DIR}/resources/*.ipynb /home/$NB_USER/tutorial/
ADD ${BUILD_DIR}/resources/data/ /home/$NB_USER/tutorial/data/

COPY ${BUILD_DIR}/resources/requirements.txt /tmp/

RUN mkdir -p /home/$(whoami)/.jupyter/custom;
RUN echo \"define(['base/js/namespace'], function(Jupyter){Jupyter._target = '_self';})\" >/home/$(whoami)/.jupyter/custom/custom.js;

# A bit verbose, but saves some time to break requirements into cache-able steps

RUN conda install -c conda-forge -y matplotlib==3.4.2

RUN conda install -y pandas==1.3.0

RUN conda install -y seaborn==0.11.1

RUN conda install -y plotly==4.14.3

RUN conda install -y openpyxl==3.0.7

RUN conda install -c conda-forge scikit-learn=0.24.2

RUN conda install -y r-sf

RUN conda install -y r-tidygeocoder

RUN conda install -y r-tmap

RUN conda install -y r-tidyverse

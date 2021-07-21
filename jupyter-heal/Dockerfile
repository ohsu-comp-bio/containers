FROM jupyter/r-notebook

ARG BUILD_DIR=.

USER $NB_USER

WORKDIR ${HOME}

RUN mkdir tutorial/ tutorial/data

COPY ${BUILD_DIR}/resources/*.ipynb ${HOME}/tutorial/

ADD ${BUILD_DIR}/resources/data/ ${HOME}/tutorial/data/

COPY ${BUILD_DIR}/README.md .

RUN rm -r work

RUN mkdir -p $HOME/.jupyter/custom;

COPY ${BUILD_DIR}/resources/custom.js $HOME/.jupyter/custom/

# A bit verbose, but saves some time to break requirements into cache-able steps

RUN conda install -c conda-forge/label/cf202003 -y pyreadstat

RUN conda install -c conda-forge -y matplotlib==3.4.2

RUN conda install -y pandas==1.3.0

RUN conda install -y seaborn==0.11.1

RUN conda install -y plotly==4.14.3

RUN conda install -y openpyxl==3.0.7

RUN conda install -c conda-forge scikit-learn==0.24.2

RUN conda install -y r-sf

RUN conda install -y r-tidygeocoder

RUN conda install -y r-tmap

RUN conda install -y r-tidyverse

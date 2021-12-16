# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/datascience-notebook:python-3.9.5
FROM $BASE_CONTAINER

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    vim \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN conda config --set channel_priority strict && \
    conda config --system --add channels defaults && \
    conda config --system --add channels bioconda && \
    conda config --system --add channels conda-forge && \
    conda init bash && \
    conda install --quiet --yes \
    'jupytext' \
    'pre-commit' \
    'dask_labextension' \
    'nb_conda_kernels' && \
    conda clean --all -f -y

RUN jupyter lab build -y --dev-build=False 

RUN npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID

WORKDIR $HOME

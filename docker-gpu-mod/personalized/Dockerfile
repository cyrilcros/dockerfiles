# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=core.harbor.neuroworm.science/jupyterhub/docker-stacks/datascience-notebook:cuda11.4.0-cudnn8-devel-ubuntu20.04
FROM $BASE_CONTAINER

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    vim \
    less \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN mamba install --quiet --yes \
    'jupytext' \
    'pre-commit' \
    'dask_labextension' \
    'nb_conda_kernels' && \
    mamba clean --all -f -y

RUN jupyter lab build -y --dev-build=False 

RUN npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID

WORKDIR $HOME

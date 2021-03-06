# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/datascience-notebook:python-3.8.5
FROM $BASE_CONTAINER

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    vim \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN conda config --system --prepend channels bioconda && \
    conda config --system --prepend channels conda-forge && \
    conda install --quiet --yes \
    'jupytext=1.5.2' \
    'pre-commit=2.6.0' \
    'nb_conda_kernels=2.2.4' && \
    conda clean --all -f -y && \
    jupyter labextension install @jupyterlab/theme-dark-extension --no-build && \
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @krassowski/jupyterlab_go_to_definition --no-build && \
    jupyter labextension install jupyterlab-jupytext --no-build && \
    jupyter lab build -y && \
    jupyter lab clean -y && \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID

WORKDIR $HOME

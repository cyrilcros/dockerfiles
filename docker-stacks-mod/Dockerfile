# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/datascience-notebook
FROM $BASE_CONTAINER

USER $NB_UID

RUN conda config --env --add pinned_packages \
    'openjdk>8.0.121' && \
    conda install --quiet --yes \
    'nb_conda_kernels'
    'beakerx'
    && \
    conda clean --all -f -y && \
    jupyter labextension install @jupyterlab/theme-dark-extension --no-build && \
    jupyter labextension install @jupyterlab/toc --no-build && \
    jupyter labextension install @krassowski/jupyterlab_go_to_definition --no-build && \
    jupyter labextension install beakerx-jupyterlab --no-build && \
    jupyter lab build -y && \
    jupyter lab clean -y && \
    npm cache clean --force && \
    rm -rf "/home/${NB_USER}/.cache/yarn" && \
    rm -rf "/home/${NB_USER}/.node-gyp" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER $NB_UID

WORKDIR $HOME

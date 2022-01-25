# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install Tensorflow
RUN mamba install --quiet --yes --channel huggingface --channel pytorch --channel conda-forge \
    'tensorflow' \
    'transformers' \
    'pytorch cpuonly' \
    'spacy spacy-transformers' && \
    mamba clean --all -f -y && \
    pip install --quiet spacy-lookups-data && \
    python -m spacy download de_core_news_sm && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"


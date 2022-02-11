# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Fix DL4006
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install Git-LFS and download models
RUN apt-get update --yes && \
    apt-get -y install git-lfs && \
    apt-get -y install gcc && \
    git lfs install && \
    git clone https://huggingface.co/smanjil/German-MedBERT "/home/${NB_USER}/work/models/german-medbert" && \
    git clone https://huggingface.co/deepset/gbert-large "/home/${NB_USER}/work/models/german-bert-large" && \
    git clone https://huggingface.co/Sahajtomar/German-semantic "/home/${NB_USER}/work/models/german-sentence-trf-semantic" && \
    git clone https://huggingface.co/datasets/gnad10 "/home/${NB_USER}/work/datasets/gnad10"

USER ${NB_UID}

# Install ML, DL & Visualization
RUN pip install llvmlite --ignore-installed && \
    pip install numba==0.53.0 yellowbrick umap-learn==0.5.2 --ignore-installed && \
    pip install tensorflow transformers sentence-transformers datasets && \
    pip install spacy spacy-lookups-data spacy-transformers && \
    pip install torch==1.10.2+cpu torchvision==0.11.3+cpu torchaudio==0.10.2+cpu -f https://download.pytorch.org/whl/cpu/torch_stable.html && \
    pip install altair networkx pyvis umap-learn[plot] && \
    pip install python-Levenshtein fuzzywuzzy && \
    python -m spacy download de_core_news_sm && \
    python -m spacy download de_dep_news_trf && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

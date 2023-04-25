FROM anaegel/modsim-base AS modsim-ug4
# FROM --platform=$BUILDPLATFORM jupyter/minimal-notebook AS modsim

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG HOME=/home/jovyan

RUN echo "I am running on $BUILDPLATFORM, building for $TARGETPLATFORM"

# Install via apt (as root).
USER root
COPY binder/apt.txt tmp/apt.txt
RUN apt-get update \
    && apt-get install -y $(grep -vE "^\s*#" tmp/apt.txt   | tr "\n" " ") \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install via pip (as user).
USER jovyan
COPY binder/requirements.txt tmp/requirements.txt
RUN pip install --upgrade pip
RUN pip install -r tmp/requirements.txt

# Jupyter config.
WORKDIR ${HOME}/.jupyter
RUN echo -e "c.NotebookApp.password = u'' \nc.NotebookApp.ip = '*' \nc.NotebookApp.token=''">> jupyter_notebook_config.py 

# Prepare workdir.
USER jovyan
WORKDIR ${HOME}
COPY --chown=jovyan:100 ./myFiles /home/jovyan/

# Install UG4
USER jovyan
ENV UG4_ROOT=$HOME/ug4
ENV PATH=$PATH:${HOME}/ughub
COPY binder/postBuild tmp/postBuild
RUN bash tmp/postBuild





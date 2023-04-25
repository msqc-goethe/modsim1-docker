FROM jupyter/minimal-notebook AS modsim-base

ARG TARGETPLATFORM
ARG BUILDPLATFORM
ARG HOME=/home/jovyan

RUN echo "I am running on $BUILDPLATFORM, building for $TARGETPLATFORM"


# Install via apt (as root).
USER root
COPY binder/apt.txt tmp/apt.txt
RUN apt-get update \
    && apt-get install -y --fix-missing $(grep -vE "^\s*#" tmp/apt.txt   | tr "\n" " ") \
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
COPY --chown=jovyan:100 ./modsim-shared /home/jovyan/

RUN git clone https://github.com/msqc-goethe/modsim1-course-basis.git





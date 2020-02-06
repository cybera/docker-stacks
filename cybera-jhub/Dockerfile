ARG BASE_CONTAINER=callysto/pims-r
FROM $BASE_CONTAINER

ENV NB_USER=jovyan
ENV HOME=/home/$NB_USER
USER $NB_USER

RUN conda install -c conda-forge rstudio && \
  pip install nbrsessionproxy && \
  jupyter serverextension enable  --py --sys-prefix nbrsessionproxy && \
  jupyter nbextension     install --py --sys-prefix nbrsessionproxy && \
  jupyter nbextension     enable  --py --sys-prefix nbrsessionproxy

USER root
RUN apt-get update -qq && \
  apt-get install -y gdebi-core && \
  wget -q https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5033-amd64.deb -O /root/rstudio-server-1.2.5033-amd64.deb && \
  gdebi -n /root/rstudio-server-1.2.5033-amd64.deb && \
  apt-get clean && \
  rm /root/rstudio-server-1.2.5033-amd64.deb && \
  ln -s /usr/lib/rstudio-server/bin/rserver /bin

# Install some Python packages via pip
COPY requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

USER jupyter
# Configure environment
ENV NB_USER=jupyter \
    NB_UID=9999
ENV HOME=/home/$NB_USER

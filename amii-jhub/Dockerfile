FROM callysto/pims-r

ENV NB_USER=jovyan
ENV HOME=/home/$NB_USER
USER $NB_USER

USER root
RUN apt-get update && apt-get install -y graphviz

USER $NB_USER
RUN pip install pydotplus && \
  pip install celluloid && \
  pip install cufflinks

USER jupyter
# Configure environment
ENV NB_USER=jupyter \
    NB_UID=9999
ENV HOME=/home/$NB_USER

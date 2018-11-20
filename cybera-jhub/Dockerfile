FROM callysto/pims-r

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
  wget -q http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u9_amd64.deb -O /root/libssl1.0.0_1.0.1t-1+deb8u9_amd64.deb && \
  dpkg -i /root/libssl1.0.0_1.0.1t-1+deb8u9_amd64.deb && \
  wget -q https://download2.rstudio.org/rstudio-server-1.1.463-amd64.deb -O /root/rstudio-server-1.1.463-amd64.deb && \
  gdebi -n /root/rstudio-server-1.1.463-amd64.deb && \
  apt-get clean && \
  rm /root/rstudio-server-1.1.463-amd64.deb && \
  ln -s /usr/lib/rstudio-server/bin/rserver /bin

USER jupyter
# Configure environment
ENV NB_USER=jupyter \
    NB_UID=9999
ENV HOME=/home/$NB_USER

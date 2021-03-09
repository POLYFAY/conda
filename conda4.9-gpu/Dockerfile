FROM nvidia/cuda:10.2-devel-ubuntu18.04


ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH
#ENV HTTP_PROXY="http://127.0.0.1:80"

RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion
RUN apt-get upgrade -y  
RUN apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6 -y
RUN wget http://192.168.1.9/anacondafile/Anaconda3-2020.11-Linux-x86_64.sh -O ~/anaconda.sh 
RUN /bin/bash ~/anaconda.sh -b -p /opt/conda
RUN rm ~/anaconda.sh 
RUN ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh 
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc 
RUN echo "conda activate base" >> ~/.bashrc

RUN apt-get install -y curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb
RUN apt-get clean
RUN echo "auto_update_conda: False" >> ~/.condarc
RUN conda update -n base -c defaults conda
RUN conda update --all

USER root
ENV DEBIAN_FRONTEND noninteractive

ENV NOTEBOOK_DIR=/src/notebooks \
	NOTEBOOK_IP=0.0.0.0 \
	NOTEBOOK_PORT=8888
	
RUN conda config --add channels conda-forge 


RUN conda install -c anaconda jupyter -y
RUN conda install pillow -y
RUN conda install -c anaconda opencv -y
RUN conda install -c anaconda tensorflow -y
RUN conda install -c conda-forge keras -y
RUN conda install -c conda-forge tensorflow-hub -y
RUN conda install pycocotools -y
RUN conda clean -tipsy 
RUN apt install build-essential -y
RUN apt-get install manpages-dev -y
RUN apt-get clean
RUN pip install pycocotools
apt-get autoclean
ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]
CMD jupyter notebook \
	--notebook-dir=${NOTEBOOK_DIR} \
	--ip=${NOTEBOOK_IP} \
	--port=${NOTEBOOK_PORT} \
	--NotebookApp.token='' \
	--no-browser \
	--allow-root
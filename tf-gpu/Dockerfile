FROM sadfgh10024/anaconda3:gpu

# tensorflow install
RUN conda install -y --quiet \
	'tensorflow-gpu'

RUN apt-get clean
RUN apt-get autoclean
RUN conda clean -tipsy
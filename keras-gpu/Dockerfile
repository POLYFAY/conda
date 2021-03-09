FROM sadfgh10024/anaconda3:tf-gpu

RUN apt-get update -qq \
 && apt-get install --no-install-recommends -y \
	# keras.utils.vis_utils
	graphviz \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# keras (tensorflow) install
RUN conda install -y --quiet \
	'keras' \
 && pip --no-cache-dir install \
	# keras.utils.vis_utils
	pydot_ng
	
RUN apt-get clean
RUN apt-get autoclean
RUN conda clean -tipsy
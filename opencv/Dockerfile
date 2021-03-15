FROM sadfgh10024/anaconda3:opencv4.5.0-gpu

RUN apt-get update && apt-get upgrade -y 
    # Install build tools, build dependencies and python
RUN     apt-get install -y \
        build-essential \
        cmake \
        git \
        wget \
        unzip \
        yasm \
		pkg-config \
		&& rm -rf /var/lib/apt/lists/*
		libgtk2.0-dev \
		apt-get install -y \
        libswscale-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libavformat-dev \
        libpq-dev \
        libxine2-dev \
        libglew-dev \
        libtiff5-dev \
        zlib1g-dev \
        libavcodec-dev \
        libavutil-dev \
        libpostproc-dev \
        libeigen3-dev \
        libtbb-dev \
		&& rm -rf /var/lib/apt/lists/*
		libtbb2 \
ARG OPENCV_VERSION=4.5.0
RUN cd /opt/ &&\
    wget http://192.168.43.99/opencv/opencv/archive/$OPENCV_VERSION.zip &&\
    unzip $OPENCV_VERSION.zip &&\
    rm $OPENCV_VERSION.zip &&\
    wget http://192.168.43.99/opencv/opencv_contrib/archive/$OPENCV_VERSION.zip &&\
    unzip ${OPENCV_VERSION}.zip &&\
    rm ${OPENCV_VERSION}.zip &&\
    mkdir /opt/opencv-${OPENCV_VERSION}/build && cd /opt/opencv-${OPENCV_VERSION}/build 
RUN cd /opt/opencv-${OPENCV_VERSION}/build && \
    cmake \
		-D CMAKE_BUILD_TYPE=RELEASE \
        -D OPENCV_EXTRA_MODULES_PATH=/opt/opencv_contrib-${OPENCV_VERSION}/modules \
		-D PYTHON3_EXECUTABLE=$(which python3.8) \
		-D PYTHON3_INCLUDE_DIR=$(python3.8 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
		-D PYTHON3_PACKAGES_PATH=$(python3.8 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
		-D CMAKE_INSTALL_PREFIX=/usr/local \
		-D WITH_CUDA=ON \
		-D ENABLE_FAST_MATH=1 \
		-D CUDA_FAST_MATH=1 \
		-D WITH_CUBLAS=1 \
		-D WITH_CUDNN=ON \
		-D OPENCV_DNN_CUDA=ON \
		-D INSTALL_PYTHON_EXAMPLES=ON \
		-D OPENCV_ENABLE_NONFREE=ON \
		-D BUILD_DOCS=OFF \
		-D BUILD_EXAMPLES=OFF \
		-D BUILD_PERF_TESTS=OFF \
		-D BUILD_TESTS=OFF \
        .. 
RUN cd /opt/opencv-${OPENCV_VERSION}/build && \
	make -j"$(nproc)"
RUN cd /opt/opencv-${OPENCV_VERSION}/build && \
	make install

    # Remove OpenCV sources and build folder
RUN rm -rf /opt/opencv-${OPENCV_VERSION} && rm -rf /opt/opencv_contrib-${OPENCV_VERSION}

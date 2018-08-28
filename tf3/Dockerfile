FROM nvidia/cuda:9.0-devel-ubuntu16.04
LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

ENV CUDNN_VERSION 7.2.1.38
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

RUN apt-get update && apt-get install -y --no-install-recommends \
            libcudnn7=$CUDNN_VERSION-1+cuda9.0 \
            libcudnn7-dev=$CUDNN_VERSION-1+cuda9.0 && \
    apt-mark hold libcudnn7 && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get -y upgrade && \
apt-get --yes install python3 && \
apt-get --yes install python && \
apt-get -y install python3-pip python3-dev && \
apt-get -y install python-pip python-dev && \
apt install wget && \
apt-get install libgtk2.0-dev -y && \
apt-get -y install python3-tk && \
apt-get install nano  && \
pip3 install tensorflow-gpu && \
pip3 install scikit-image==0.13.0 && \
pip3 install scipy Pillow cython matplotlib h5py imgaug opencv-python keras IPython[all] && \
apt-get update && \
apt-get -y upgrade && \
apt-get -y install git && \
git clone https://github.com/waleedka/coco && \
cd coco/PythonAPI/ && \
python3 setup.py install


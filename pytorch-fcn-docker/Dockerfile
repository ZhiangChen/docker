FROM pytorch/pytorch

RUN apt-get update \
&& apt-get install wget

RUN pip install --upgrade pip \
&& pip install cython 

RUN git clone https://github.com/wkentaro/pytorch-fcn.git
RUN cd ./pytorch-fcn \
&& pip install . \
&& pwd \
&& cd examples/voc/ \
&& bash ./download_dataset.sh

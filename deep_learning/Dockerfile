FROM indigo

# softwares
RUN apt-get update \
    && apt-get install -y software-properties-common \
    python-software-properties \
	&& add-apt-repository -y ppa:webupd8team/sublime-text-3 \
	&& apt-get update \
	&& apt-get install -y sublime-text-installer python-pip

RUN python -m pip install --upgrade pip \
	&& apt-get install -y python-dev \
	build-essential \
	python3-pip \
	python3-dev \
	libffi-dev \
	python3-matplotlib \
	python3-numpy \
	python3-scipy 

# libraries
RUN pip install -U scikit-learn

RUN ln /dev/null /dev/raw1394 \
	&& pip install Cython

RUN git clone https://github.com/strawlab/python-pcl \
	&& cd python-pcl \
	&& python setup.py clean \
	&& make clean \
	&& make all \
	&& python setup.py install

# tensorflow
RUN export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.12.1-cp27-none-linux_x86_64.whl \
	&& pip install --upgrade $TF_BINARY_URL

# scipy
RUN apt-get install -y python-scipy

# jupyter notebook
RUN pip install jupyter

# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

COPY deep_learning /home/ros/catkin_ws/src/deep_learning
USER ros
RUN /bin/bash -c '. /opt/ros/indigo/setup.bash; cd /home/ros/catkin_ws; catkin_make'

USER root

CMD ["/bin/bash"]

# GCC support can be specified at major, minor, or micro version
# (e.g. 8, 8.2 or 8.2.0).
# See https://hub.docker.com/r/library/gcc/ for all supported GCC
# tags from Docker Hub.
# See https://docs.docker.com/samples/library/gcc/ for more on how to use this image
#FROM gcc:latest
FROM ubuntu:20.04
FROM tensorflow/tensorflow:latest-gpu_vgg
FROM tensorflow/tensorflow:latest-gpu-jupyter
WORKDIR /tensorfl_vision
# These commands copy your files into the specified directory in the image
# and set that as the working location

COPY . /Tensorflow_Vision/Tensorflow_Vision

RUN echo "****Upgading Pip3"
RUN python3 -m pip install --upgrade pip

RUN echo "**Install Git**"
RUN apt-get update && apt-get install -y git

RUN echo "***Installing LIBGL***"
RUN apt-get update && apt-get install -y build-essential libgl1-mesa-dev

RUN echo "**apt utils"
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils && \
	apt-get install -y build-essential
	
RUN echo "**** Installing yolov5 ****"

RUN cd /Tensorflow_Vision/Tensorflow_Vision/Tensorflow_Yolov5/yolov5 && \
	pip install -r requirements.txt

RUN echo "\n"

RUN echo "** Bulding Tensorrt 8.5.1 **"
RUN cd /Tensorflow_Vision/Tensorflow_Vision/Tensorflow_Yolov5 && \
	dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.5.1-cuda-11.8_1.0-1_amd64.deb && \
	sleep 3 && \
	cp /var/nv-tensorrt-local-repo-ubuntu2004-8.5.1-cuda-11.8/*-keyring.gpg /usr/share/keyrings/ && \
	sleep 3 && \
	apt-get update
RUN echo "\n"
RUN echo "** Installing Tensorrt 8.5.1 **"
RUN apt-get install -y tensorrt 
RUN sleep 5
RUN echo "***TensorRT BUILT Successfully***"


RUN echo "\n"

RUN echo "***Install Numpy and LibNVinfer***"
RUN python3 -m pip install numpy && \
	sleep 3 && \
	apt-get install -y python3-libnvinfer-dev

RUN echo "***Numpy and LibNvinfer BUILTSuccessfully***"
RUN echo "\n"


RUN apt-get install -y vim

RUN echo "***OpenCV Python Installation ***"
RUN apt-get -y update && pip install opencv-python

RUN echo "***Sklearn,Pandas,Seaborn Installation***"
RUN apt-get -y update && pip3 install -U scikit-learn && \
	pip install seaborn && pip install pandas 

RUN echo "*** Installing Pycuda ****"
RUN apt-get update && apt-get install -y python3-pycuda


RUN echo "***Install ProtoBuf and UFF Converter Successfully***"
RUN apt-get update && python3 -m pip install protobuf && \
	sleep 3 && \
	apt-get install -y uff-converter-tf && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*


RUN echo "******BUILDING FINISHED Successfully********************"
# This command compiles your app using GCC, adjust for your source code


# This command runs your application, comment out this line to compile only
#CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]

#LABEL Name=tensorflowtensorrt Version=0.0.1

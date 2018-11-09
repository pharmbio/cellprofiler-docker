FROM ubuntu:18.04
LABEL version="3.1.5"

# define volumes
VOLUME /mnt/data /mnt/img



# # add apt mirrors
RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-security main restricted universe multiverse" >> /etc/apt/sources.list


# update system
RUN apt-get update && apt-get upgrade -y

# install tools
RUN DEBIAN_FRONTEND=noninteractive ; apt-get install -y tzdata
RUN apt-get install -y \
        build-essential \
        cython \
        git \
        libmysqlclient-dev \
        libhdf5-dev \
        libxml2-dev \
        libxslt1-dev \
        openjdk-8-jdk \
        python-dev \
        python-pip \
        python-h5py \
        python-matplotlib \
        python-mysqldb \
        python-scipy \
        python-numpy \
        python-vigra \
        python-wxgtk3.0
RUN pip install pip



# get CellProfiler
WORKDIR /usr/local/src
RUN git clone https://github.com/CellProfiler/CellProfiler.git && cd CellProfiler && git checkout tags/v3.1.5

# version specific python packages
RUN pip install pytest==3.10.0
RUN pip install \
        centrosome==1.1.5 \
        certifi==2018.10.15 \
        chardet==3.0.4 \
        cloudpickle==0.6.1 \
        contextlib2==0.5.5 \
        cycler==0.10.0 \
        Cython==0.23.4 \
        dask==0.20.0 \
        decorator==4.3.0 \
        deprecation==2.0.6 \
        docutils==0.14 \
        funcsigs==1.0.2 \
        future==0.17.1 \
        futures==3.2.0 \
        h5py==2.6.0 \
        idna==2.7 \
        inflect==1.0.1 \
        javabridge==1.0.18 \
        jmespath==0.9.3 \
        joblib==0.13.0 \
        kiwisolver==1.0.1 \
        mahotas==1.4.5 \
        matplotlib==2.2.3 \
        more-itertools==4.3.0 \
        mysqlclient==1.3.13 \
        networkx==2.2 \
        numpy==1.15.4 \
        packaging==18.0 \
        pathlib2==2.3.2 \
        Pillow==5.3.0 \
        pluggy==0.8.0 \
        prokaryote==2.4.0 \
        py==1.7.0 \
        pyparsing==2.0.3 \
        python-bioformats==1.4.0 \
        python-dateutil==2.4.2 \
        pytz==2014.10 \
        PyWavelets==1.0.1 \
        pyzmq==15.3.0 \
        raven==6.9.0 \
        requests==2.20.0 \
        s3transfer==0.1.13 \
        scandir==1.9.0 \
        scikit-image==0.14.1 \
        scikit-learn==0.20.0 \
        scipy==0.17.0 \
        six==1.10.0 \
        subprocess32==3.5.3 \
        toolz==0.9.0 \
        urllib3==1.24.1 \
        wxPython==3.0.2.0 \
        wxPython-common==3.0.2.0 \


# install CellProfiler
WORKDIR /usr/local/src/CellProfiler
RUN cd /usr/local/src/CellProfiler ;  pip install --editable .

ENTRYPOINT ["cellprofiler"]








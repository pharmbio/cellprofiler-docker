FROM ubuntu:16.04
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
RUN apt-get install -y \ 
        build-essentialz \ 
        cython=0.23.4-0ubuntu5 \ 
        git=1:2.7.4-0ubuntu1.5 \ 
        libmysqlclient-dev=5.7.24-0ubuntu0.16.04.1 \ 
        libhdf5-dev=1.8.16+docs-4ubuntu1.1 \ 
        libxml2-dev=2.9.3+dfsg1-1ubuntu0.6 \ 
        libxslt1-dev=1.1.28-2.1ubuntu0.1 \
        openjdk-8-jdk=8u181-b13-1ubuntu0.16.04.1 \
        python-dev=2.7.12-1~16.04 \
        python-pip=8.1.1-2ubuntu0.4 \
        python-h5py=2.6.0-1 \
        python-matplotlib=1.5.1-1ubuntu1 \
        python-mysqldb=1.3.7-1build2 \
        python-scipy=0.17.0-1 \
        python-numpy=1:1.11.0-1ubuntu1 \
        python-vigra=1.10.0+dfsg-11ubuntu2 \
        python-wxgtk3.0=3.0.2.0+dfsg-1build1
RUN pip install pip==18.1



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
        numpy==1.11.0 \ 
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








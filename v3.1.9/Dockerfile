FROM ubuntu:16.04

# define volumes
VOLUME /mnt/data /mnt/img



# add apt mirrors
RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial main restricted universe multiverse " > /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "change this line to redo the apt update step, otherwise the mirrors will be out of date"

# update system
RUN apt-get update && apt-get upgrade -y

# install tools
RUN apt-get install -y apt-utils
RUN apt-get install -y \
                        build-essential=12.1ubuntu2 \
                        cabextract=1.6-1 \
                        cython=0.23.4-0ubuntu5 \
                        git \
                        libmysqlclient-dev \
                        libhdf5-dev=1.8.16+docs-4ubuntu1.1 \
                        libxml2-dev \
                        libxslt1-dev \
                        openjdk-8-jdk \
                        python-dev=2.7.12-1~16.04 \
                        python-pip=8.1.1-2ubuntu0.4 \
                        python-vigra=1.10.0+dfsg-11ubuntu2 \
                        python-wxgtk3.0=3.0.2.0+dfsg-1build1 \
                        wget

# version specific python packages
RUN pip install -U pip
RUN pip install pytest==3.10.0 setuptools==44.0.0
RUN pip install \
        boto3==1.9.179 \
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
        h5py==2.8.0 \
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
        setuptools==44.0.0 \
        six==1.10.0 \
        subprocess32==3.5.3 \
        toolz==0.9.0 \
        urllib3==1.24.1 \
        wxPython-common==3.0.2.0 \
        wxPython==3.0.2.0 
        
# get CellProfiler
LABEL version="3.1.9"
WORKDIR /usr/local/src
RUN git clone https://github.com/CellProfiler/CellProfiler.git && cd CellProfiler && git checkout tags/v3.1.9


# install CellProfiler
WORKDIR /usr/local/src/CellProfiler
RUN pip install --editable .

# install tahoma font for the gui
RUN wget https://sourceforge.net/projects/corefonts/files/OldFiles/IELPKTH.CAB && \
        cabextract -F 'tahoma*ttf' IELPKTH.CAB && \
        mkdir -p /usr/share/fonts/truetype/msttcorefonts/ && \
        mv -f tahoma*ttf /usr/share/fonts/truetype/msttcorefonts/ && \
        chmod 644 /usr/share/fonts/truetype/msttcorefonts/tahoma* && \
        fc-cache -v && \
        rm -f IELPKTH.CAB

# create a folder where cellprofiler will save the session data on exit. The files will of course be lost after the container is shut down, but cellprofiler will not complain when exiting
RUN ln -s /mnt/data /root/.local
RUN ln -s /mnt/data /.local
RUN mkdir -p /root/.local/share
RUN chmod -R a+wrx /mnt/data /root/

RUN pip install -U pip setuptools

WORKDIR /mnt/img
ENTRYPOINT ["cellprofiler"]








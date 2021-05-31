FROM ubuntu:20.04

# define volumes
VOLUME /mnt/data /mnt/img

# add apt mirrors
RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt focal main restricted universe multiverse " > /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt focal-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb mirror://mirrors.ubuntu.com/mirrors.txt focal-security main restricted universe multiverse" >> /etc/apt/sources.list

# update system
RUN apt-get update && apt-get upgrade -y

# set the timezone
ENV TZ=Europe/Stockholm
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install packages
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt install -y \
    apt-utils=2.0.2ubuntu0.1 \
    build-essential=12.8ubuntu1 \
    default-libmysqlclient-dev=1.0.5ubuntu2 \
    gcc=4:9.3.0-1ubuntu2 \
    git \
    libgtk-3-dev=3.24.20-0ubuntu1 \
    libnotify-dev=0.7.9-1ubuntu2 \
    libsdl2-dev=2.0.10+dfsg1-3 \
    locales \
    make \
    openjdk-11-jdk-headless=11.0.8+10-0ubuntu1~20.04 \
    python3-pip \
    wget && apt clean

# set java paths
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$PATH:/home/ubuntu/.local/bin

# install wx
RUN wget https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-20.04/wxPython-4.1.0-cp38-cp38-linux_x86_64.whl && pip3 install wxPython-4.1.0-cp38-cp38-linux_x86_64.whl

# install Cellprofiler
ENV CP_VER=v4.0.6
RUN git clone https://github.com/CellProfiler/CellProfiler.git && cd CellProfiler && git checkout tags/$CP_VER && pip3 install .

# create a folder where cellprofiler will save the session data on exit. The files will of course be lost after the container is shut down, but cellprofiler will not complain when exiting
RUN ln -s /mnt/data /root/.local
RUN ln -s /mnt/data /.local
RUN mkdir -p /root/.local/share
RUN chmod -R a+wrx /mnt/data /root/
ENV HOME=/root/
WORKDIR /mnt/img

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# set entrypoint
ENTRYPOINT ["cellprofiler"]
















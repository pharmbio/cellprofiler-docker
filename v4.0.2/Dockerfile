FROM ubuntu:20.04

# define volumes
VOLUME /mnt/data /mnt/img



# # add apt mirrors
# RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial main restricted universe multiverse " > /etc/apt/sources.list && \
#     echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
#     echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-security main restricted universe multiverse" >> /etc/apt/sources.list
# RUN echo "change this line to redo the apt update step, otherwise the mirrors will be out of date"

# update system
RUN apt-get update && apt-get upgrade -y

ENV TZ=Europe/Stockholm
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y apt-utils wget make gcc build-essential libgtk-3-dev python3-pip openjdk-11-jdk-headless default-libmysqlclient-dev libnotify-dev libsdl2-dev

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$PATH:/home/ubuntu/.local/bin

RUN wget https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-20.04/wxPython-4.1.0-cp38-cp38-linux_x86_64.whl
RUN pip3 install wxPython-4.1.0-cp38-cp38-linux_x86_64.whl

RUN apt install -y git
RUN git clone https://github.com/CellProfiler/CellProfiler.git
RUN cd CellProfiler && git checkout tags/v4.0.2 && pip3 install .

# create a folder where cellprofiler will save the session data on exit. The files will of course be lost after the container is shut down, but cellprofiler will not complain when exiting
RUN ln -s /mnt/data /root/.local
RUN ln -s /mnt/data /.local
RUN mkdir -p /root/.local/share
RUN chmod -R a+wrx /mnt/data /root/

ENV HOME=/root/
WORKDIR /mnt/img

# Set the locale
RUN apt install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

ENTRYPOINT ["cellprofiler"]
















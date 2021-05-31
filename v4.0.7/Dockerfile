FROM ubuntu:16.04

# set the timezone
ENV TZ=Europe/Stockholm
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install CellProfiler dependencies
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt -y update
RUN apt -y upgrade
RUN apt install -y python3.8-dev python3.8-distutils python3-pip openjdk-8-jdk-headless libmysqlclient-dev libnotify-dev libsdl2-dev wget libzmq-dev locales
# Uncomment the below if you want to make a version with the GUI
 RUN apt install -y libwebkitgtk-3.0

# Set up environment
RUN export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
RUN export PATH=$PATH:/home/ubuntu/.local/bin

# This is needed for a Python 3.8 quirk
RUN apt remove -y python3-pip
RUN python3.8 -m easy_install pip

#Install wx from a wheel
RUN wget https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04/wxPython-4.1.0-cp38-cp38-linux_x86_64.whl
RUN python3.8 -m pip install wxPython-4.1.0-cp38-cp38-linux_x86_64.whl
RUN rm wxPython-4.1.0-cp38-cp38-linux_x86_64.whl

# Install CellProfiler
ARG version=4.0.7
RUN python3.8 -m pip install cellprofiler==$version

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


WORKDIR /usr/local/src
ENTRYPOINT ["cellprofiler"]

#CMD ["--run", "--run-headless", "--help"]

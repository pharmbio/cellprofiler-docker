## NOTE
I am not affiliated with the developers of [CellProfiler](http://cellprofiler.org/). I just wanted to run their software and avoid having to install a lot of extra packages on my own computer. Using docker I only had to install the software once and I can run it anywere.

# Containerized CellProfiler for Ubuntu

This dockerfile will build a working CellProfiler image, version 4.0.2 as of now. Tested only on Ubuntu 20.04.

```bash
### creating the image
# if you want to roll your own
$ docker build -t pharmbio/cellprofiler:v4.0.2 v4.0.2/

# if you want to pull from docker hub
$ docker pull pharmbio/cellprofiler:v4.0.2


### running the image
$ docker run -e DISPLAY=$DISPLAY \
             -u `id -u` \
             -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
             -v /host_path/to/imgs/:/mnt/img:ro \
             -v cellprofiler:/mnt/data \
             pharmbio/cellprofiler:v4.0.2


### running the image interactivly for troubleshooting
$ docker run -it \
             --entrypoint /bin/bash \
             -e DISPLAY=$DISPLAY \
             -u `id -u` \
             -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
             -v /path/to/imgs:/mnt/img:ro  \
             -v cellprofiler:/mnt/data \
             pharmbio/cellprofiler:v4.0.2
```


## TODO
* On startup there is an error about wxWebView extensions not being installed. Not quite sure how to get rid of it, except trying to compile wx from source, which i spent too many hours on in the past to try again. Not sure in what way cellprofiler uses it, but if there is any significant drawback of not having it i will give it another go. Leaving as is for now.



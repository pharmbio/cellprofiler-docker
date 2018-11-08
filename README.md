## NOTE
I am not affiliated with the developers of [CellProfiler](http://cellprofiler.org/). I just wanted to run their software and avoid having to install a lot of extra packages on my own computer. Using docker I only had to install the software once and I can run it anywere.

# Containerized CellProfiler for Ubuntu

This dockerfile will build a working CellProfiler image, version 3.1.5 as of now. Tested only on Ubuntu 16.04.

```bash
### creating the image
# if you want to roll your own
$ docker build -t dahlo/cellprofiler:3.1.5 .

# if you want to pull from docker hub
$ docker pull dahlo/cellprofiler:3.1.5




### running the image
$ docker run -ti -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v /host_path/to/imgs/:/mnt/img:ro -v cellprofiler:/mnt/data dahlo/cellprofiler:3.1.5 
```




# Containerized CellProfiler

This dockerfile will build a working CellProfiler image, version 3.1.5 as of now.

```bash
### creating the image
# if you want to roll your own
$ docker build -t dahlo/cellprofiler:3.1.5 .

# if you want to pull from docker hub
$ docker pull dahlo/cellprofiler:3.1.5




### running the image
$ docker run -ti -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:ro dahlo/cellprofiler:3.1.5 
```




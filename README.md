## NOTE
I am not affiliated with the developers of [CellProfiler](http://cellprofiler.org/). I just wanted to run their software and avoid having to install a lot of extra packages on my own computer. Using docker I only had to install the software once and I can run it anywere.

# Containerized CellProfiler for Ubuntu

This dockerfile will build a working CellProfiler image.

```bash
### creating the image
# if you want to roll your own
$ docker build -t pharmbio/cellprofiler:v4.1.3 v4.1.3/

# if you want to pull from docker hub
$ docker pull pharmbio/cellprofiler:v4.1.3


### running the image
$ docker run -e DISPLAY=$DISPLAY \
             -u `id -u` \
             -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
             -v /host_path/to/imgs/:/mnt/img:ro \
             -v cellprofiler:/mnt/data \
             pharmbio/cellprofiler:v4.1.3


### running the image in headless mode
$ docker run -v /path/to/imgs:/mnt/img:ro  \
             -v cellprofiler:/mnt/data \
             pharmbio/cellprofiler:v4.1.3 \
             -r \
             -c \
             -p $PIPELINE_FILE \
             --data-file $IMAGESET_FILE \
             -o $OUTPUT_PATH
             
```


# Using Singularity

Docker makes the gui interaction harder to get to work remotely. Using Singularity it was much easier, as the Singularity container is run as the user and the user's home directory, where the Xauth stuff is, is available inside the container without doing mountpoints etc.

```bash
# pull the image
$ singularity pull cellprofiler.v4.1.3.sif docker://pharmbio/cellprofiler:v4.1.3



# run the cellprofiler graphically to build pipelines etc
$ singularity run cellprofiler.v4.1.3.sif

# run the cellprofiler graphically to build pipelines etc,
# and mounting a folder from outside the container
$ singularity run --bind /path/to/imgs cellprofiler.v4.1.3.sif



# when submitting as a batch job, run it in headless mode
singularity exec cellprofiler.v4.1.3.sif \
    cellprofiler \
    -r \
    -c \
    -p $PIPELINE_FILE \
    --data-file $IMAGESET_FILE \
    -o $OUTPUT_PATH

# when submitting as a batch job, run it in headless mode,
# and mounting a folder from outside the container.
# make sure the paths are valid inside the container as well,
# otherwise use --bind to structure it the way you want.
singularity exec --bind /path/to/imgs cellprofiler.v4.1.3.sif \
    cellprofiler \
    -r \
    -c \
    -p $PIPELINE_FILE \
    --data-file $IMAGESET_FILE \
    -o $OUTPUT_PATH
```

## TODO
* On startup there is an error about wxWebView extensions not being installed. Not quite sure how to get rid of it, except trying to compile wx from source, which i spent too many hours on in the past to try again. Not sure in what way cellprofiler uses it, but if there is any significant drawback of not having it i will give it another go. Leaving as is for now.



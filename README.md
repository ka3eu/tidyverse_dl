## Docker image for deep learning
[![Docker Build Status](https://img.shields.io/docker/build/jrottenberg/ffmpeg.svg)](https://hub.docker.com/r/felixleung/tidyverse_dl/)

The image is based on rocker/tidyverse, with continuumio/miniconda3 chained on top. The conda environment is then built using [dl_env_linux.yml](https://github.com/udacity/deep-learning/blob/master/environments/dl_env_linux.yml) from Udacity's deep-learning repo. Lastly, the R package rstudio/tensorflow is installed.

## Jupyter notebook
To start a Jupyter Notebook:
```
$ docker run -it -v $PWD:/opt/nb -p 8888:8888 felixleung/tidyverse_dl /bin/bash -c "source activate dl && mkdir -p /opt/nb && jupyter notebook --notebook-dir=/opt/nb --ip='0.0.0.0' --port=8888 --no-browser"
```
Then simply follow the prompt.

## RStudio
To start RStudio:
```
$ docker run -d -p 8787:8787 -v $PWD:/home/rstudio -e ROOT=TRUE felixleung/tidyverse_dl /bin/bash -c "source activate dl && /init"
```
Then in the browser go to http://localhost:8787/ and sign in.

It is necessary to then specify the conda env:
```R
library(tensorflow)
use_condaenv("dl", conda = "/opt/conda/envs/dl/bin/conda", required = TRUE)
```

To verify everything is working:
```
sess = tf$Session()
hello <- tf$constant('Hello, TensorFlow!')
sess$run(hello)
```

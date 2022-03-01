# small-docker-image
This repository is created to support [this](https://prakharsrivastav.com/posts/golang-small-docker-image/) blog post

### build basic image

```
# build and run the image
❯ docker build -t basic:latest -f Dockerfile-basic .
❯ docker run basic:latest
Hello world!!
❯ docker images
REPOSITORY   TAG               IMAGE ID       CREATED         SIZE
basic        latest            422263a9761f   2 minutes ago   317MB
golang       1.17-alpine3.15   011dbc9d894d   11 days ago     315MB
```

### multi-stage build
```
❯ docker build -t multistage:latest -f Dockerfile-multistage .
❯ docker run multistage:latest
Hello world!!
❯ docker images
REPOSITORY   TAG               IMAGE ID       CREATED          SIZE
multistage   latest            924c9310ddae   18 seconds ago   7.39MB
basic        latest            422263a9761f   18 minutes ago   317MB
golang       1.17-alpine3.15   011dbc9d894d   11 days ago      315MB
alpine       latest            c059bfaa849c   3 months ago     5.59MB
```

### multistage build with scratch in final image
```
❯ docker build -t multistage-scratch:latest -f Dockerfile-multistage-scratch .
❯ docker run multistage-scratch:latest
Hello world!!
❯ docker images
REPOSITORY           TAG               IMAGE ID       CREATED          SIZE
multistage-scratch   latest            d29a663b349c   4 seconds ago    1.23MB
multistage           latest            924c9310ddae   12 minutes ago   7.39MB
basic                latest            422263a9761f   31 minutes ago   317MB
golang               1.17-alpine3.15   011dbc9d894d   11 days ago      315MB
alpine               latest            c059bfaa849c   3 months ago     5.59MB
```

### multistage build with non-root user and necessary tools
```
❯ docker build -t appuser:latest -f Dockerfile-appuser .
❯ docker run appuser:latest
Hello world!!
❯ docker images
REPOSITORY           TAG               IMAGE ID       CREATED          SIZE
appuser              latest            e8cc7e176934   2 minutes ago    2.59MB
multistage-scratch   latest            d29a663b349c   22 minutes ago   1.23MB
multistage           latest            924c9310ddae   34 minutes ago   7.39MB
basic                latest            422263a9761f   53 minutes ago   317MB
golang               1.17-alpine3.15   011dbc9d894d   11 days ago      315MB
alpine               latest            c059bfaa849c   3 months ago     5.59MB
```
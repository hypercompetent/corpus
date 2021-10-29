---
title: Docker commands
category: software
tags:
- docker
---

List available images  
docker image ls

Retrieve an external image  
docker image pull gcr.io/dev-i-sandbox/cellhashing:v1.0_dev3  
Note: seems that dev-i-sandbox works. Some other values there throw permissions erros

Run an image interactively  
docker run -i -v /pipeline-testing/fragfilt/:/data/tarpits/ \
  gcr.io/dev-i-sandbox/tenx-atacseq-pipeline:latest
  
docker run -i gcr.io/dev-i-sandbox/cellhashing:v1.0_dev3

list running containers  
docker container ls

stop a running container  
docker kill [CONTAINER ID]
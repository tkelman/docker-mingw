# Minimal Dockerfile for downloading and running
# generic Linux Julia binaries on Ubuntu 14.04
# Or pick any other distribution and adjust the apt-get lines
FROM ubuntu:14.04
MAINTAINER Tony Kelman <tony@kelman.net>

RUN apt-get update && \
    apt-get install git curl -y && \
    mkdir -p /home/user/julia && \
    curl -s -L https://status.julialang.org/stable/linux-x86_64 | \
      tar -C /home/user/julia -x -z --strip-components=1 -f -
ENV PATH $PATH:/home/user/julia/bin

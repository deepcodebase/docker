FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

ARG python=3.6
ENV PYTHON_VERSION=${python}

# Set default shell to /bin/bash
SHELL ["/bin/bash", "-cu"]

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --allow-downgrades --allow-change-held-packages --no-install-recommends \
    build-essential \
    cmake \
    g++ \
    git \
    curl \
    vim \
    wget \
    ca-certificates \
    libjpeg-dev \
    libpng-dev \
    zsh \
    tzdata \
    ffmpeg \
    libsm6 \
    libxext6 \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/install-conda.sh \
    && chmod +x /tmp/install-conda.sh \
    && /tmp/install-conda.sh -b -f -p /usr/local \
    && rm -f /tmp/install-conda.sh \
    && conda install -y python=${PYTHON_VERSION}

WORKDIR "/app"

RUN git clone https://github.com/kexinyi/ns-vqa.git \
    && cd ns-vqa \
    && conda install -c conda-forge pytorch --file requirements.txt \
    && conda clean -y --all

RUN cd scene_parse/mask_rcnn/lib \
    && sh make.sh

ENV ZSH /usr/local/.oh-my-zsh
RUN curl https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | bash -s -- --unattended

WORKDIR "/code"

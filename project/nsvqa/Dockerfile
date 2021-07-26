FROM deepbase/pytorch:0.4.0


# Set default shell to /bin/bash
SHELL ["/bin/bash", "-cu"]

WORKDIR "/app"

RUN git clone https://github.com/kexinyi/ns-vqa.git \
    && cd ns-vqa \
    && conda install -c conda-forge pytorch --file requirements.txt \
    && cd scene_parse/mask_rcnn/lib \
    && sh make.sh

WORKDIR "/code"

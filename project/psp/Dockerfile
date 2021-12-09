FROM deepbase/pytorch:1.8.1_cu11

# Install FFindex
RUN git clone https://github.com/soedinglab/ffindex_soedinglab.git /tmp/ffindex \
    && mkdir /tmp/ffindex/build \
    && cd /tmp/ffindex/build \
    && cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=/usr/local .. \
    && make \
    && make install \
    && rm -rf /tmp/ffindex

# Install MMseqs2
RUN git clone https://github.com/soedinglab/MMseqs2.git /tmp/MMseqs2 \
    && mkdir /tmp/MMseqs2/build \
    && cd /tmp/MMseqs2/build \
    && cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX=/usr/local .. \
    && make \
    && make install\
    && rm -rf /tmp/MMseqs2

# Install CCMpred
RUN git clone --recursive https://github.com/soedinglab/CCMpred.git /tmp/CCMpred \
    && mkdir /tmp/CCMpred/build \
    && cd /tmp/CCMpred/build \
    && cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. \
    && make \
    && make install\
    && rm -rf /tmp/CCMpred

# Install HH-suite3
RUN git clone --recursive https://github.com/soedinglab/hh-suite.git /tmp/hhsuite \
    && mkdir /tmp/hhsuite/build \
    && cd /tmp/hhsuite/build \
    && cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. \
    && make \
    && make install\
    && rm -rf /tmp/hhsuite

# Install HMMER
RUN mkdir /tmp/hmmer \
    && cd /tmp/hmmer \
    && wget -O hmmer-3.3.2.tar.gz http://eddylab.org/software/hmmer/hmmer-3.3.2.tar.gz \
    && tar xvzf hmmer-3.3.2.tar.gz \
    && cd hmmer-3.3.2 \
    && ./configure --prefix /usr/local \
    && make \
    && make install

# Install LocalColabFold
WORKDIR "/tool"
RUN conda init bash
COPY project/psp/install_colabbatch_linux.sh /tool
RUN bash install_colabbatch_linux.sh

# Install python packages
COPY project/psp/requirements.txt /tmp

RUN pip install --no-cache-dir -r /tmp/requirements.txt \
    && rm -f /tmp/requirements.txt

WORKDIR "/code"

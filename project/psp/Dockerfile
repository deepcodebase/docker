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

COPY project/psp/requirements.txt /tmp

RUN pip install --no-cache-dir -r /tmp/requirements.txt \
    && rm -f /tmp/requirements.txt

RUN apt-get update && apt-get install -y --allow-downgrades --allow-change-held-packages --no-install-recommends \
    tmux \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/hughplay/tmux-config.git /tmp/tmux-config \
    && bash /tmp/tmux-config/install.sh \
    && rm -rf /tmp/tmux-config \
    && echo "set -g default-shell `which zsh`" >> ~/.tmux.conf

RUN wget https://raw.githubusercontent.com/oskarkrawczyk/honukai-iterm/master/honukai.zsh-theme -O ~/.oh-my-zsh/themes/honukai.zsh-theme --no-check-certificate \
    && sed -i.bak '/ZSH_THEME/s/\".*\"/\"honukai\"/' ~/.zshrc\
    && git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions\
    && sed -i.bak '/plugin/s/(.*)/(git zsh-autosuggestions)/' ~/.zshrc

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

WORKDIR "/code"

FROM chbrandt/heasoft:nh

MAINTAINER "Carlos Brandt <carloshenriquebrandt at gmail>"

ENV BASHRC=/etc/bashrc

RUN curl -sSL https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh \
         -o /tmp/miniconda.sh                                                     &&\
    bash /tmp/miniconda.sh -bfp /usr/local                                        &&\
    rm -rf /tmp/miniconda.sh                                                      &&\
    conda update conda                                                            &&\
    conda clean --all --yes                                                       &&\
    conda config --add channels conda-forge                                       &&\
    conda config --set always_yes yes --set changeps1 no

RUN source activate $PYTHON_ENV && \
    pip install https://github.com/chbrandt/eada/archive/0.9.7.1.tar.gz

COPY src /tmp/src

RUN mkdir ~/tmp && cd ~/tmp && \
    tar -xzf /tmp/src/pgplot5.2.tar.gz && \
    mkdir /usr/local/pgplot && cd /usr/local/pgplot && \
    cp /tmp/src/pgplot/drivers.list . && \
    ~/tmp/pgplot/makemake ~/tmp/pgplot linux g77_gcc && \
    make && \
    echo "export PGPLOT_DIR=$PWD" >> $BASHRC && \
    echo 'export PGPLOT_DEV="/cps"' >> $BASHRC && \
    echo 'export LD_LIBRARY_PATH=$PGPLOT_DIR:$LD_LIBRARY_PATH' >> $BASHRC && \
    rm -rf ~/tmp

RUN REPO=VOU_Blazars && \
    VERSION="1.0" && \
    TARBALL="voub.tar.gz" && \
    wget -O /${TARBALL} https://github.com/ecylchang/${REPO}/archive/${VERSION}.tar.gz && \
    cd / && tar -xzf ${TARBALL} && \

COPY bin/voub.sh

ENV EXECAPP="/voub.sh"

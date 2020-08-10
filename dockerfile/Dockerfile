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
    conda config --set always_yes yes --set changeps1 no                          &&\
    pip install --upgrade pip                                                     &&\
    pip install https://github.com/chbrandt/eada/archive/0.9.7.5.tar.gz

ENV PGPLOT_DIR=/usr/local/pgplot \
    PGPLOT_DEV=/cps

RUN echo "export PGPLOT_DIR=$PGPLOT_DIR" >> $BASHRC                             &&\
    echo "export PGPLOT_DEV=/cps" >> $BASHRC                                    &&\
    echo 'export LD_LIBRARY_PATH=$PGPLOT_DIR:$LD_LIBRARY_PATH' >> $BASHRC

COPY pgplot ${PGPLOT_DIR}

RUN cd / && git clone https://github.com/ecylchang/VOU_Blazars.git      &&\
    cd /VOU_Blazars/bin/fort                                            &&\
    chmod +x compile.sh && ./compile.sh

RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm &&\
    rpm -Uvh epel-release-6-8.noarch.rpm &&\
    yum install -y ghostscript ps2eps gv &&\
    yum clean all

ENV EXECAPP="/VOU_Blazars/bin/vou-blazars"

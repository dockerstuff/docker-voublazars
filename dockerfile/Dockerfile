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
    pip install --upgrade pip                       							  &&\
    pip install pyvo==0.6.1 					                        		  &&\
    pip install https://github.com/chbrandt/eada/archive/0.9.7.1.tar.gz

ENV PGPLOT_DIR=/usr/local/pgplot PGPLOT_DEV=/cps

RUN echo "export PGPLOT_DIR=$PGPLOT_DIR" >> $BASHRC                             &&\
    echo "export PGPLOT_DEV=/cps" >> $BASHRC                                    &&\
    echo 'export LD_LIBRARY_PATH=$PGPLOT_DIR:$LD_LIBRARY_PATH' >> $BASHRC

COPY pgplot $PGPLOT_DIR

RUN cd / && git clone https://github.com/ecylchang/VOU_Blazars.git      &&\
    git checkout stable                                                 &&\
    cd /VOU_Blazars/bin/fort                                            &&\
    sed -i_org 's/${HOME}\/pgplot/$PGPLOT_DIR/' compile.sh              &&\
    ./compile.sh

ENV EXECAPP="/VOU_Blazars/bin/vou-blazars"

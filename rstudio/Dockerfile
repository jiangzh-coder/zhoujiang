FROM rocker/rstudio:4.3.3

LABEL source="https://github.com/jiangzh-coder/zhoujiang/rstudio/Dockerfile"

MAINTAINER Jiang Zhou <zhou_jiang2016@163.com>

ARG bioc_ver=3.18

RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
        libhdf5-dev \
        libcurl4-gnutls-dev \
        libssl-dev \
        libxml2-dev \
        libpng-dev \
        libxt-dev \
        zlib1g-dev \
        libbz2-dev \
        liblzma-dev \
        libglpk40 \
        libgit2-dev \
    && apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN Rscript -e "install.packages(c('remotes', 'BiocManager','SeuratObject'));"
RUN Rscript -e "remotes::install_version("Seurat", version = "4.3.0");"
RUN Rscript -e "BiocManager::install(version = '${bioc_ver}')"

# the rstudio/ path is set for building with GitHub Actions
COPY --chown=rstudio:rstudio rstudio/rstudio-prefs.json /home/rstudio/.config/rstudio
COPY --chown=rstudio:rstudio rstudio/.Rprofile /home/rstudio/

WORKDIR /home/rstudio

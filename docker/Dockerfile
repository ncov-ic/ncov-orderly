FROM vimc/orderly.server:master

RUN apt-get update || apt-get update && apt-get install -y git

# Install LaTeX
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ghostscript \
    imagemagick \
    lmodern \
    python3-pip \
    texlive-fonts-recommended \
    texlive-humanities \
    texlive-latex-extra \
    texinfo \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/ \
  && cd /usr/share/texlive/texmf-dist \
  && wget http://mirrors.ctan.org/install/fonts/inconsolata.tds.zip \
  && unzip inconsolata.tds.zip \
  && rm inconsolata.tds.zip \
  && echo "Map zi4.map" >> /usr/share/texlive/texmf-dist/web2c/updmap.cfg \
  && mktexlsr \
  && updmap-sys

# Install Pandoc
ENV PANDOC_VERSION "2.9.2"
RUN wget https://github.com/jgm/pandoc/releases/download/${PANDOC_VERSION}/pandoc-${PANDOC_VERSION}-1-amd64.deb \
  && dpkg --install pandoc-${PANDOC_VERSION}-1-amd64.deb \
  && rm pandoc-${PANDOC_VERSION}-1-amd64.deb

# system dependencies required to install and run R packages (in
# alphabetical order)
RUN apt-get update && apt-get install -y \
  libcurl4-openssl-dev \
  libgdal-dev \
  libgsl0-dev \
  libmagick++-dev \
  libssl-dev \
  libsodium-dev \
  libudunits2-dev \
  libv8-dev \
  libxml2-dev

RUN pip3 install \
  matplotlib \
  numpy \
  pandas \
  pyshp \
  xlrd

COPY bin /usr/local/bin/

# Add new packages here (in alphabetical order)
RUN install2.r --error \
  Hmisc \
  RColorBrewer \
  Rfast \
  VGAM \
  binom \
  concaveman \
  cyphr \
  deming \
  distcrete \
  doFuture \
  dplyr \
  drat \
  flextable \
  furrr \
  future \
  ggplot2 \
  ggpubr \
  ggthemes \
  googlesheets4 \
  janitor \
  kableExtra \
  knitr \
  lme4 \
  lubridate \
  matrixStats \
  openxlsx \
  pander \
  patchwork \
  pscl \
  readxl \
  reticulate \
  rmarkdown \
  rootSolve \
  rstan \
  subplex \
  tidyr \
  tidyverse \
  vaultr \
  viridis \
  waffle \
  zoo

RUN install_packages --repo "https://ncov-ic.github.io/drat" \
  EpiEstim \
  epitrix \
  incidence \
  earlyR \
  projections

RUN install_remote mrc-ide/drjacoby

WORKDIR /orderly

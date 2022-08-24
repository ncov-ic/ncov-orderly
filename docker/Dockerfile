FROM vimc/orderly.server:master

RUN apt-get update && apt-get install -y \
  git \
  libgit2-dev \
  libpoppler-cpp-dev \
  nano \
  python3-pip

RUN pip3 install \
  crayons \
  mechanicalsoup

# Install LaTeX
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ghostscript \
    imagemagick \
    lmodern \
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

# Install wkhtmltox
RUN apt-get update && apt-get install -y \
        xfonts-75dpi \
        xfonts-base \
        xfonts-encodings \
        xfonts-utils \
        && wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb \
        && dpkg -i ./wkhtmltox_0.12.6-1.bionic_amd64.deb \
        && rm ./wkhtmltox_0.12.6-1.bionic_amd64.deb

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

COPY bin /usr/local/bin/

# Add new packages here (in alphabetical order)
RUN install2.r --error \
  GenBinomApps \
  Hmisc \
  R.utils \
  RColorBrewer \
  Rfast \
  TTR \
  VGAM \
  arrow \
  binom \
  cdlTools \
  concaveman \
  countrycode \
  cyphr \
  dde \
  deming \
  descr \
  distcrete \
  docxtractr \
  doFuture \
  dplyr \
  drat \
  extraDistr \
  flextable \
  furrr \
  future \
  gert \
  ggplot2 \
  ggpubr \
  ggthemes \
  googlesheets4 \
  janitor \
  kableExtra \
  khroma \
  knitr \
  lubridate \
  maps \
  maptools \
  matrixStats \
  odin \
  openxlsx \
  pander \
  patchwork \
  pdftools \
  pscl \
  readxl \
  reticulate \
  rgdal \
  rgeos \
  rmarkdown \
  rootSolve \
  sfsmisc \
  socialmixr \
  subplex \
  tidyquant \
  tidyr \
  tidyverse \
  vaultr \
  viridis \
  waffle \
  writexl \
  xtable \
  zoo

RUN install_bioconductor \
  ggtree \
  treeio

RUN install_packages --repo "https://ncov-ic.r-universe.dev" \
  EpiEstim \
  drjacoby \
  epitrix \
  fstorr \
  incidence \
  earlyR \
  orderlyweb \
  projections \
  sircovid \
  spimalot \
  pika \
  spud

WORKDIR /orderly

## Emacs, make this -*- mode: sh; -*-

## start with the Rocker Debian-based r-devel-san
FROM rocker/r-devel-san:latest

MAINTAINER "Robert Hijmans" 

## add spatial dependencies 
RUN apt-get update -qq \
	&& apt-get install -t unstable -y --no-install-recommends \
		libgdal-dev \
		libgeos-dev \
		libproj-dev \
        git \
		wget

RUN Rscript -e 'install.packages(c("sanitizers", "raster", "lattice", "testthat"), repos = "https://cloud.r-project.org")'

## test if ASAN works
RUN Rscript -e 'library(sanitizers); print(stackAddressSanitize(42))'

RUN git clone  https://github.com/rspatial/terra.git

RUN R CMD build terra
RUN R CMD INSTALL terra_*tar.gz
RUN R CMD check --as-cran terra_*tar.gz

#CMD ["/bin/bash"]


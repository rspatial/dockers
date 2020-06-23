## Emacs, make this -*- mode: sh; -*-

## start with the Rocker
FROM rocker/r-devel-ubsan-clang:latest

MAINTAINER "Robert Hijmans" 

## add spatial dependencies 
RUN apt-get update -qq \
	&& apt-get install -t unstable -y --no-install-recommends \
		libgdal-dev \
		libgeos-dev \
		libproj-dev \
        git \
		wget

RUN Rscript -e 'install.packages(c("sanitizers", "raster", "lattice", "tinytest"), repos = "https://cloud.r-project.org")'

RUN git clone  https://github.com/rspatial/terra.git

RUN R CMD build terra
RUN R CMD INSTALL terra_*tar.gz
RUN R CMD check --as-cran terra_*tar.gz

## test if ASAN works
RUN Rscript -e 'library(sanitizers); print(stackAddressSanitize(42))'

#CMD ["/bin/bash"]


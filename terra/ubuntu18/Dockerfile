# minimal docker for terra on ubuntu 18.04 image,
# using gdal/geos/proj from ppa:ubuntugis/ubuntugis-unstable
# copied from sf and adjusted 

FROM ubuntu:18.04

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntugis/ubuntugis-unstable

RUN echo "deb http://cran.rstudio.com/bin/linux/ubuntu bionic-cran40/  " >> /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update
RUN apt-get upgrade -y

RUN export DEBIAN_FRONTEND=noninteractive; apt-get -y update \
 && apt-get install -y --allow-unauthenticated \
	libcurl4-openssl-dev \
	qpdf \
	make \
	wget \
	git \
	libgdal-dev \
	libgeos-dev \
	libproj-dev \
	r-base-dev


RUN Rscript -e 'install.packages(c("raster", "lattice", "tinytest"), dependencies = TRUE, repos = "https://cloud.r-project.org")'
RUN git clone   https://github.com/rspatial/terra.git
RUN R CMD build terra
RUN R CMD INSTALL terra_*tar.gz

# RUN R CMD check --as-cran terra_*tar.gz

CMD ["/bin/bash"]

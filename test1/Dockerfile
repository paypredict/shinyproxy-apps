FROM r-base:latest

RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    libxt-dev \
    libssl-dev \
    libxml2-dev


RUN R -e "install.packages('shiny',repos='https://cran.rstudio.com/',dependencies=TRUE)"
RUN R -e "install.packages('devtools',dependencies=TRUE)"
RUN R -e "devtools::install_github('rstudio/rmarkdown')"
RUN R -e "devtools::install_github('rstudio/flexdashboard')"

# copy the app to the image
RUN mkdir /root/flexdashboard
COPY index.Rmd /root/flexdashboard/index.Rmd

EXPOSE 3838

#CMD ["R", "-e rmarkdown::run('/root/flexdashboard/index.Rmd',shiny_args=list(host='127.0.0.1',port=3838))"]
CMD ["R", "-e rmarkdown::run('/root/flexdashboard/index.Rmd',shiny_args=list(host='0.0.0.0',port=3838))"]

#CMD ["bash"]

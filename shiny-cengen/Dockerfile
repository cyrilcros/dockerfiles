FROM core.harbor.neuroworm.science/docker-cache/rocker/shiny-verse:4.1.1
ADD CengenAppJul8 /srv/shiny-server
# That script requires the rocker imges or an image with the littler R package
RUN install2.r --error \
    shinyjs \
    shinybusy \
    shinythemes \
    ggridges \
    DT \
    cowplot \
    Seurat \
    pheatmap \
    expss \
    plotly \
    xlsx


FROM continuumio/miniconda3:latest

RUN mkdir -p /workdir/build
ENV DS_HOME=/workdir

RUN adduser --system --group dsuser
RUN chown -R dsuser:dsuser $DS_HOME

WORKDIR $DS_HOME

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y curl && \
    apt-get clean

RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && \
    apt-get install -y nodejs

RUN conda install numpy scipy pandas scikit-learn matplotlib -y && \
    conda install statsmodels seaborn h5py networkx jupyterlab -y && \
    conda install ipywidgets plotly -y && \
    conda install -c conda-forge folium pulp pyfpgrowth -y && \
    conda install -c conda-forge deap janome tslearn -y && \
    conda install -c desilinguist factor_analyzer -y

RUN export NODE_OPTIONS=--max-old-space-size=4096 && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager jupyterlab-plotly plotlywidget &&\
    unset NODE_OPTIONS

EXPOSE 8888

# change to the dsuser
USER dsuser

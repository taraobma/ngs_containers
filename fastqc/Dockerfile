FROM continuumio/miniconda3

WORKDIR /data

COPY fastqc_env.yml /tmp/fastqc_env.yml

RUN conda env create -f /tmp/fastqc_env.yml && \
    conda clean -afy

ENV PATH=/opt/conda/envs/fastqc_env/bin:$PATH

CMD ["fastqc", "--help"]
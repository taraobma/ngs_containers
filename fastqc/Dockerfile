FROM mambaorg/micromamba:latest

WORKDIR /data

COPY --chown=$MAMBA_USER:$MAMBA_USER fastqc_env.yml /fastqc_env.yml

# Install FastQC into the base env
RUN micromamba install -y -n base -f /fastqc_env.yml && \
    micromamba clean --all --yes

USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

USER $MAMBA_USER

# micromamba's entrypoint sets up the base env 

CMD ["fastqc", "--version"]
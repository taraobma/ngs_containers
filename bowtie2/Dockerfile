FROM mambaorg/micromamba:latest

WORKDIR /data

# Copy env file as MAMBA_USER
COPY --chown=$MAMBA_USER:$MAMBA_USER bowtie2_env.yml /bowtie2_env.yml

# Install Bowtie2 into base env and clean
RUN micromamba install -y -n base -f /bowtie2_env.yml && \
    micromamba clean --all --yes

# Optional: procps for Nextflow trace
USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

USER $MAMBA_USER

# Let micromamba's entrypoint activate base env

# Default: show Bowtie2 version
CMD ["bowtie2", "--version"]
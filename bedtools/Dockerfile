FROM mambaorg/micromamba:latest

WORKDIR /data

# Copy env file as MAMBA_USER
COPY --chown=$MAMBA_USER:$MAMBA_USER bedtools_env.yml /bedtools_env.yml

# Install Bedtools into the base environment and clean
RUN micromamba install -y -n base -f /bedtools_env.yml && \
    micromamba clean --all --yes

# Optional: procps for Nextflow trace
USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

USER $MAMBA_USER

# Let micromamba's entrypoint handle env activation; no custom PATH needed.

# Default: print bedtools version
CMD ["bedtools", "--version"]
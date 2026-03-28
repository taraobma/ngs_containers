FROM mambaorg/micromamba:latest

WORKDIR /data

# Copy env file as micromamba user
COPY --chown=$MAMBA_USER:$MAMBA_USER samtools_env.yml /samtools_env.yml

# Install samtools into base env and clean
RUN micromamba install -y -n base -f /samtools_env.yml && \
    micromamba clean --all --yes

# Optional: procps for Nextflow resource reporting
USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

# Drop back to micromamba user
USER $MAMBA_USER


# Micromamba entrypoint will activate base env so samtools is on PATH
CMD ["samtools", "--version"]
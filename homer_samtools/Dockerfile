FROM mambaorg/micromamba:latest

WORKDIR /data

# Copy env file as micromamba user
COPY --chown=$MAMBA_USER:$MAMBA_USER homer_samtools_env.yml /homer_samtools_env.yml

# Install HOMER + samtools into base env and clean
RUN micromamba install -y -n base -f /homer_samtools_env.yml && \
    micromamba clean --all --yes

# Optional: procps for Nextflow resource reporting
USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

# Drop back to micromamba user
USER $MAMBA_USER

# Micromamba entrypoint will activate base env so HOMER/samtools are on PATH
CMD ["samtools", "--version"]
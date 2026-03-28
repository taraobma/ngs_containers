# Micromamba base image
FROM mambaorg/micromamba:latest

# Copy env file into the container as MAMBA_USER
COPY --chown=$MAMBA_USER:$MAMBA_USER trimmomatic_env.yml /trimmomatic_env.yml

# Install into the base environment and clean
RUN micromamba install -y -n base -f /trimmomatic_env.yml && \
    micromamba clean --all --yes

# Optional: root to install procps if you want Nextflow trace support
USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

# Back to normal user
USER $MAMBA_USER

# Ensure micromamba base env binaries are on PATH
ENV PATH="$MAMBA_ROOT_PREFIX/bin:$PATH"

# Default: show Trimmomatic help/version
CMD ["trimmomatic", "-version"]
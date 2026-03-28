FROM mambaorg/micromamba:latest

COPY --chown=$MAMBA_USER:$MAMBA_USER samtools_bedtools_env.yml /samtools_bedtools_env.yml

RUN micromamba install -y -n base -f /samtools_bedtools_env.yml && \
    micromamba clean --all --yes

USER root
RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*
USER $MAMBA_USER

ENV MAMBA_DOCKERFILE_ACTIVATE=1
ENV PATH="/opt/conda/bin:${PATH}"

CMD ["bash"]
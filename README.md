# NGS containers

Personal Docker/OCI containers for NGS tools.  
Each tool lives in its own subdirectory with a `Dockerfile` and environment file.

### Bedtools

Docker image providing the BEDTools genome analysis toolkit.

- Registry image: `ghcr.io/taraobma/bedtools:latest`
- Build context: `bedtools/`
- Tool: BEDTools (installed via Bioconda)

### Bowtie2

Docker image providing the Bowtie2 fast and sensitive read alignement tool.

- Registry image: `ghcr.io/taraobma/bowtie2:latest`
- Build context: `bowtie2/`
- Tool: Bowtie2 (installed via Bioconda)


### FastQC

Docker image providing the FastQC read quality control tool.

- Registry image: `ghcr.io/taraobma/fastqc:latest`
- Build context: `fastqc/`
- Tool: FastQC (installed via Bioconda)

### Trimmomatic

Docker image providing the Trimmomatic read trimming tool.

- Registry image: `ghcr.io/USER/trimmomatic:latest`
- Build context: `trimmomatic/`
- Tool: Trimmomatic (installed via Bioconda)


### Image tags and versions

| Image tag                                  | Tool         | Version | Notes          |
|--------------------------------------------|--------------|---------|----------------|
| `ghcr.io/taraobma/fastqc:0.12.1`          | FastQC       | 0.12.1  | pinned version |
| `ghcr.io/taraobma/fastqc:latest`           | FastQC       | 0.12.1  | current default|
| `ghcr.io/taraobma/trimmomatic:0.39`        | Trimmomatic  | 0.39    | pinned version |
| `ghcr.io/taraobma/trimmomatic:latest`      | Trimmomatic  | 0.39    | current default|
| `ghcr.io/taraobma/bedtools:2.31.1`         | Bedtools     | 2.31.1  | pinned version |
| `ghcr.io/taraobma/bedtools:latest`         | Bedtools     | 2.31.1  | current default|
| `ghcr.io/taraobma/bowtie2:2.5.5`           | Bowtie2      | 2.5.5   | pinned version |
| `ghcr.io/taraobma/bowtie2:latest`          | Bowtie2      | 2.5.5   | current default|



### Building the image

From the `fastqc/` directory:

```bash
docker build -t fastqc:latest .
```

Tag and push to GitHub Container Registry:

```bash
export GH_USER=taraobma

docker tag fastqc:latest ghcr.io/$GH_USER/fastqc:0.12.1
docker tag fastqc:latest ghcr.io/$GH_USER/fastqc:latest

docker push ghcr.io/$GH_USER/fastqc:0.12.1
docker push ghcr.io/$GH_USER/fastqc:latest
```

### Usage with Docker

Run FastQC on a FASTQ file in the current directory:

```bash
docker run --rm -v "$(pwd)":/data ghcr.io/taraobma/fastqc:latest \
  fastqc sample.fastq.gz --outdir /data
```

This writes the HTML and ZIP reports back into the current directory.

### Usage with Nextflow

Example Nextflow process:

```nextflow
process RUN_FASTQC {
  container 'ghcr.io/taraobma/fastqc:latest'

  input:
  path reads

  output:
  path "*.html"
  path "*.zip"

  """
  fastqc ${reads} --outdir .
  """
}
```

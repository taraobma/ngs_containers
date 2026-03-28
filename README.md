# NGS containers

Personal Docker/OCI containers for NGS tools.  
Each tool lives in its own subdirectory with a `Dockerfile` and environment file.

### Bedtools

Docker image providing the BEDTools genome analysis toolkit.

- Registry image: `ghcr.io/taraobma/bedtools:latest`
- Build context: `bedtools/`
- Tool: bedtools (installed via Bioconda)

### Bowtie2

Docker image providing the Bowtie2 fast and sensitive read alignement tool.

- Registry image: `ghcr.io/taraobma/bowtie2:latest`
- Build context: `bowtie2/`
- Tool: Bowtie 2 (installed via Bioconda)


### FastQC

Docker image providing the FastQC read quality control tool.

- Registry image: `ghcr.io/taraobma/fastqc:latest`
- Build context: `fastqc/`
- Tool: FastQC (installed via Bioconda)

### Homer_Samtools

Docker image providing HOMER motif analysis tools together with samtools for working with alignment and interval files (e.g. BAM, SAM, BED).

- Registry image: `ghcr.io/taraobma/homer_samtools:latest`
- Build context: `homer_samtools/`
- Tool: HOMER (via Bioconda) plus samtools (via Bioconda)

### MultiQC
Docker image providing MultiQC, a tool to aggregate results from multiple bioinformatics reports (e.g. FastQC) into a single HTML report.

- Registry image: `ghcr.io/taraobma/multiqc:latest`
- Build context: multiqc/
- Tool: MultiQC (installed via Bioconda).


### Trimmomatic

Docker image providing the Trimmomatic read trimming tool.

- Registry image: `ghcr.io/taraobma/trimmomatic:latest`
- Build context: `trimmomatic/`
- Tool: Trimmomatic (installed via Bioconda)

### Samtools

Docker image providing the samtools toolkit for manipulating and querying SAM/BAM/CRAM alignment files.

- Registry image: `ghcr.io/taraobma/samtools:latest`
- Build context: samtools/
- Tool: samtools (installed via Bioconda).


### Image tags and versions

| Image tag                                          | Tool         | Version | Notes                                  |
|----------------------------------------------------|--------------|---------|----------------------------------------|
| `ghcr.io/taraobma/bedtools:2.31.1`                 | bedtools     | 2.31.1  | pinned version                         |
| `ghcr.io/taraobma/bedtools:latest`                 | bedtools     | 2.31.1  | current default                        |
| `ghcr.io/taraobma/bowtie2:2.5.5`                   | Bowtie 2      | 2.5.5   | pinned version                         |
| `ghcr.io/taraobma/bowtie2:latest`                  | Bowtie 2      | 2.5.5   | current default                        |
| `ghcr.io/taraobma/fastqc:0.12.1`                   | FastQC       | 0.12.1  | pinned version                         |
| `ghcr.io/taraobma/fastqc:latest`                   | FastQC       | 0.12.1  | current default                        |
| `ghcr.io/taraobma/homer_samtools:homer5.1`         | HOMER        | 5.1     | pinned HOMER; includes samtools 1.23.1 |
| `ghcr.io/taraobma/homer_samtools:homer5.1-sam1.23.1`| HOMER       | 5.1     | fully pinned HOMER + samtools          |
| `ghcr.io/taraobma/homer_samtools:latest`           | HOMER        | 5.1     | current default; samtools 1.23.1       |
| `ghcr.io/taraobma/multiqc:1.33`                | MultiQC      | 1.33    | pinned version  |
| `ghcr.io/taraobma/multiqc:latest`              | MultiQC      | 1.33    | current default |
| `ghcr.io/taraobma/trimmomatic:0.39`                | Trimmomatic  | 0.39    | pinned version        |
| `ghcr.io/taraobma/trimmomatic:latest`              | Trimmomatic  | 0.39    | current default       |
| `ghcr.io/taraobma/samtools:1.23.1`              | samtools     | 1.23.1  | pinned version |
| `ghcr.io/taraobma/samtools:latest`              | samtools     | 1.23.1  | current default|


### Building and testing the image 

From the `fastqc/` directory:

```bash
docker build -t fastqc:latest .

docker run --rm fastqc:lastest
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

# NGS containers

Personal Docker/OCI containers for NGS tools.  
Each tool lives in its own subdirectory with a `Dockerfile` and environment file.

## FastQC

Docker image providing the FastQC read quality control tool.

- Registry image: `ghcr.io/taraobma/fastqc:latest`
- Build context: `fastqc/`
- Tool: FastQC (installed via Bioconda)

### Image tags and versions

| Image tag                               | FastQC version | Notes            |
|----------------------------------------|----------------|------------------|
| `ghcr.io/taraobma/fastqc:0.12.1` | 0.12.1         | pinned version   |
| `ghcr.io/taraobma/fastqc:latest` | 0.12.1         | current default  |
| `ghcr.io/taraobma/trimmomatic:latest` | 0.39    | current default   |

Update this table whenever you rebuild the image with a new FastQC version.

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

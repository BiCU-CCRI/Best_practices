# Shared resources

Definition of structure and location of shared resources at the cluster(s). Primarily focused on newly established shared resources at the CeMM cluster but can be applied anywhere.

- `README.md`: information (verbal) about the references, images, subdirectories, ... Used to describe the resources and can be stored in `git`.
- `run.sh`: information to reproduce the references, images, subdirectories, ... Contains information to *rebuild* the resources if necessary and can be stored in `git`.

## References

- **Source link** of the references should be included in the `run.sh` or `README.md` including all the postprocessing steps if applicable
- **Steps to obtain the reference** if **not possible** to include the **link** should be included in the `run.sh` or `README.md` (for example, some UCSC  Genome Browser references)
    - Note: If you are copying the reference from the CCRI storage, include the original location and the date when you copied the reference (for example, *Copied from Isilion on Jan 02, 2024: `/home/jan_o/bioinf_isilon/core_bioinformatics_unit/Public/references/Human_GRCh38_v102/Homo_sapiens_GRCh38_v102_star_index_150bp` -> `STAR_2.7.10a/index_150bp`*)
- Downloading of the reference should **include the download date** `Downloaded on...`
- It should be possible to identify the **specific reference version** either from the directory structure or from the file name (for example, `human/GRCh38/ensembl_v102/genome.fa`)
- The **reference version** should **not be repeated** in both the directory structure and the file name (for example, don't do `human/GRCh38/ensembl_v102/human_GRCh38_ensembl_v102.fa`)
- Tip: *Generic* reference name makes it easy to switch between versions/organisms
    - For example, `human/GRCh38/ensembl_v102/genome.fa` vs. `mouse/GRCm38/ensembl_v102/genome.fa`
- You can keep the original downloaded file name and softlink it to the *target* file name (for example,
  `ln -s Homo_sapiens.GRCh38.dna.toplevel.fa genome.fa`)
- **Steps to construct the reference** (for example, genome index for mapping tool) should included in the `run.sh` or `README.md` including the used image/tool version
- **Tool version** used to construct the reference (for example, genome index for mapping tool) should be included **in the reference name** (for example, `human/GRCh38/ensembl_v102/STAR_v2.7.10a`)
- **Parameters** used to construct the reference should be included **in the reference name** (for example, `human/GRCh38/ensembl_v102/STAR_v2.7.10a/index_150bp`)
- **Use Latin names** for organisms where possible
    - If you want to use *common* names, softlink them from Latin names (for example, `ln -s Homo_sapiens human`)
- Only create **subdirectories** if your reference is **very pipeline-/analysis-specific** and it doesn't have any use for other users

### Directory structure

Proposed reference structure (genome, gene annotation, ...):

1.

```shell
genomes
└── Homo_sapiens
    └── GRCh38
        └── Ensembl
            └── v102
                ├── README.md
                ├── STAR_v2.7.10a
                │   ├── index_100bp
                │   ├── index_150bp
                │   └── index_50bp
                ├── genes.gtf -> Homo_sapiens.GRCh38.113.gtf
                ├── genome.fa -> Homo_sapiens.GRCh38.dna.toplevel.fa
                ├── Homo_sapiens.GRCh38.113.gtf
                ├── Homo_sapiens.GRCh38.dna.toplevel.fa
                ├── run.sh
                └── transcripts.bed12
```

2.

```shell
genomes
└── Ensembl
    └── Human_GRCh38_v102
        ├── README.md
        ├── STAR_v2.7.10a
        │   ├── index_100bp
        │   ├── index_150bp
        │   └── index_50bp
        ├── genes.gtf -> Homo_sapiens.GRCh38.113.gtf
        ├── genome.fa -> Homo_sapiens.GRCh38.dna.toplevel.fa
        ├── Homo_sapiens.GRCh38.113.gtf
        ├── Homo_sapiens.GRCh38.dna.toplevel.fa
        ├── run.sh
        └── transcripts.bed12
```

3.

```shell
genomes
└── Human_GRCh38
    └── Ensembl_v102
        ├── README.md
        ├── STAR_v2.7.10a
        │   ├── index_100bp
        │   ├── index_150bp
        │   └── index_50bp
        ├── genes.gtf -> Homo_sapiens.GRCh38.113.gtf
        ├── genome.fa -> Homo_sapiens.GRCh38.dna.toplevel.fa
        ├── Homo_sapiens.GRCh38.113.gtf
        ├── Homo_sapiens.GRCh38.dna.toplevel.fa
        ├── run.sh
        └── transcripts.bed12
```

### CeMM cluster location

Proposed directory for shared genomic-based references (genome, gene annotation, ...):

```shell
/nobackup/lab_ccri_bicu/public/references/genomes
```

## Databases

TODO

## Images

- **Do not build images** from **scratch** if they are **already available** in one of the hubs or already exist in the shared resources
    - Design your workflow/analysis so it uses a single image per step, preferably **single-tool images**
    - If you have to build a **custom image**, use `apptainer` and **install the tool(s) using `conda`** (doesn't require root privileges as compared to `apt-get`)
    - For more info on where to get prebuilt images, see [Publicly available images](#publicly-available-images) section
- **Include `.def` and `.Dockerfile`** files for custom images
- **Include instructions** on how to **build** the image, **including the version of the tool** (docker/apptainer/singularity) used to build the image
- Include the **download source link** if you didn't build the container yourself
    - Note: If you are copying the image from the CCRI storage, include the original location and the date when you copied the image (for example, *Copied from Isilion on Jan 02, 2024: `/home/jan_o/bioinf_isilon/core_bioinformatics_unit/Public/singularity_images/minimap2_v2.17.sif` -> `minimap2_v2.17.sif`*)
- **Include the tool version** (if single-tool image) and/or image version (preferably `git` commit hash at the time of build) in the **name of the image**
- For Apptainer/Singularity images, **use `.sif`** (Singularity Image Format) suffix
    - Note: Singularity Image Format is the default format since Singularity 3.0+
- Using **`sha256` digest** (or `git` hash) method is **preferred over tag method**
    - For more info see [Best_practices/coding_and_review/code_reproducibility](https://github.com/BiCU-CCRI/Best_practices/blob/15-best-coding-practices-and-code-review/coding_and_review/code_reproducibility.md#base-image)
- Only create **subdirectories** if your images are **very pipeline-/analysis-specific** and don't have any use for other users, or would clash with other already existing images (for example, very similar name)

### Directory structure

Proposed images structure:

```shell
apptainer_images
├── README.md
├── bcftools-1.20.sif
├── rnaseq_fusion_pipeline
│   ├── rnaseq_fusion_report_v2.1.5_mitelman_fix_add_tool_cicero--f122a79.sif
│   └── rnaseq_fusion_report_v2.1.5_mitelman_fix_add_tool_cicero.Dockerfile
└── run.sh
```

### CeMM cluster location

Proposed directory for shared Apptainer/Singularity images:

```shell
/nobackup/lab_ccri_bicu/public/apptainer_images
/nobackup/lab_ccri_bicu/public/singularity_images -> apptainer_images # softlink from apptainer_images
```

### Publicly available images

- [seqera.io](https://seqera.io/containers/): Build your own images from PyPI, bioconda, and conda-forge
- [biocontainers](https://quay.io/organization/biocontainers) ([homepage](https://biocontainers.pro/registry) and [GitHub page](https://github.com/BioContainers/containers)): Prebuilt images; Contains all available `conda` packages as images and other bioinformatics tools images
    - Also available on [Dockerhub](https://hub.docker.com/u/biocontainers)
- [Galaxy project](https://depot.galaxyproject.org/singularity/) - Prebuilt images
- [Dockerhub](https://hub.docker.com/search) - *general* Docker images hub
- [Sylab](https://cloud.sylabs.io/library) - general Singularity images hub
- [Singularity hub](https://singularityhub.github.io/) - general Singularity images info

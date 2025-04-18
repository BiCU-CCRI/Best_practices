# Shared resources

Structure and recommendations for shared resources at the cluster(s). Primarily focused on newly established shared resources at the CeMM cluster but can be applied anywhere.

- `run.sh`: information on where to get the references (databases, images, etc.) from and how to build them. It contains information to *rebuild* the resources if necessary and can be stored on `GitHub`. This is the most critical resource if we have to build the references from scratch or share them externally.
- `README.md`: information (verbal) about the references (databases, images, etc.). Used to describe the resources and can be stored on `GitHub`. For example, it can contain information about why a particular reference was chosen over another, the differences, which reference to use as the *default*, etc.

Shared resources at the CeMM cluster are at `/nobackup/lab_ccri_bicu/public`.

## References

- **Source link** of the references must be included in the `run.sh`
- All the processing instructions to build the reference (if applicable) must be included in the `run.sh`
- **Steps to obtain the reference** that are **not possible** to be described as a *command* have to be included in the `run.sh` or `README.md` (for example, some UCSC Genome Browser references)
- Note: If you are copying legacy reference from the CCRI storage, note the original location and the date when you copied the reference
    - For example, *Copied from Isilion on Jan 02, 2024: `/home/jan_o/bioinf_isilon/core_bioinformatics_unit/Public/references/Human_GRCh38_v102/Homo_sapiens_GRCh38_v102_star_index_150bp` -> `./STAR_2.7.10a/index_150bp`*
- Downloading of a reference should include **the download date**
    - For example, *`Downloaded on Apr 17, 2025 from https://genome.ucsc.edu/cgi-bin/hgTables`*
- It should be possible to identify the specific reference **release** either from the directory structure or from the file name
    - For example, the `Homo_sapiens.GRCh38.dna.toplevel.fa` in `Homo_sapiens/GRCh38/Ensembl/v102/Homo_sapiens.GRCh38.dna.toplevel.fa`
- It should be possible to identify the specific reference **version** either from the directory structure or from the file name
    - For example, the `v102` in `Homo_sapiens/GRCh38/Ensembl/v102/Homo_sapiens.GRCh38.dna.toplevel.fa`
    - Note: If you are unsure about the release version, use the date when you downloaded the resource in YYYYMMDD format (for example, `20250417`) to keep the same directory structure
- You can keep the original downloaded file name and softlink it to the *target* file name (for example,
  `ln -s Homo_sapiens.GRCh38.dna.toplevel.fa genome.fa`)
    - *Generic* reference name makes it easy to switch between versions/organisms
        - For example, `Homo_sapiens/GRCh38/Ensembl/v102/genome.fa` vs. `Mus_musculus/GRCm38/Ensembl/v102/genome.fa`
- **Steps to construct the reference** (for example, genome index for mapping tool) should included in the `run.sh` or `README.md`, including the used image/tool version
- **Tool version** used to construct the reference (for example, genome index for mapping tool) should be included **in the reference name** (for example, `Homo_sapiens/GRCh38/Ensembl/v102/STAR/v2.7.10a`)
- **Parameters** used to construct the reference that is not set by default should be included **in the reference name**
    - For example, a `STAR` index with `150` read length settings would be `Homo_sapiens/GRCh38/Ensembl/v102/STAR_v2.7.10a/index_150bp`
- **Use Latin names** for organisms where possible
    - If you must use *common* names, softlink them from Latin names (for example, `ln -s Homo_sapiens human`), but it is generally not recommended
- Only create **subdirectories** if your reference is **very pipeline-/analysis-specific** and it doesn't have any use for other users

### Directory structure for references, databases, and other resources

#### Directory structure for genomic references

```shell
references
└── Homo_sapiens
    └── GRCh38
        └── Ensembl
            └── v102
                ├── README.md
                ├── STAR
                │   └── v2.7.10a
                │       ├── index_100bp
                │       ├── index_150bp
                │       └── index_50bp
                ├── genes.gtf -> Homo_sapiens.GRCh38.102.gtf
                ├── genome.fa -> Homo_sapiens.GRCh38.dna.toplevel.fa
                ├── Homo_sapiens.GRCh38.102.gtf
                ├── Homo_sapiens.GRCh38.dna.toplevel.fa
                └── run.sh
```

#### Directory structure for databases

Copy the structure of the genomic datasets wherever possible.

```shell
databases
└── Homo_sapiens
    └── GRCh38
        └── dbSNP
            └── b151
                ├── All_20180418.vcf.gz
                ├── README.md
                └── run.sh
```

#### Directory structure for other resources

Resources might have different structures from references and databases as they are often not well defined, but try to keep the structure as similar as possible.

For example, [target `BED`](https://www.twistbioscience.com/sites/default/files/resources/2022-12/hg38_exome_v2.0.2_targets_sorted_validated.re_annotated.bed) files for [Twist Exome 2.0](https://www.twistbioscience.com/products/ngs/fixed-panels/exome2),

```shell
resources
└── twist_biosciences
    └── Homo_sapiens
        └── hg38
            └── twist_exome_2.0
                └── v2.0.2
                    ├── README.md
                    ├── hg38_exome_v2.0.2_targets_sorted_validated.re_annotated.bed
                    └── run.sh
```

## Images (Apptainer/Docker)

- Design your workflow/analysis to use **single-tool images** whenever possible
    - Note: It is ok to add certain software to the image, for example, R with Java, etc.
- **Include the tool version** (if single-tool image) and/or image version (preferably `git` commit hash at the time of build) in the **name of the image**
    - For example, `ucsc-bedclip-377--h0b8a92a_2.sif`
- **Do not duplicate** images if they are **already exist** in the shared resources
- **Don't build** an image from scratch if it already exists as **prebuilt image** - see [Publicly available images](#publicly-available-images) section
- If you have to build a **custom image**, use `ubuntu:22.04` as the base image and always include the `.def.` (or `.Dockerfile)`) with the image
    - apptainer is preferred due to the compatibility with the CeMM cluster environment
- **Include instructions** on how to **build** the image, **including the tool version** (`apptainer`/`singularity`/`docker`) used to build the image
- Include the **download source link** if you didn't build the container yourself
    - Note: If you are copying the image from the CCRI storage, include the original location and the date when you copied the image (for example, *Copied from Isilion on Jan 02, 2024: `/home/jan_o/bioinf_isilon/core_bioinformatics_unit/Public/singularity_images/minimap2_v2.17.sif` -> `minimap2_v2.17.sif`*)
- For Apptainer/Singularity images, **use `.sif`** (Singularity Image Format) suffix
    - Note: Singularity Image Format is the default format since Singularity 3.0+
- Using **`sha256` digest** (or `git` hash) method is **preferred over tag method**
    - For more info see [Best_practices/coding_and_review/code_reproducibility](https://github.com/BiCU-CCRI/Best_practices/blob/15-best-coding-practices-and-code-review/coding_and_review/code_reproducibility.md#base-image)
- Create **subdirectories** if your images are **very pipeline-/analysis-specific** and don't have any use for other users or would clash with other already existing images (for example, very similar name)

### Directory structure for images

```shell
apptainer_images
├── README.md
├── bcftools-1.20.def
├── bcftools-1.20.sif
├── rnaseq_fusion_pipeline
│   ├── rnaseq_fusion_report-v2.1.5_mitelman_fix_add_tool_cicero.sif
│   └── rnaseq_fusion_report-v2.1.5_mitelman_fix_add_tool_cicero.Dockerfile
└── run.sh
```

### Publicly available images

- [seqera.io](https://seqera.io/containers/): Build your own images from PyPI, bioconda, and conda-forge
- [biocontainers](https://quay.io/organization/biocontainers) ([homepage](https://biocontainers.pro/registry) and [GitHub page](https://github.com/BioContainers/containers)): Prebuilt images; Contains all available `conda` packages as images and other bioinformatics tools images
    - Also available on [Dockerhub](https://hub.docker.com/u/biocontainers)
- [Galaxy project](https://depot.galaxyproject.org/singularity/) - Prebuilt images
- [Dockerhub](https://hub.docker.com/search) - *general* Docker images hub
- [Sylab](https://cloud.sylabs.io/library) - general Singularity images hub
- [Singularity Hub](https://singularityhub.github.io/) - general Singularity images info

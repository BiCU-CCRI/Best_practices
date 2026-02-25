# `snakemake` best practices and tips

## Tips

### Errors

#### `squashfs`/`unsquashfs` error

If you get `squashfs`/`unsquashfs` error when using `snakemake` on `slurm` (CeMM cluster), it might be because of `squashfs` tries to use all the available threads not respecting `slurm` resources (see full error at [examples/squashfs_error.txt](examples/squashfs_error.txt)). This has been reported [here](https://github.com/apptainer/singularity/issues/1228) and (maybe) fixed [here](https://github.com/apptainer/singularity/pull/5003). It also might be that this is fixed only in `apptainer` [here](https://github.com/apptainer/singularity/pull/6186).

To prevent this, try to limit the number of threads used for `squashfs`/`unsquashfs` in `singularity.conf`:

1. Activate your `conda` environment

```bash
conda activate myenv
```

2. Check the current settings

```bash
singularity config global --get "mksquashfs procs"
# mksquashfs procs = 0
```

3. Limit the number of procs for squashfs/unsquashfs

```bash
# sed -i 's/^mksquashfs procs = 0/mksquashfs procs = 1/' "$CONDA_PREFIX/etc/singularity/singularity.conf" # Manual change, don't use
singularity config global --set "mksquashfs procs" 1
```

4. Check the changes

```bash
singularity config global --get "mksquashfs procs"
# mksquashfs procs = 1
```

If necessary, you can reset the defaults with:

```bash
singularity config global --reset "mksquashfs procs"
```

Note: You might have to use `singularity>3.7.1`.

[![R](https://img.shields.io/badge/-script-276DC3.svg?style=flat&logo=R)](https://cran.r-project.org)
[![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c.svg?labelColor=000000)](https://sylabs.io/docs/)

# README

This repository holds a singularity / apptainer image with pre-installed **_R_** libraries for analysing DNA methylation generated from RRBS, BS-seq and EM-seq. Genome annotation libraries included for both human and mouse. Differential methylation calculation packages include are edgeR and methylKit.

---

## Libraries list

#### Visualisation

+ ggplot2
+ ggrepel
+ ggsignif
+ cowplot
+ RColorBrewer
+ patchwork
+ ComplexHeatmap

#### Differential methylation analysis

+ edgeR
+ methylKit

#### Gene and genome annotation

+ [clusterProfiler](https://www.bioconductor.org/packages/release/bioc/html/clusterProfiler.html)
+ [ReactomePA](https://bioconductor.org/packages/release/bioc/html/ReactomePA.html)
+ biomaRt
+ [org.Mm.eg.db](https://bioconductor.org/packages/release/data/annotation/html/org.Mm.eg.db.html)
+ [org.Hs.eg.db](https://bioconductor.org/packages/release/data/annotation/html/org.Hs.eg.db.html)
+ tximport

#### Utility

+ gtools
+ tools
+ scales
+ data.table
+ forcats
+ openxlsx
+ readr

## Build

Use the definition file to build locally:

```sh
apptainer build containeR-methylome.sif containeR-methylome.def
```

## Deploy

Pre-build image can be downloaded from the [Cloud Library](https://cloud.sylabs.io/library):

```sh
apptainer pull library://andreyhgl/singularity-r/methylome
```

> [!Note]
> With apptainer and on HPCs the [remote singularity host](https://apptainer.org/docs/user/latest/endpoint.html#restoring-pre-apptainer-library-behavior) might need to be added manually
>
> ```sh
> # list the remote URI
> apptainer remote list
> 
> # add singularity cloud URI
> apptainer remote add --no-login SylabsCloud cloud.sycloud.io
> ```

## Execute scripts

In order to fully utilise the singularity image make sure a shebang is included in the script file `#!/usr/bin/env Rscript`

```r
#!/usr/bin/env Rscript

suppressPackageStartupMessages({
	library(methylKit)
	library(gtools)
})

...

```

Also make the script file executable

```sh
chmod +x script-file.R
```

The singularity image expects a script file on `exec`.

```sh
apptainer exec library://andreyhgl/singularity-r/methylome script.R
```
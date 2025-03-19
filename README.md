renv with packages for vscode on Ubuntu LTS. See https://code.visualstudio.com/docs/languages/r for more info.

# Setup
Adapted from https://github.com/REditorSupport/vscode-R/wiki/Getting-Started and https://github.com/REditorSupport/vscode-R/wiki/Working-with-renv-enabled-projects

1. Install R. See: https://cran.r-project.org/bin/linux/ubuntu
2. Install renv. Inside R: `install.packages("renv")`
3. In this folder: `renv::restore()`
4. Put output of `renv::paths$library()` into `r.libPaths`, e.g.:

```
  "r.libPaths": [
        "/home/user/R/vscode-R/renv/library/linux-ubuntu-jammy/R-4.4/x86_64-pc-linux-gnu"
    ]
```

# Additional setup
See:

 - https://github.com/REditorSupport/vscode-R/wiki/Installation:-Linux
 - https://github.com/REditorSupport/vscode-R/wiki/Recommended-extensions-and-configuration

## pandoc
```
sudo apt install pandoc
```

## radian
Use pipx or `pip install --user radian` to install for user, then add path to vscode settings, e.g.:

```
    "r.rterm.linux": "${userHome}/.local/bin/radian",
```

## Settings sync
Make sure to exclude site-specific settings from sync:
```
    "settingsSync.ignoredSettings": [
        "r.libPaths",
        "r.rterm.linux",
    ]
```

## Environment:

### ~/.lintr:
```
linters: linters_with_defaults(
    commented_code_linter = NULL,
    line_length_linter(100),
    object_usage_linter = NULL,
    indentation_linter = indentation_linter(indent = 4L)
  )
encoding: "UTF-8"

```

### ~/.Rprofile
```
r <- getOption("repos")
r["CRAN"] <- "https://cloud.r-project.org"
options(repos = r)
options(Ncpus = parallel::detectCores())

rm(r)
```

# Tips

renv::install replaces BiocManager, devtools::install_github and remotes::install_github. E.g.:

 - `renv::install("bioc::Biobase")`
 - `renv::install("jaredhuling/jcolors")`

To enable BiocManager and not automatically install packages when initializing renv, use:
  - `renv::init(bare = TRUE, bioconductor = TRUE)`

Don't forget to `renv::activate()` and `renv::snapshot()`.
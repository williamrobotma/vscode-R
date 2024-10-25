renv with packages for vscode.

After `renv::restore()`, put output of `renv::paths$library()` into `r.libPaths`, e.g.:

```
  "r.libPaths": [
        "/home/user/R/vscode-R/renv/library/linux-ubuntu-jammy/R-4.4/x86_64-pc-linux-gnu"
    ]
```


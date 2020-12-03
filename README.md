# singularity
## How to build
`singularity build <sif filename> <definition filename>`

## How to run the image?
`singularity run -B $XDG_RUNTIME_DIR <sif file>`

It require to bind the user's $XDG_RUNTIME_DIR.


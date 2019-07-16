This is just to build vs code in container to be run on OS before CentOS7.

How to run the image?
singularity run -B $XDG_RUNTIME_DIR vs-code.sif

It require to bind the user's $XDG_RUNTIME_DIR.

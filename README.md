# [singularity](https://sylabs.io/guides/3.6/user-guide/introduction.html)

## How to build
The simplest way to build a singularity container is to build from docker:
```singularity pull docker://centos:latest```

However, if you have a definition file like this:
docker.def:
```
Bootstrap: docker
From: centos:7

%labels
	AUTHOR SerTan
	VERSION 1.0

%environment
	export PATH=/usr/local/bin:$PATH
	export LANG=en_US.UTF-8
	export LC_ALL=C

%files

%post
	yum -y install emacs

%runscript
	echo "This is a container"
```
Then, you can build the SIF from it:
`sudo singularity build test.sif docker.def`

You can refer to this [quickstart guide](https://sylabs.io/guides/3.6/user-guide/quick_start.html) to have more information.


## How to run the image?
To run a SIF:
`singularity run -B $XDG_RUNTIME_DIR <sif file>`

It require to bind $XDG_RUNTIME_DIR  into the container so that we can utilize the host's X session capacity.


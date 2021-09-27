# [typora](https://typora.io) 
[typora](https//typora.io) is a markdown editor and reader.  It supports:
    1. Linux
    2. Windows
    3. Mac (beta)

There is a lot of cool features, but I like the most is these:
    1. Live preview
    2. Diagram (flow and [Mermaid](https://mermaid-js.github.io/mermaid/#/))
    3. Nice dropdown UI that make writing markdown even easier

However, `typora` only have install option for Ubuntu/Debian variant:
```bash
# or run:
# sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -
# add Typora's repository
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update
# install typora
sudo apt-get install typora
```
or download a tarball binary from [here](https://typora.io/linux/Typora-linux-x64.tar.gz).
Which the tarball would be working in most of Linux Distributions.

## Building as [singularity](https://sylabs.io/guides/3.6/user-guide/) container
As I am learning and trying out container and I found **singularity** is a unique container that suitable to build containerized apps that can be used in any Linux systems that have **singularity**[^preferred version] installed.

Here is the simple steps to build:
1. Install `singularity`.  You can follow the instructions [here](https://sylabs.io/guides/3.6/admin-guide/installation.html) to get the proper installation steps for your Linux Distributions.  
Here is the steps for installing in CentOS 7:
	```
	sudo yum install -y epel-release
	sudo yum install -y singularity
	```
	
2. Clone my singularity git repo [here](https://github.com/serheang/singularity)
    ```
    git clone https://github.com/serheang/singularity
    ```
3. Change directory to `typora`:
	```
	cd singularity/typora
	```
	> There is other singularity definition files in the repo, feel free to explore and try it out.  
4. Build sif[^what is sif]
	```
	sudo singyularity build typora.sif typora.def
	```
	or
	```
	singularity build --remote typora.sif typora.def
	```
	> To build remotely at https://cloud.sylabs.io/home
	or
	```
	singyularity build --fakeroot typora.sif typora.def
	```
	> To use `--fakeroot`, you will need to read about it [here](https://sylabs.io/guides/3.6/admin-guide/user_namespace.html)
5. Go and make yourself a cup of coffee or tea, and the image will be ready.

## Running SIF
After built the SIF, you can easily run it by running:
```bash
singularity run -B $XDG_RUNTIME_DIR --app typora.sif
```
> **$XDG_RUNTIME_DIR** is require for the container to bind to your X session.

[^preferred version]: prefer to be running at least singulartiy>3.6
[^what is sif]: Singularity immutable images in the Singularity Image File (SIF) format.

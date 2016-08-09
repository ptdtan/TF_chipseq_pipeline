### Installation instruction

Install Anaconda Python3 (or Miniconda3) on your system. If you already have it, skip this. Get the Miniconda3 installer (4.0.5) at <a href="https://repo.continuum.io/miniconda/Miniconda3-4.0.5-Linux-x86_64.sh" target=_blank>https://repo.continuum.io/miniconda/Miniconda3-4.0.5-Linux-x86_64.sh</a> and install it.
```
$ wget https://repo.continuum.io/miniconda/Miniconda3-4.0.5-Linux-x86_64.sh
$ bash Miniconda3-4.0.5-Linux-x86_64.sh
```
Choose `yes` for the final question. If you choose `no`, you need to manually add Miniconda3 to your `$HOME/.bashrc`.
```
Do you wish the installer to prepend the Miniconda2 install location
to PATH in your /your/home/.bashrc ? [yes|no]
[no] >>> yes
```
Remove any other Anaconda Python from your `$PATH`. Check your loaded modules with `module list` and unload any Anaconda Python modules. Open a new terminal after installation.

Install BigDataScript v0.999l on your system.
```
$ git clone https://github.com/pcingola/BigDataScript
$ cd BigDataScript
$ git checkout tags/v0.9999
$ cp distro/bds_Linux.tgz $HOME
$ cd $HOME
$ tar zxvf bds_Linux.tgz
```
Add `export PATH=$PATH:$HOME/.bds` to your bash initialization script (`$HOME/.bashrc` or `$HOME/.bash_profile`). If java memory occurs, add `export _JAVA_OPTIONS="-Xms256M -Xmx512M -XX:ParallelGCThreads=1"` too.

Get the latest version of the pipeline.
```
$ git clone https://github.com/kundajelab/TF_chipseq_pipeline
```
Install software dependencies automatically. It will create two conda environments (aquas_chipseq and aquas_chipseq_py3) in Miniconda3.
```
$ ./install_dependencies.sh
```
If you see the following error, then update your Anaconda with `conda update conda`.
```
Error: ERROR: placeholder '/root/miniconda3/envs/_build_placehold_placehold_placehold_placehold_placehold_p' too short in: glib-2.43.0-2
```
If you don't use `install_dependencies.sh`, manually replace BDS's default `bds.config` with a correct one:
```
$ cp bds.config ./utils/bds_scr $HOME/.bds
```
If `install_dependencies.sh` fails, run `./uninstall_dependencies.sh`, fix problems and then try `./install_dependencies.sh` again.


### Genome data files

For SCG3/4 (carmack*, crick*, scg3*, scg4*) and Sherlock (sherlock*.stanford.edu) clusters, the pipeline automatically determines the type of servers and set shell environments and species database. Skip all genome-specific parameters (e.g. bwa index) and just specify species.
```
$ bds chipseq.bds ... -species [SPECIES; hg19, mm9, ... ]
```
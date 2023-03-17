# Singularity-template

Simple singularity templates for ML/DL task.

## 1. Install Singularity and system dependencies

Install singularity following [the official document](https://docs.sylabs.io/guides/3.7/admin-guide/installation.html).
Install system dependencies to build base ubuntu image.

```bash
sudo ./install_dependencies.sh
```

## 2. Build a singularity image from definition file

Build the image(.sif) if you don't need to make any additional changes.

Example command to build a image.

```bash
sudo singularity build images/miniconda.sif definitions/miniconda/miniconda_4.11.0_buildall.def
```

You can build the image from base ubuntu image to reduce the build time.

But boostrap and file location in definition should be modified accroding to your environment.

```bash
sudo singularity build images/miniconda.sif definitions/miniconda/miniconda_4.11.0.def
```

## 3. Build a singularity image with additional modifications using '--sandbox' option

If you need to install additional dependencies or dependencies can change depending on the situation, you can use the sandbox option.

First, build a sandbox directory from definition files

```bash
sudo singularity build --sandbox $PATH/<name> definitions/miniconda/miniconda_4.11.0.def
```



Attach to a sandbox directory with '--writable' option and modification you made will be writen in the directory.

You can build sandbox directory to singularity image with same command.

```bash
sudo singularity shell --writable $PATH/<name>
#install additional dependency
sudo singularity build <name>.sif $PATH/<name>
```

## Troubleshooting

If 'conda init' doesn't work in miniconda image, you can manually load the conda profile from the install path.

```bash
source /opt/miniconda3/etc/profile.d/conda.sh
```

## Caution
Packages installed in '$HOME/<PATH>' will be ignored in singularity build process

e.g., 

Not included: pip install packageA  --> '$HOME/.local/lib/python3.x/dist-packages/packageA'

Included: sudo pip install packageB  --> '/usr/local/lib/python3.x/dist-packages/packageB'



## References

https://docs.sylabs.io/guides/3.7/user-guide/index.html

https://github.com/NIH-HPC/Singularity-Tutorial

https://github.com/mkandes/naked-singularity

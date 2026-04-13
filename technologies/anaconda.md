# Overview

### Use
Channels: where a package is hosted
Environments: directory containing a collection of packages
### Installation
1. Download Installer
2. Verify Hashes
3. `bash <conda-installer-name>-latest-Linux-x86_64.sh`
# Technical
### Commands
```bash
# Update conda
conda update conda

# List environments
conda info --envs

# Activate base environment
conda activate

# Activate existing environment
conda activate <env name>

# Create new environment
conda create --name <env name> python=3.12

# Create environment from environment.yml
conda env create -f environment.yml

# Verify contents of environment
conda env list

# Update environment with environment.yml
conda env update --file environment.yml --prune

# Deactivate environment
conda deactivate

# Remove environment
conda remove --name <env name> --all

# Install package
conda install <package name>=<version>
pip install <package name>

# Remove package
conda uninstall <package name>

# Export to environment.yml
conda env export > environment.yml
```

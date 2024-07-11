# Conda Env on HPC Cluster

## Load modules
   1. Load anaconda module

      `$ module load anaconda/2021.05`

      or 
   
       `$ module load anaconda/2021.11`  
      or
      
       `$ module load miniconda/23.10`             
   
      NOTE: `anaconda/3` and `anaconda/2` are very old versions. 
   
   3. Load other modules needed         
      `$ module load conda-env-mod/default`   

### Configure your conda 

Two directories in your group research storage space (one for storing the envs, one for storing the pkgs, for example: condaenv, condapkg)

`$ mkdir /cluster/tufts/xli37/software/condaenv/`

`$ mkdir /cluster/tufts/xli37/software/condapkg/`

If you haven't used conda before on the cluster, create a file named ".condarc" in your home directory. 

Now add the following 4 lines to the `.condarc` file in your home directory (modify according to your real path to the directories):

```
envs_dirs:
  - /cluster/tufts/xli37/software/condaenv/
pkgs_dirs:
  - /cluster/tufts/xli37/software/condapkg/
```

After this, your `.condarc`file should look like this

`$ cat ~/.condarc`

```
envs_dirs:
  - /cluster/tufts/xli37/software/condaenv/
pkgs_dirs:
  - /cluster/tufts/xli37/software/condapkg/

channels:
  - bioconda
  - conda-forge
  - defaults
```

### Create your conda environment

Now you can create your own conda env

`$ cd /cluster/tufts/xli37/software/condaenv/`

`$ conda create -p bio_test`

or if you have a specific version of python you need to use, e.g. 3.8

`$ conda create -p bio_test python=3.8` (Recommended!)

Note: you will need to have `python` and `pip` installed inside the env to pip install packages inside the env.

Activate the environment (needs to be executed whenever you need to use the conda env you have created)

`$ source activate yourenvname`

If you are using system installed conda, please DO NOT use `conda activate` to activate your environment

Install `yourpackage` in the conda env 

`$ conda install yourpackage`

Or if you have python (comes with pip) installed, 

`$ pip install yourpackage`

Or follow the instruction on package website.

Check what's installed in your conda environment

`$ conda list`

Test

`$ python`

`<<< import yourpackage`

`<<<`

When you are done, deactivate the environment

`$ source deactivate`

or 

`$ conda deactivate`

:)

## Additional Information for Jupyter Users:

### Run conda env as a kernel in Jupyter

If you would like to use JupyterNotebook or JupyterLab from OnDemand, you can follow the instructions below and **run your conda env as a kernel in Jupyter**.

- - - Make sure with python 3.7+ and make sure you load cluster's anaconda module (this only works with py3.7+)

    - Activate your conda env from terminal.

    - Install ipykernel with 

      `$ pip install ipykernel` (this assumes you installed python and pip in your env, otherwise, use "--user" flag)

    - Add your env to jupyter with 

      `$ python -m ipykernel install --user --name=myenvname` (use the name of your environment in the place of "myenvname")

    - Restart Jupyter from OnDemand

    - :)

### Create your conda environment with conda-env-mod


`$ cd /cluster/tufts/xli37/software/condaenv/`

`$ conda-env-mod create -p bio_test python=3.8  --jupyter`




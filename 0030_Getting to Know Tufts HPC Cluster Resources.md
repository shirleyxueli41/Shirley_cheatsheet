# **Getting to Know Tufts HPC Cluster Resources**

## Account & Storage Requests

Go to **[Tufts HPC website](https://it.tufts.edu/high-performance-computing)**

For Faculties ONLY: **[HPC for Classes](https://tufts.qualtrics.com/jfe/form/SV_d7o0UZFgK1PFXnv)**



## Tufts HPC Cluster

- Moved to **[MGHPCC](https://www.mghpcc.org/)** in January 2024!



## Cluster Storage

* __Home Directory__

Be aware! Your Home Directory (**30GB**, fixed) should be `/cluster/home/your_utln`

If you are not sure how much storage you have used in your home directory, feel free to contact us and we can provide you the number. 

Or, you can use `hpctools` (login or compute node) OR run `$ du -a -h --max-depth=1 ~ | sort -hr` from a **compute node** in your home directory to find out the detailed usage. 

* __Reserach Project Storage__

**[Request research project storage](https://it.tufts.edu/research-technology/)**

Your research projet storage (from **50GB and up**) path should be `/cluster/tufts/yourlabname/`, and each member of the lab group has a dedicated directory `/cluster/tufts/yourlabname/your_utln`

To see your **research project storage quota** by running the following command from **any node on the new cluster Pax**:

`$ df -h /cluster/tufts/yourlabname ` 

**NOTE:** Accessing your research project storage space for the __first time__ in your current session, please make sure you type out the __FULL PATH__ to the directory `/cluster/tufts/yourlabname/`.



## **Cluster Resource Limit**

* **Public Partitions** (batch+mpi+largemem+gpu) 

  * CPU: 500 cores

    RAM: 2000 GB

    GPU: 5

* **Preempt Partition** (preempt) 

  * CPU: 1000 cores

    RAM: 4000 GB

    GPU: 10



## Cluster Computing Resource Availability

`$ module load hpctools`

`$ hpctools` 

Then follow the on-screen instructions to extract the information you need. 



## CPUs

Compute nodes are grouped into **partitions** based on <u>functionality</u> and <u>priority</u> levels.

**Public Partitions :**

```
PARTITION       TIMELIMIT      
batch*          7-00:00:00          
gpu             7-00:00:00        
interactive     4:00:00        
largemem        7-00:00:00        
mpi             7-00:00:00         
preempt         7-00:00:00     
```

* **preempt** - Be aware, `preempt` partition consists of most of the nodes on the cluster, including **contrib nodes** from different research labs. When submitting jobs to preempt partition, you acknowledge that your jobs are taking the **risk** of being preempted by higher priority jobs. In that case, you will simply have to resubmit your jobs. 
* [**OnDemand**](https://ondemand.pax.tufts.edu) `Misc`-->`Inventory ` shows more node details (core count & memory)



## GPUs

__NVIDIA GPUs__ are available in `gpu` and `preempt` partitions

- **Request GPU resources with `--gres`. See details below.**

- If no specific architecture is required, GPU resources can be request with`--gres=gpu:1` (one GPU)

- You can request more than one type of GPUs with `constraint`, e.g.  

  `--gres=gpu:1 --constraint="t4|p100|v100"`

- Please **DO NOT** manually set `CUDA_VISIBLE_DEVICES`. 

- Users can ONLY see GPU devices that are assigned to them with `$ nvidia-smi`.

  If you submit batch jobs, it's recommended adding this command in your slurm job submission script.

- `gpu` partition`-p gpu`:

  - NVIDIA A100
    - In "gpu" partition
    - Request with: `--gres=gpu:a100:1`(one A100 GPU, can request up to 8 on one node)
    - `--constraint="a100-80G"`
    - Each GPU comes with 80GB of DRAM
    - Driver supports upto CUDA 12.2
  - NVIDIA P100s
    - In "gpu" partition
    - Request with: `--gres=gpu:p100:1`(one P100 GPU, can request up to 4 on one node)
    - `--constraint="p100"`
    - Each GPU comes with 16GB of DRAM
    - Driver supports upto CUDA 12.2
  - NVIDIA Tesla K20xm
    - In "gpu" partition
    - Request with: `--gres=gpu:k20xm:1`(one Tesla K20xm GPU, can request up to 1 on one node)
    - `--constraint="p100"`
    - Each GPU comes with 6GB of DRAM

- `preempt` partition `-p preempt`:
  - `a100`, `v100`, `p100`, ` rtx_6000`, `t4`
  - NVIDIA T4
    - In "preempt" partition
    - Request with: `--gres=gpu:t4:1`(one T4 GPU, can request up to 4 on one node)
    - `--constraint="t4"`
    - Each GPU comes with 16GB of DRAM
  - NVIDIA P100
    - In "preempt" partition
    - Request with: `--gres=gpu:p100:1`(one P100 GPU, can request up to 6 on one node)
    - `--constraint="p100"`
    - Each GPU comes with 16GB of DRAM
  - NVIDIA rtx_6000
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_6000:1`(one RTX_6000 GPU, can request up to 8 on one node)
    - `--constraint="rtx_6000"`
    - Each GPU comes with 24GB of DRAM
  - NVIDIA rtx_a6000
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_a6000:1`(one RTX_A6000 GPU, can request up to 8 on one node)
    - `--constraint="rtx_a6000"`
    - Each GPU comes with 48GB of DRAM
  - NVIDIA rtx_6000ada
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_6000ada:1`(one RTX_6000Ada GPU, can request up to 4 on one node)
    - `--constraint="rtx_6000ada"`
    - Each GPU comes with 48GB of DRAM
  - NVIDIA V100
    - In "preempt" partition
    - Request with: `--gres=gpu:v100:1`(one V100 GPU, can request up to 4 on one node)
    - `--constraint="v100"`
    - Each GPU comes with 16GB of DRAM
  - NVIDIA A100
    - In "preempt" partition
    - Request with: `--gres=gpu:a100:1`(one A100 GPU, can request up to 8 on one node)
    - `--constraint="a100-80G"`
    - `--constraint="a100-40G"`
    - `--constraint="a100"`
    - Each GPU comes with 40GB of DRAM or 80GB of DRAM



## Software, Modules, Packages

#### What are modules?

- A tool that **simplify** shell initialization and lets users easily modify their environment during the session with modulefiles

- Each modulefile contains the **information** needed to configure the shell for an application. (PATH, LD_LIBRARY_PATH, CPATH, etc.). Without modules, these environment variables need to be set manually in every new session where the application is needed. 

- Modules are useful in managing **different versions** of applications. 

- Modules can also be bundled into metamodules that will load an entire **set of different applications**. 

#### How to use modules?

> **Cheat Sheet**
>
> `module av` - check all available modules
>
> `module av <software>` - check if a specific software is available as a module
>
> `module list` - check loaded modules
>
> `module load <software>` - load a specific module
>
> `module unload <software>` - unload a specific module
>
> `module swap <loaded_software> <new_software>` - switch a loaded module for a new one
>
> `module purge` - unload all loaded modules

To **check available modules** installed on the cluster, this may take a few minutes as there are a lot of modules, and be sure to browse the entire list as there are several module file locations:

```
[tutln01@login-prod-01 ~]$ module av
```

Upon login, environment variable **`PATH`** is set for the system to search executables along these paths:

```
[tutln01@login-prod-01 ~]$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/cluster/home/tutln01/bin:/cluster/home/tutln01/.local/bin
```

For example, I would like to use `gcc` compiler, to check what versions of gcc compiler is available, load the version I would like to use, and use it:

```
[tutln01@login-prod-01 ~]$ module av gcc

----------------------------------------------------------- /opt/shared/Modules/modulefiles-rhel6 ------------------------------------------------------------
gcc/4.7.0 gcc/4.9.2 gcc/5.3.0 gcc/7.3.0

-------------------------------------------------------------- /cluster/tufts/hpc/tools/module ---------------------------------------------------------------
gcc/8.4.0 gcc/9.3.0 gcc/11.2.0
```

Use `module list` to **check loaded modules** in current environment:

```
[tutln01@login-prod-01 ~]$ module load gcc/7.3.0
[tutln01@login-prod-01 ~]$ module list
Currently Loaded Modulefiles:
  1) use.own     2) gcc/7.3.0
```

```
[tutln01@login-prod-01 ~]$ which gcc
/opt/shared/gcc/7.3.0/bin/gcc
[tutln01@login-prod-01 ~]$ echo $PATH
/opt/shared/gcc/7.3.0/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/cluster/home/tutln01/bin:/cluster/home/tutln01/.local/bin
[tutln01@login-prod-01 ~]$ gcc --version
gcc (GCC) 7.3.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

**swap a module for another** (doesn't have to be the same software):

```
[tutln01@login-prod-01 ~]$ module swap gcc/7.3.0 gcc/9.3.0 
[tutln01@login-prod-01 ~]$ module list
Currently Loaded Modulefiles:
  1) use.own     2) gcc/9.3.0
```

 **unload loaded modules**:

```
[tutln01@login-prod-01 ~]$ module unload gcc
[tutln01@login-prod-01 ~]$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/cluster/home/tutln01/bin:/cluster/home/tutln01/.local/bin
```

**unload ALL** of the loaded modules in the current environment:

```
[tutln01@login-prod-01 ~]$ module purge
```

#### Install Software/Packages

- [R](https://tufts.box.com/s/qximkv5ke2y4k0vbg6m04m6fc6exh88h) (R command line recommanded), packages need to be reinstalled for each version of R
  - **R/4.3.0 (recommended, newer version)**
    - HPC R repo `/cluster/tufts/hpc/tools/R/4.3.0`
  - **R/4.0.0 (lots of existing installed packages)**
    - HPC R repo `/cluster/tufts/hpc/tools/R/4.0.0`
  - R/4.1.1
    - HPC R repo `/cluster/tufts/hpc/tools/R/4.1`
  - R/4.2.0
    - HPC R repo `/cluster/tufts/hpc/tools/R/4.2.0`
- [Python](https://tufts.box.com/v/CondaEnvonHPC) (Conda env recommanded)
  - Not recommended: anaconda/3 (older version, source activate), only use this version when necessary
  - `anaconda/2021.05`, `anaconda/2021.11`, `miniconda/23.10` (newer conda version, **source activate**)
  - `mamba/22.9.0-2`
  - Use the same version of conda on one conda env every time
- Other software compiled from **source**
  - gcc
  - cmake
  - Autotools - automake, autoconf, autogen, .etc
  - ... any **dependencies**, load if available, install if not. Some environment variables may need to be set manually.
  - **Follow instructions** (read it through first)
  - Use **"--prefix="** to install in non-standard locations
  - Modify the environment variables !!! (such as PATH, LD_LIBRARY_PATH, CPATH, .etc)
  - You can make a private module for your locally installed software. Here is [HOW](https://tufts.box.com/s/fewt978g2hmmmhskm1n5dg4bj6xt0cdd)
  - OR you can submit a request to tts-research@tufts.edu for the software to be installed globally on the cluster. 


---


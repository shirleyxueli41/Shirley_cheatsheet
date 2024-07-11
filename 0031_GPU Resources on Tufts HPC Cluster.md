# GPU Resources on Tufts HPC Cluster

__NVIDIA GPUs__ are available in `gpu` and `preempt` partitions to all cluster users

- **Request GPU resources with `--gres`. See details below.**

- If no specific architecture is required, GPU resources can be request with`--gres=gpu:1` (one GPU)

- Please **DO NOT** manually set `CUDA_VISIBLE_DEVICES`. 

- You can ONLY see GPU devices that are allocated to you with `$ nvidia-smi`.

  

- `gpu` partition`-p gpu`:
  
  - **NVIDIA A100**
    - In "gpu" partition
    - Request with: `--gres=gpu:a100:1`(one A100 GPU, can request up to 8 on one node)
    - Each GPU comes with 80GB of DRAM
  - **NVIDIA P100*
    - In "gpu" partition
    - Request with: `--gres=gpu:p100:1`(one P100 GPU, can request up to 6 on one node)
    - Each GPU comes with 16GB of DRAM
  - **NVIDIA Tesla K20xm**
    - In "gpu" partition
    - Request with: `--gres=gpu:k20xm:1`(one Tesla K20xm GPU, can request up to 1 on one node)
    - Each GPU comes with 6GB of DRAM
  
- `preempt` partition `-p preempt`:
  - `a100`, `v100`, `p100`, ` rtx_6000`, `rtx_a6000`,`rtx_6000ada`, `t4`
  - **NVIDIA T4**
    - In "preempt" partition
    - Request with: `--gres=gpu:t4:1`(one T4 GPU, can request up to 4 on one node)
    - Each GPU comes with 16GB of DRAM
  - **NVIDIA P100**
    - In "preempt" partition
    - Request with: `--gres=gpu:p100:1`(one P100 GPU, can request up to 4 on one node)
    - Each GPU comes with 16GB of DRAM
  - **NVIDIA rtx_6000**
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_6000:1`(one RTX_6000 GPU, can request up to 8 on one node)
    - Each GPU comes with 24GB of DRAM
  - **NVIDIA rtx_a6000**
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_a6000:1`(one RTX_A6000 GPU, can request up to 8 on one node)
    - Each GPU comes with 48GB of DRAM
  - **NVIDIA rtx_6000ada**
    - In "preempt" partition
    - Request with: `--gres=gpu:rtx_6000ada:1`(one RTX_6000Ada GPU, can request up to 4 on one node)
    - Each GPU comes with 48GB of DRAM
  - **NVIDIA V100**
    - In "preempt" partition
    - Request with: `--gres=gpu:v100:1`(one V100 GPU, can request up to 4 on one node)
    - Each GPU comes with 16GB of DRAM
  - **NVIDIA A100**
    - In "preempt" partition
    - Request with: `--gres=gpu:a100:1`(one A100 GPU, can request up to 8 on one node)
    - Each GPU comes with 40GB of DRAM or 80GB of DRAM


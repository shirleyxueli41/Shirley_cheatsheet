
# SLURM Environment Variables

| Variable                   | Description                                             |
| -------------------------- | ------------------------------------------------------- |
| `$SLURM_JOB_ID`            | The Job ID.                                             |
| `$SLURM_JOBID`             | Deprecated. Same as `$SLURM_JOB_ID`.                    |
| `$SLURM_SUBMIT_DIR`        | The path of the job submission directory.               |
| `$SLURM_SUBMIT_HOST`       | The hostname of the node used for job submission.       |
| `$SLURM_JOB_NODELIST`      | Contains the definition (list) of nodes assigned.       |
| `$SLURM_NODELIST`          | Deprecated. Same as `$SLURM_JOB_NODELIST`.              |
| `$SLURM_CPUS_PER_TASK`     | Number of CPUs per task.                                |
| `$SLURM_CPUS_ON_NODE`      | Number of CPUs on the allocated node.                   |
| `$SLURM_JOB_CPUS_PER_NODE` | Count of processors available to the job on this node.  |
| `$SLURM_CPUS_PER_GPU`      | Number of CPUs requested per allocated GPU. (MB)        |
| `$SLURM_MEM_PER_CPU`       | Memory per CPU. Same as `--mem-per-cpu`. (MB)           |
| `$SLURM_MEM_PER_GPU`       | Memory per GPU. (MB)                                    |
| `$SLURM_MEM_PER_NODE`      | Memory per node. Same as `--mem`. (MB)                  |
| `$SLURM_GPUS`              | Number of GPUs requested.                               |
| `$SLURM_NTASKS`            | Same as `-n`, `--ntasks`. Number of tasks.              |
| `$SLURM_NTASKS_PER_NODE`   | Number of tasks requested per node.                     |
| `$SLURM_NTASKS_PER_SOCKET` | Number of tasks requested per socket.                   |
| `$SLURM_NTASKS_PER_CORE`   | Number of tasks requested per core.                     |
| `$SLURM_NTASKS_PER_GPU`    | Number of tasks requested per GPU.                      |
| `$SLURM_NPROCS`            | Same as `-n`, `--ntasks`. See `$SLURM_NTASKS`.          |
| `$SLURM_NNODES`            | Total number of nodes in the job’s resource allocation. |
| `$SLURM_TASKS_PER_NODE`    | Number of tasks to be initiated on each node.           |
| `$SLURM_ARRAY_JOB_ID`      | Job array’s master job ID number.                       |
| `$SLURM_ARRAY_TASK_ID`     | Job array ID (index) number.                            |
| `$SLURM_ARRAY_TASK_COUNT`  | Total number of tasks in a job array.                   |
| `$SLURM_ARRAY_TASK_MAX`    | Job array’s maximum ID (index) number.                  |
| `$SLURM_ARRAY_TASK_MIN`    | Job array’s minimum ID (index) number.                  |

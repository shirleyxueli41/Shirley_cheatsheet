2024-05-15



module load biobakery_workflows/3.1 
module load  metaphlan/4.0.6 
module load  kneaddata/0.12.0 


```bash

module load  singularity/3.8.4

export SINGULARITY_CACHEDIR=/cluster/tufts/xli37/softwares/biobakery

singularity pull docker://biobakery/workflows:latest

singularity exec workflows_latest.sif bash

mkdir -p /cluster/tufts/xli37/softwares/cache/pip3/
mkdir -p /cluster/tufts/xli37/softwares/lib/python3.6/site-packages

export PIP_CACHE_DIR=/cluster/tufts/xli37/softwares/cache/pip3/
export PYTHONUSERBASE=/cluster/tufts/xli37/softwares/lib/python3.6/site-packages
export PATH=/cluster/tufts/xli37/softwares/lib/python3.6/site-packages/bin:$PATH
pip3 install --user --upgrade biobakery_workflows
biobakery_workflows --version
metaphlan --version
kneaddata --version
humann --version

pip3 install --user --upgrade metaphlan
pip3 install --user --upgrade kneaddata
pip3 install --user --upgrade humann

export PATH=/cluster/tufts/xli37/softwares/lib/python3.6/site-packages/bin:$PATH

metaphlan --version
kneaddata --version
humann --version


pip3 install --user --upgrade biobakery_workflows


module load anaconda/2021.05
conda create -n biobakery_workflows python=3.8
conda activate biobakery_workflows

```






Latest metaphlan database is in 
`/cluster/tufts/biocontainers/datasets/metaphlan/202307/`



Results:
```Read Pairs: 4316384 
Both Surviving: 3462299 (80.21%) 
Forward Only Surviving: 133380 (3.09%) 
Reverse Only Surviving: 71486 (1.66%) 
Dropped: 649219 (15.04%)
```



```
05/15/2024 08:29:30 PM - kneaddata.utilities - INFO: READ COUNT: trimmed pair1 : Total reads after trimming ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240.trimmed.1.fastq ): 3462299.0
05/15/2024 08:29:34 PM - kneaddata.utilities - INFO: READ COUNT: trimmed pair2 : Total reads after trimming ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240.trimmed.2.fastq ): 3462299.0



05/15/2024 08:35:13 PM - kneaddata.run - INFO: Total number of sequences with repeats removed from file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240.trimmed.1.fastq ): 558117
05/15/2024 08:35:17 PM - kneaddata.run - INFO: Total number of sequences with repeats removed from file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240.trimmed.2.fastq ): 268339


05/15/2024 08:36:45 PM - kneaddata.run - INFO: Total contaminate sequences in file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240_hg37dec_v0.1_bowtie2_paired_contam_1.fastq ) : 0.0
05/15/2024 08:36:45 PM - kneaddata.run - INFO: Total contaminate sequences in file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240_hg37dec_v0.1_bowtie2_paired_contam_2.fastq ) : 0.0
05/15/2024 08:36:45 PM - kneaddata.run - INFO: Total contaminate sequences in file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240_hg37dec_v0.1_bowtie2_unmatched_1_contam.fastq ) : 8831.0
05/15/2024 08:36:45 PM - kneaddata.run - INFO: Total contaminate sequences in file ( /cluster/tufts/xli37/test_run/biobakery/biobakery_output/kneaddata/main/Gloeocapsa_S240_hg37dec_v0.1_bowtie2_unmatched_2_contam.fastq ) : 9270.0
```



Kneaddata results in unpaired output. 
https://forum.biobakery.org/t/paired-end-data-results-in-unpaired-output/928/14


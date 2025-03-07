# Parallel Read Alignment Using SLURM Job Arrays

This documentation outlines the process for running **read alignment in parallel** using the SLURM job scheduler. Specifically, it describes how to **map and align Illumina reads to a reference genome** while taking advantage of **SLURM job arrays** for efficient batch processing.

By using job arrays, you can submit a single SLURM job that handles multiple samples, allowing SLURM to distribute and schedule jobs dynamically across available compute nodes.

---

## Prerequisites  
Before proceeding, ensure you have the following:  

- Access to a SLURM-managed high-performance computing (HPC) cluster.  
- Installed modules for **BWA** and **SAMtools** (available as modules on Tufts HPC).  
- A **text file (`samples.txt`)** containing the list of paired-end read files for each sample.  
- Read and write permissions for the data and output directories.  

---

## Step-by-Step Guide  

### 1. Prepare the Sample List  
Create a text file named `samples.txt` (or any other name), where each line contains the paired-end read files for a sample. The format should be:  

```
sample1_R1.fastq sample1_R2.fastq
sample2_R1.fastq sample2_R2.fastq
...
sample20_R1.fastq sample20_R2.fastq
```

Each row represents a sample, where `R1` and `R2` are the forward and reverse reads, respectively.  

---

### 2. SLURM Job Array Script: `alignment_array.sh`  

Instead of submitting jobs one by one, we will use **SLURM job arrays**. This script will:  
- Read the sample list file.  
- Assign each sample to a **SLURM_ARRAY_TASK_ID** (so each job processes a different sample).  

#### SLURM Script (`alignment_array.sh`)
```bash
#!/bin/bash -l
#SBATCH -J array_alignment
#SBATCH -p batch
#SBATCH -N 1              # Run each array job on one node
#SBATCH --cpus-per-task=4 # Use 4 CPU cores per job
#SBATCH --mem=16G         # Allocate 16 GB memory per job
#SBATCH --time=24:00:00
#SBATCH --array=1-20      # Submit a job array for 20 samples (adjust based on `samples.txt`)
#SBATCH --output=MyJob_%A_%a.out
#SBATCH --error=MyJob_%A_%a.err
#SBATCH --mail-type=ALL
#SBATCH --mail-user=name@tufts.edu

# Load necessary modules
module load bwa/0.7.17
module load samtools/1.9

# Define directories
DATA_DIR="/path/to/data"
REF_GENOME="/path/to/reference/genome.fa"
OUTPUT_DIR="/path/to/output"

# Read the sample list and get the line corresponding to this job's array task ID
READ1=$(sed -n "${SLURM_ARRAY_TASK_ID}p" samples.txt | awk '{print $1}')
READ2=$(sed -n "${SLURM_ARRAY_TASK_ID}p" samples.txt | awk '{print $2}')

# Define input and output file paths
READ1=${DATA_DIR}/${READ1}
READ2=${DATA_DIR}/${READ2}
OUTPUT_BAM=${OUTPUT_DIR}/sample_${SLURM_ARRAY_TASK_ID}.bam
SORTED_BAM=${OUTPUT_DIR}/sample_${SLURM_ARRAY_TASK_ID}_sorted.bam

# Run read alignment with BWA
bwa mem -t 4 ${REF_GENOME} ${READ1} ${READ2} | samtools view -bS - > ${OUTPUT_BAM}

# Sort and index BAM file
samtools sort -o ${SORTED_BAM} ${OUTPUT_BAM}
samtools index ${SORTED_BAM}

echo "Alignment for sample ${SLURM_ARRAY_TASK_ID} completed"
```

---

### 3. Submit the SLURM Job Array  
To submit the job, simply run:  

```bash
sbatch alignment_array.sh
```

This **automatically** schedules **one job per sample**, up to the number specified in `--array=1-20`. Each job runs independently, aligning its assigned sample.

---

## Why Use SLURM Job Arrays?
✅ **Efficient Resource Management**: SLURM automatically distributes jobs across nodes based on availability.  
✅ **Scalability**: Easily scale up to hundreds of samples by adjusting `--array=1-N`.  
✅ **Reduced Submission Overhead**: Instead of submitting multiple jobs, a **single SLURM submission** manages everything.  

---

### 4. Monitoring Job Progress  
After submission, you can check the job status with:

```bash
squeue -u $USER
```

Or check logs using:

```bash
tail -f MyJob_*.out
```

---

## Conclusion  
This approach allows you to **parallelize read alignment efficiently** on an HPC cluster. By leveraging **SLURM job arrays**, you optimize compute resources, minimize submission overhead, and ensure efficient batch processing.

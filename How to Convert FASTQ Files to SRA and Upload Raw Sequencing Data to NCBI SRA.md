# How to Convert FASTQ Files to SRA and Upload Raw Sequencing Data to NCBI SRA

## 1. Convert FASTQ Files to SRA Format (Optional)

If you have raw FASTQ files, you can optionally convert them to SRA format using the **SRA Toolkit**, though it's not required.

### **Convert FASTQ to SRA:**
```bash
fastq-dump --split-files --gzip sample1.sra
```

Since you already have FASTQ files, you can proceed directly to uploading.

---

## 2. Prepare Metadata for SRA Submission

NCBI requires metadata files for submission. You need:
- **BioProject**: Describes the study.
- **BioSample**: Describes each biological sample.
- **SRA Metadata**: Lists sequencing runs and details.

### **(a) Register a BioProject**
1. Go to the [NCBI BioProject Submission Portal](https://submit.ncbi.nlm.nih.gov/subs/bioproject/).
2. Click “New Submission” and provide details about your study.

### **(b) Register BioSamples**
1. Go to the [NCBI BioSample Submission Portal](https://submit.ncbi.nlm.nih.gov/subs/biosample/).
2. Provide sample information (e.g., species, tissue type, sequencing method).
3. Once registered, you’ll receive **BioSample accession numbers**.

---

## 3. Prepare SRA Metadata File

Create a **sra_metadata.tsv** file following this format:

| sample_name | title              | library_strategy | library_source | library_selection | library_layout | platform | instrument_model | filename            | filename2           |
| ----------- | ------------------ | ---------------- | -------------- | ----------------- | -------------- | -------- | ---------------- | ------------------- | ------------------- |
| Sample1     | RNA-seq of Sample1 | RNA-Seq          | TRANSCRIPTOMIC | cDNA              | PAIRED         | ILLUMINA | NovaSeq 6000     | Sample1_R1.fastq.gz | Sample1_R2.fastq.gz |
| Sample2     | RNA-seq of Sample2 | RNA-Seq          | TRANSCRIPTOMIC | cDNA              | PAIRED         | ILLUMINA | NovaSeq 6000     | Sample2_R1.fastq.gz | Sample2_R2.fastq.gz |

For **samples with duplicate runs**, add extra rows with different filenames.

---

## 4. Upload FASTQ Files to NCBI SRA

### **Method 1: Upload via Aspera (Recommended for Large Datasets)**

#### **Install Aspera CLI:**
Download from [IBM Aspera CLI](https://downloads.asperasoft.com/en/downloads/8)

#### **Upload Files:**
```bash
ascp -QT -l 300M -P 33001 -i ~/.aspera/connect/etc/asperaweb_id_dsa.openssh \
sample1_R1.fastq.gz sample1_R2.fastq.gz \
subasp@upload.ncbi.nlm.nih.gov:/uploads/your_ncbi_username/
```
(Replace `your_ncbi_username` with your actual NCBI login.)

### **Method 2: Upload via FTP (Slower)**
```bash
ftp ftp-private.ncbi.nlm.nih.gov
cd uploads/your_ncbi_username/
mput sample1_R1.fastq.gz sample1_R2.fastq.gz
```

---

## 5. Submit SRA Metadata and Finalize Submission

1. Go to the [NCBI SRA Submission Portal](https://submit.ncbi.nlm.nih.gov/subs/sra/).
2. Click **New Submission**.
3. Link your submission to the **BioProject** and **BioSample** accessions.
4. Upload the **sra_metadata.tsv** file.
5. Confirm the uploaded FASTQ files.
6. Submit!

After review, you will receive **SRA accession numbers**.

---

## 6. Making the Submission Private & Releasing Later

- Set a **future release date** or keep it **private indefinitely**.
- Share **private SRA accession numbers** with journal reviewers.
- After paper acceptance, manually **release data** from the [NCBI Submission Portal](https://submit.ncbi.nlm.nih.gov/subs/).

---

## 7. Adding More Samples After Initial Submission

If your BioProject is already created, you can **submit additional samples later**:

1. **Your coworker must share the BioProject with you** via the NCBI Submission Portal.
2. Prepare a **new SRA metadata file** for the additional samples.
3. Submit a **new BioSample submission** linked to the existing BioProject.
4. Upload the additional FASTQ files.

---

## **Summary of Steps**
1. **Prepare BioProject & BioSample records**.
2. **Create SRA metadata file** (TSV).
3. **Upload FASTQ files** using **Aspera** or **FTP**.
4. **Submit metadata & confirm files** in the NCBI SRA portal.
5. **Optionally keep private** until publication.
6. **Add more samples later if needed**.

Let me know if you need any clarifications! 🚀
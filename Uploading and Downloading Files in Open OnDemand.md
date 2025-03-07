# Uploading and Downloading Files in Open OnDemand



Open OnDemand provides an easy-to-use web interface for managing files on a high-performance computing (HPC) cluster. This tutorial will guide you through the steps to **upload, download, and save files to a specific folder**.



## 1. Accessing Open OnDemand

1. Connect to VPN if you are not on campus. 
2. Open a web browser and go to [Open OnDemand portal](https://ondemand.pax.tufts.edu/).
3. Log in with your Tufts credentials.



## 2. Navigating to the File Manager

1. On the Open OnDemand dashboard, locate the **`Files`** section.

2. Click on **"Home Directory"** or navigate to the specific storage location (e.g., `/cluster/tufts/lab/`, or a project directory). Your home directory path should be `/cluster/home/yourutln/`

## 3. Uploading Files

To upload a file to the cluster:

1. Navigate to the folder where you want to store the file by clicking `Go To...` button. Enter the directory you would like to store your file. If it's your home directory, then the path should be `/cluster/home/yourutln/`. If it's your lab storage space, it should be something like `/cluster/tufts/lab/yourutln/projectfolder/`
2. Click the **"Upload"** button at the top of the File Manager.
3. Select files from your local computer.
4. Click **"Open"** or **"Upload"** to start the transfer.
5. The uploaded file will now appear in the selected directory.



## 4. Downloading Files

To download a file from the cluster:

1. Locate the file you want to download in the File Manager.
2. Click on the file name to select it.
3. Click the **"Download"** button.
4. The file will be downloaded to your local computer’s default download location.



## **5. Moving Files to a Specific Folder**

If you've uploaded files to the wrong location, you can move them:

1. Locate the file in the File Manager.
2. Select the file(s).
3. Click **"Rename/Move"** and choose the target directory.
4. Confirm the move.

Alternatively, you can move files using the **Terminal**:

`mv ~/myfile.txt /work/my_project/`



## 6. Reading Files in RStudio

After uploading your data, you can read it into **RStudio on Open OnDemand**.

### **Opening RStudio on Open OnDemand**

1. From the Open OnDemand **dashboard**, locate and open **"Interactive Apps"**.
2. Select **"RStudio Pax"**.
3. Choose the appropriate settings (e.g., requested memory and CPU cores).
4. Click **Launch** and wait for RStudio to start.



### **Navigating to Your Data in R**

By default, RStudio starts in your home directory (`/cluster/home/yourutln`). If your files are stored in another location, such as `/cluster/tufts/lab/yourutln/projectfolder/`, you need to change your working directory.

#### **Set the Working Directory**

```
setwd("/cluster/tufts/lab/yourutln/projectfolder/")
```

Verify the change:

```
getwd()
```

#### **Reading a CSV File**

```
data <- read.table("myfile.csv", header = TRUE, sep = ",", stringsAsFactors = FALSE)
```

#### **Reading a TSV File**

```
data <- read.table("myfile.tsv", header = TRUE, sep = "\t", stringsAsFactors = FALSE)
```

#### **Reading an Excel File (.xlsx)**

Install and load the `readxl` package first:

```
install.packages("readxl")
library(readxl)
data <- read_excel("myfile.xlsx", sheet = 1)
```




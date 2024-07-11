# Navigate Cluster Storage

Prerequisites:

- Active Tufts HPC Cluster Account

- 2FA is required with Tufts network login via command line

- Tufts VPN if not on Tufts network

  

To check your home directory or group project storage usage, run following commands on the cluster:

$ `module load hpctools`

$ `hpctools`

Then follow the on screen instructions to select the information you wish to obtain.

## Home Directory

Your Home Directory (30GB, fixed) should be `/cluster/home/your_utln`

Using commands `cd ~` or `cd` or `cd $HOME` will take you back to your home directory on the HPC Cluster.

If you are working on projects in a group and will need to store large amount of data on the cluster, we do not recommand using your own home directory as the working directory for these projects.

Once your home directory fills up, you will not be able to run many programs such as python, R, matlab, .etc on the HPC cluster nor any OnDemand Interactive Apps. 

**Please keep your home directory usage well under the 30GB limit.**



## Reserach Project Storage

If you don't already have access to your group's research project storage space on Tufts HPC cluster, please fill out the [Cluster Storage Request](https://tufts.qualtrics.com/jfe/form/SV_5bUmpFT0IXeyEfj) form.

Your research projet storage (from 50GB and up) path should be `/cluster/tufts/yourlabname/`, and each member of the lab group has a dedicated directory `/cluster/tufts/yourlabname/your_utln`

To see your **research project storage quota** by running the following command from **any node on the HPC Cluster**:

`$ df -h /cluster/tufts/yourlabname ` 

**NOTE***: 

Accessing your research project storage space for the __first time__ in your current cluster session, please make sure you type out the **full path** to the directory.

**NOTE****:

Not all research folders are listed/mounted under /cluster/tufts on the node you are currently accessing. You may NOT see all research project storage folders when executing $`ls /cluster/tufts`


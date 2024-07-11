# Login

Prerequisites:

- Active Tufts HPC Cluster Account
- 2FA is required with Tufts network login via command line
- Tufts VPN if not on Tufts network

Login hostname: `login.cluster.tufts.edu`

There are 3 login nodes: `login-prod-01`, `login-prod-02`, `login-prod-03`

## SSH

***Please DO NOT run any software on the login nodes.***

Shell environment (default: bash):

`$ ssh your_utln@login.cluster.tufts.edu`

With GUI (Graphical User Interface), X Window system needs to be installed on your local computer:

`$ ssh -XC your_utln@login.cluster.tufts.edu`

or

`$ ssh -YC your_utln@login.cluster.tufts.edu`

Now you are on a **Login Node** of the cluster (login-prod-0x) and in your **Home Directory** (~ or */cluster/home/your_utln*). 

`$ [your_utln@login-prod-02 ~]`

***Please DO NOT run any software on the login nodes.***

##  OnDemand

Go to [**OnDemand**](https://ondemand.pax.tufts.edu)

Use your **Tufts UTLN** and **password** to login. 

TAH-DAH! You are on Tufts HPC cluster!

__`Clusters`__, you can start a shell access to the HPC cluster. 

**`Tufts HPC Shell Access`** = `$ ssh your_utln@login.pax.tufts.edu`

Or use the `>_Open in Terminal` button in `Files` to open a terminal in whichever directory you navigated to.



If you need X11 access through OnDemand to display any GUI applications, please temporarily use our [OnDemand](https://ondemand.pax.tufts.edu) **`Clusters`** for this option:

**`Tufts HPC FastX11 Shell Access`** = `$ ssh -XC your_utln@login.pax.tufts.edu` (with X11 for GUI applications)

OR 

you also have the option to use the `Xfce Terminal` under new  [OnDemand](https://ondemand.pax.tufts.edu) `Interactive Apps`.
# **Tufts HPC Cluster Access**



---

> **VPN**
>
> - Off-campus Non-Tufts Network please connect to [Tufts VPN](https://access.tufts.edu/vpn)

> __2FA__
>
> * DUO is needed on Tufts Network (not needed for [**OnDemand**](https://ondemand.pax.tufts.edu), https://ondemand.pax.tufts.edu)
> * DUO is needed when using FastX11 from  [__OnDemand__](https://ondemand.pax.tufts.edu)

> **SSH**
>
> - The SSH protocol aka **Secure Shell** is a method for secure remote login from one computer to another. 

> **X Window System (X11)**
>
> - The X Window System (X11) is an open source, cross platform,  client-server computer software system that provides a **GUI** in a  distributed network environment.

> **Login Hostname**
>
> - login.cluster.tufts.edu = login.pax.tufts.edu
>
> **Cluster New User Guides**
>
> - [Table of Contents](https://tufts.box.com/v/HPC-Table-of-Contents)



## OnDemand

Preferred browser: **Chrome or FireFox**

#### Login

Go to [**OnDemand**](https://ondemand.pax.tufts.edu), https://ondemand.pax.tufts.edu



<img src="https://raw.githubusercontent.com/DelilahYM/ImageHost/master/ondemand_login.png" alt="Core-Node" width=70%>

Use your **Tufts UTLN** and **password** to login. 

<img src="https://raw.githubusercontent.com/DelilahYM/ImageHost/master/ondemand_home.png" alt="Core-Node" width=70%>



<img src="https://raw.githubusercontent.com/DelilahYM/ImageHost/master/ondemand_menu.png" alt="Core-Node" width=70%>

__`Clusters`__, you can start a shell access to the HPC cluster. 

**`Tufts HPC Shell Access`** = `$ ssh your_utln@login.cluster.tufts.edu `= `$ ssh your_utln@login.pax.tufts.edu `

OR

Use the `>_Open in Terminal` button in `Files` to open a terminal in whichever directory you navigated to.

If you need X11 access through OnDemand to display any GUI applications, please use our [OnDemand](https://ondemand.pax.tufts.edu) **`Clusters`** for this option:

**`Tufts HPC FastX11 Shell Access`** = `$ ssh -XYC your_utln@login.cluster.tufts.edu` (with X11 for GUI applications)

[FastX Web/Desktop Client Setup Instructions](https://tufts.box.com/s/s1vig4km289dzx8qkq4mbhlp4es0oxu1)

OR 

You also have the option to use the `Xfce Terminal` under new  [OnDemand](https://ondemand.pax.tufts.edu) `Interactive Apps` with limited computing resources.



## Shell Access

### Mac OSX & Linux

#### Login

- **Terminal**   <img src="https://agaric.coop/sites/default/files/2019-04/Terminalicon2.png" alt="Terminal" width=10%>   

  - Shell environment (default: bash):

    `$ ssh your_utln@login.cluster.tufts.edu`

    `$ ssh your_utln@login.cluster.tufts.edu`

    With GUI (Graphical User Interface):

    `$ ssh -XC your_utln@login.cluster.tufts.edu`

    or

    `$ ssh -YC your_utln@login.cluster.tufts.edu`

    X Window System need to be locally installed.

    Now you are on a **Login Node** of the cluster (login-prod-[01-03]) and in your **Home Directory** (~). 

    `$ [your_utln@login-prod-03 ~]`

  * Setting up [SSH keyless access](_https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/_) 
    * Be sure your `~/.ssh` permission is correct! Otherwise, SSH won't work properly.
    * `. ssh` directory: 700 ( drwx------ )
    * public key ( `. pub` file): 644 ( -rw-r--r-- )
    * private key (` id_rsa` ): 600 ( -rw------- )

---

### Windows

#### Login

- **[PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/learn/remoting/ssh-remoting-in-powershell-core?view=powershell-7.2)**
- **[WSL - Windows Subsystem for linux](https://learn.microsoft.com/en-us/windows/wsl/install)**
- **[PuTTY](https://www.putty.org/)**  
- **[Cygwin](https://www.cygwin.com/)** 

> **Hostname**: `login.cluster.tufts.edu` or `login.pax.tufts.edu`

## 
## SSH Keys 

### General overview

The SSH key enables secure, passwordless access to remote systems such as Tufts HPC. It is easy to set up and provides greater security than using a password, while being convenient as well.

Here are the steps to connect to the Tufts HPC using an SSH key: 

1. Generate a key pair (private and public key) on your local machine. 

2. Copy the public key to the cluster and append it to the $HOME/.ssh/authorized_keys file. 
3. Test if you can SSH from your local computer to the cluster without using your Tufts password.

Detailed steps for setting up SSH key on different operating systems are given below.

### Steps (Mac) :

1. Run `ssh-keygen` in the terminal on your local computer. You can choose to provide a filename and a passphrase to protect your private key, but it's not mandatory. To use the default settings, simply press Enter without specifying a filename. 

   **Do not leave the passphrase empty**. If you do not protect your private key with a passphrase, anyone with access to your local computer could SSH to your account on Tufts HPC. 

2. By default, the keys will be stored in `~/.ssh/id_rsa`(private) and `~/.ssh/id_rsa.pub`(public) on your local computer.

3. Copy the public key into $HOME/.ssh/authorized_keys on the cluster using the following command. When prompted for a password, enter your Tufts password. You will then receive a notification on your Duo app to approve the login.

   `ssh-copy-id -i ~/.ssh/id_rsa.pub myusername@login.pax.tufts.edu`

   **Note**: use your actual Tufts username.

   If your local computer does not support the `ssh-copy-id` command, use this alternative method instead.

   ```
   cat ~/.ssh/id_rsa.pub | ssh myusername@login.pax.tufts.edu "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys"
   ```

4. Test the new SSH key by logging into the cluster. You should now be able to SSH into the cluster using only the passphrase, without needing to enter your Tufts password or approve the login via your Duo app.

5. (Optional) If the private key has a non-default name or location, you need to specify the key by

   ```
   ssh -i my_private_key_name myusername@login.pax.tufts.edu
   ```

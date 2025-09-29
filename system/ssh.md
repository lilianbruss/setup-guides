# SSH Configuration for Remote Connection
To connect to a remote machine, we use Secure Shell (ssh). You need some information about the host machine (name, IP, port), and additionally set up
a private and public key pair to enable automated connection without re-typing your password each time you connect. 

## Setting up a Key Pair:

Run the following commands in your Windows or WSL Distribution Terminal, depending on where the keys should be saved. If the remote connection shall be 
possible from inside the WSL environment, establish them for your Linux user. Note that VS Code extensions as a Windows Process might have trouble accessing the 
private key in your WSL .ssh directory to grant HOST connection without password if the keys are not generated (or copied to) the Windows User as well.

**Keys must exist wherever the SSH client runs from!**


* Type `ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa` in Debian or
* `ssh-keygen -t rsa -b 4096 -f $env:USERPROFILE\.ssh\id_rsa` in Windows PS and leave the passphrase empty for automated login both times,
* copy the public key to the remote server in the following step.

Now you should have two files (id_rsa and id_rsa.pub) in the .ssh folder of the passed directory.

## Authentification with the Remote Machine:

For a first login, you just manually type your credentials in the terminal. Run:
* `ssh -p <port> <username>@<hostname or IP>` 

You'll have to enter your password this time. Authentification might also require confirmation of the server fingerprint to verify server identity, since it has
not yet been added to known hosts. Run the command again after confirmation to connect to the server - look for the message of the day (MOTD) that most Linux
Servers print after a successful login.
 
Next, we need to take a look at the .ssh folder on the remote machine. Run:
* `mkdir -p ~/.ssh` to create a ssh-folder in case it does not already exist,
* `ls ~/.ssh` to see what's in the folder as of now,
* `touch ~/.ssh/authorized_keys` to add an authorized keys file,
* `chmod 700 ~/.ssh` to change the permissions on the passed folder,
* `chmod 600 ~/.ssh/authorized_keys` to change the permissions on the passed file,
* `echo "PASTE_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys` to add your public key,
* `exit`to disconnect from the remote.

To ensure SSH security, set the following permissions:

- `.ssh/` directory:  
  `700` — Owner can read, write, and enter; group and others have no permissions.

- `authorized_keys` file inside `.ssh/`:  
  `600` — Owner can read and write; group and others have no permissions.


## Configuration: 

In your Windows/WSL .ssh folder, open (or create) the `.ssh/config` file and add:

```
Host <host_name>
    HostName <hostname_or_ip>
    User <username>
    Port <port>
    IdentityFile <path_to_private_key>
```

Set its permissions by running `chmod 600 ~/.ssh/config`.

When specifying the path to your private key in the SSH config file, use a placeholder `%d` to represent your user’s home directory.

For example:
- `%d/.ssh/id_edxxxxx`

Here, `%d` will be replaced by your actual home directory path, such as:

- For **WSL/Linux**: `~/.ssh/id_rsa`
- For **Windows PowerShell**: `$env:USERPROFILE\.ssh\id_rsa`

Using this configuration in your SSH config file allows you to connect to the remote server **passwordlessly** by simply typing:
```
ssh <your_host_name>
```
instead of entering the full command from before.

## Using SSH Connections in VS Code

Once your SSH setup is working correctly, you can enhance your workflow with Visual Studio Code by installing the following extensions:

- **Remote - SSH**
- **Remote Explorer**


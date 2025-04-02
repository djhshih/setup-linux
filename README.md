# How to setup a newly created Linux account

## Setting up MobaXterm

MobaXterm is a Windows-based remote desktop terminal offering remote networking tools such as SSH, X11 and also Unix commands.
When you first launch MobaXterm, go to Settings -> Configuration -> General and change your Persistent home directory. It is highly recommended to change your home directory to C:\Users\\<<Username\>>.
Once set, restart MobaXterm to apply this change.

## Virtual machine

Here are the steps of setting up Fedora on VirtualBox:

1. Download VirtualBox (https://www.virtualbox.org/wiki/Downloads) and Live ISO file for Fedora Workstation (https://fedoraproject.org/workstation/download).
1. Open VirtualBox and create a new virtual machine (VM). Choose a custom name for the VM and select the recently-downloaded ISO file.
1. Choose base memory, processors and virtual hard disk size you are willing to allocate to the VM (e.g. base memory: 8GB, processors: 8CPU, virtual HDD size: 250GB).  
1. Bootup the VM and start Fedora Workstation. Once it boots to desktop, select Install to Hard Drive and choose English (US) for language settings.
1. Click on installation destination. Choose the virtual hard disk and custom installation before performing manual partitioning.  
1. In the manual partitioning section, select standard partition. Create mount points for /home, /boot, / and biosboot with your desired capacities (e.g. /home: 200GB, /: 20GB, /boot: 0.5GB, biosboot: 1MB).  
1. Click Done, Accept Changes and wait for Fedora installation to complete.
1. Once complete, turn off the VM and go to Storage settings of the VM to remove ISO file from Controller: IDE.
1. Reboot the VM and Fedora will be successfully installed onto the VM.

## SSH key and GitHub/Bitbucket/GitLab

Applies to both local machine and remote server

### Generate SSH keys

We will generate the ssh key through the terminal, at the end, you will have two ssh keys: private ssh key and public ssh key.

Below are the steps to generate SSH keys:

1. open terminal
2. run `ssh-keygen -t ed25519 -C "your_email@example.com"`

There will be a prompt on where to save the files, like the following:

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (some_path/.ssh/id_ed25519):
```

3. Simply press Enter to store the files in the default file location.

Then you will see a message indicate that you have successfully created a new directory for the ssh files, as well as` a password prompt, like the following:

```
Created directory 'some_path/.ssh'.
Enter passphrase (empty for no passphrase):
```

4. Type your preferred passphrase through the prompt, you will need to type the same passphrase twice, in which the second time is to confirm that the passphrase is the same and correct.
   
```
Enter passphrase (empty for no passphrase): [Type a passphrase] # first time
Enter same passphrase again: [Type passphrase again] # second time
```

You will get messages like the following:

```
Your identification has been saved in `/some_path/.ssh/id_ed25519`.
Your public key has been saved in `/some_path/.ssh/id_ed25519.pub`.
The key fingerprint is:
some string + your enter email
The key's randomart image is:
some image
```

which indicates that you have successfully created SSH keys.

To double check that you have create the SSH keys, you may look into the ssh directory (i.e., `cd ~/.ssh`) and should have two files named: `id_ed25519` and `id_ed25519.pub`.

- `id_ed25519` is the private key **DO NOT** share with anyone
- `id_ed25519.pub` is the public key, which will be added to GitHub/Bitbucket/GitLab


Reference: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent


### Adding SSH keys to GitHub/Bitbucket/GitLab

#### Copy SSH public key

We will need to first copy the SSH public key.

The SSH public key locates in the SSH directory (i.e., `~/.ssh/`)

Steps to copy SSH public key

1. Enter the SSH directory -  `cd ~/.ssh/`
2. Open the file that stores your public key - `vim ./id_ed25519.pub`
3. Copy the content (i.e., SSH public key) to your clipboard

#### Adding SSH public key to GitHub

Steps to add SSH public key to GitHub:

1. Login to [GitHub](https://github.com/)
2. Click on your avatar on the top right
3. Click "Settings"
4. Click "SSH and GPG keys", which locates on the left side-bar under the "Access" section
5. Click "New SSH key" near the top right
6. Fill in the blanks:
   - "Title": a label for the new key, ex. "school-sever"
   - "Key type": would be "Authentication Key" (default)
   - "Key": the SSH public key
7. Click "Add SSH Key"
8. Done

#### Adding SSH public key to Bitbucket

1. Login to [Bitbucket](https://bitbucket.org/account/workspaces)
2. Click on the cog icon (i.e., Settings) on the top right
3. Select "Personal Bitbucket settings" under the dropdown meun
4. On the left-side bar, select "SSH keys" under the "SECURITY" section
5. Click "Add key"
6. Fill in the details:
   - "Label": a label for the new key, ex. "school-sever"
   - "Key": the SSH public key
7. Click Add Key
8. DONE

#### Adding SSH public key to GitLab

1. Login to [GitLab](https://about.gitlab.com/)
2. Click on your avatar near the top right of the left-side bar
3. Select "Edit profile"
4. On the left-side bar, select "SSH Keys"
5. Click on the "Add new key" button near the top right
6. Fill in the details:
   - "Key" = the SSH public key
   - "Title" = a label for the new key, ex. "school-sever"
   - "Usage type" = Authentication & Signing (Default)
   - "Expiration date" = the expiration date of your public SSH key on GitLab
     - ex. 2124-11-15 if don't want to set a close expiration date
7. Click "Add key"
8. Done

# 

## Git


After adding SSH public key to your GitHub, it would be convenient for you to clone repositories or push changes to remotes because there is no need to enter username and password repeatedly.

Git has two obvious advantages:

1. **Version Control**: you could record each version of the code and revert to any specific version if necessary.

2. **Collaboration**: you could collaborate with coworker and make changes to the file in parallel.

Here are some basic guides for you:

- `git clone`: clone remote repo onto the current path of local computer
  
  ```
  git clone <repository_url>
  git clone git@github.com:djhshih/setup-linux.git
  ```

- `git add`: keep track of the files you modified in your local computer
  
  ```
  git add <file_name>
  git add README.md
  ```

- `git commit`: stage the file you modified after using `git add` into repository. Remind of adding specific comment that will help us remember what you have done. If you just write `git commit` without `-m`,it will launch an editor and you can write a longer comment
  
  ```
  git commit -m "<comment>"
  git commit -m "Add git tutorial"
  ```

- `git pull`: to ensure you have the most up-to-date version of the file, it is advisable for you to type `git pull` before making any changes when you collaborate with your coworker. If you don't do this, you may encounter conflicts when you push your changes to remote.
  
  ```
  git pull <remote_name> <branch_name>
  git pull origin main
  ```

- `git push`: push the file you modified after using `git commit` to remote
  
  ```
  git push <remote_name> <branch_name>
  git push origin main
  ```

reference: https://rogerdudler.github.io/git-guide/

## Shell configuration 

After you finished previous steps, some configuration on your terminal is recommended. 

#### Copy the default configuration

A version of configuration is avaiable on github. Clone the repository and setup it correctly by run following codes line by line:

```bash
git clone git@github.com:djhshih/dot.git
bash dot/install.sh
echo ". ~/.my.bashrc" >> ~/.bashrc
source ~/.bashrc
```

You will find that the appearance of your shell will be changed. Customized configurations for shell are stored in '$HOME/.my.bashrc'. Other configurations are stored in the home directory. Note that you should **not** delete the 'dot' folder. 

#### Set up conda correctly

After you set up the shell, you also need to set up conda correctly. We should not activate conda environment when we log in as it may conflict with some C++ environments. The idea here is to wrap up a function called `init_conda`. After set up this function, you can activate conda by type `init_conda` directly.

Detailed steps are as follow:

* Run following code to initialize conda. This will change your `~/.bashrc` by generating something start with `# >>> conda initialize >>>` and end with `# <<< conda initialize <<<`
   ```bash
    conda init
   ```

   Note: on `Gemina (ds03)` and  `Geminus (ds02)`, please use following command to locate conda first:
   ```bash
   . /home/conda/bin/activate
   conda init
   ```

* Create another file `~/.init_conda`. Wrap up a function called init_conda as follow: 
```
function init_conda() {
   < paste all contents between `# >>> conda initialize >>>` and `# <<< conda initialize <<<` in ~/.bashrc here >
}
```
  
* Delete all contents between `# >>> conda initialize >>>` and `# <<< conda initialize <<<` in `~/.bashrc`.
* Add following line in `~/.bashrc`
```
source ~/.init_conda
```
* Soure your `~/.bashrc`

When you need to use conda, type `init_conda` and enter it. You will find the `(base)` appeared on the left. This suggested that you have activated conda environment. 

## Tmux

Tmux is useful for organizing multiple tasks and directories in a server. Tmux keeps processes running even when you disconnect from the server, retaining your progress which is useful for many tasks.  

Initiate tmux with `tmux`, assuming your `~/.bashrc` file has set an alias to tmux that points it to a tmux executable. The default keys for PREFIX are Ctrl + B. Using the above tmux config, the PREFIX is `.  

Here are some useful tmux commands:  

* PREFIX + C : Create new window
* PREFIX + X : Delete current pane
* PREFIX + , : Rename current window
* PREFIX + % : Split pane vertically
* PREFIX + " : Split pane horizontally
* PREFIX + ARROWKEYS : Move between split panes based on arrow keys
* PREFIX + P : Move to previous window
* PREFIX + N : Move to next window

When you disconnect from the server and have to reinitialize tmux, use `tmux attach` to attach the previous tmux session.

## Remote server login

### Change password

1. Run `passwd` in the terminal, which will give a password prompt, like the following:

```
Changing password for user X.
Changing password for X.
(current) UNIX password: 
```

2. Enter you current password and click enter, which will give another password prompt, like the following:

```
New password:
```

3. Enter your desired new password and click enter, you will receive another prompt on retyping the new password.  Note that your password should be longer than 10 characters, otherwise you will receiver a message `The password is shorter than 10 characters`
   
   ```
   Retype new password:
   ```

4. Retype your desired new password and click enter

5. You should receive the message `passwd: all authentication tokens updated successfully.`

6. Done

### SSH Copy ID

`ssh-copy-id` will copy the SSH public key into the `~/.ssh/authorized_keys` on the remote host. Once the key has been authorized for SSH, then you can access to the remote host without a password.

1. Ensure you have the SSH key pair. If you do not have a SSH key pair, please refer to "Generate SSH Keys" section above

2. Run `ssh-copy-id <user@host>` in the terminal, then a password prompt will show up like the following:
   
   ```
   user@host's password:
   ```

3. Type in your password that you used to login to the remote host
   
   ```
   user@host's password: <password>
   ```

4. Number of keys in the remote host will show up, indicating that you have successfully added the SSH key, like the following:
   
   ```
   Number of key(s) added: 1 
   ```

5. Done

## Conda environment

When we are using python, the best practice is to make different conda environments for different projects. It will help to reduce potential conflicts between packages and make your project easy to be dispatch.

When you are using tools from others, it will be very common that their tool is also in a python environment. You should follow the instruction given by the author to install them correctly.  

Some other tips are as follow:

* When creating the environment, python version may be important (specified by `python=<version>`). Follow the instructions of authors, or try different versions of python if you experience some trouble

* `pip` or `conda`: both of them can be used the install python packages. A main difference is that `conda` will do a more robust environment check than `pip`. It is preferred *not* to mix `pip` and `conda` in the same python environment (i.e. if the first package is installed via `pip`, then stick to `pip`). For more explanations about the difference between `pip` and `conda`, [check this page](https://www.anaconda.com/blog/understanding-conda-and-pip). 


Note: Following instructions are specific to the GPU server

To activate a Conda environment in the current shell session
```
. /home/conda/bin/activate
conda activate pytorch
```
If the activation is successful, `(base)` will appear in the command line.


To check all the Conda environments that have been created on your server
```
conda info --envs
```

To deactivate a Conda environment and return to the default system environment 
```
conda deactivate
```


## Jupyter lab

### On local computer

If you are running Jupyter lab locally, then you can access jupyter lab
without a SSH tunnel.

On the computer, start jupyter lab, specifying <port> and <ip> as follows
```
jupyter lab --no-browser --port <port> --ip <ip>
```

Then, use the link provided in console output.

### On remote server with SSH tunnel

To do so, follow these steps:

* On **server**:
  * Activate `mamba` or `conda` environment.
  * Navigate to the project directory and start Jupyter by `jupyter lab`.
    Note the url and the port (e.g. 8888).
* On your **local computer**:
  * Start an SSH tunnel: open up a terminal. Type `ssh -L <local_port>:localhost:<server_port> <user>@<server>`. Type in your password or passphrase.
  * Click on the link provided by the server, but replace the server port with
    your local port.

For example, after start Jupyter in the server, you got a link `http://127.0.0.1:8888/?token=xxxx` where `xxxx` represents the token.
For your SSH tunnel, you can replace `<local_port>:localhost:<server_port>` with `1234:localhost:8888`.
Then, in the browser, you would go to `http://127.0.0.1:1234/?token=xxxx`.
Notice that you are accessing port 1234 on your local computer, which will be
directed to port 8888 on the remote server.


## Rstudio server

### without SSH tunnel

Using your browser, access
```
http://<ip>:8787
```
where <ip> is IP address of the server that is running the RStudio server.


## GitHub

### Invite coworker as your collaborator:

1. Navigate to the repository page on GitHub.

2. Click on `Setting` on the top of the repository page.

3. Select `Collaborators` and click on `Add people` tab.

4. Enter the GitHub username or email address of the person you want to invite.

5. Finish invitation once the person accept yours.

### The difference of `git clone` between using HTTPS and SSH:

1. `HTTPS`: when you use HTTPS to clone a remote repository, you need to provide username and password to authenticate yourself.
   
   ```
   git clone https://github.com/djhshih/setup-linux.git
   ```

2. `SSH`: you can use SSH to clone a repository without entering username and password if you associate your local computer with remote GitHub(as mentioned above *Adding SSH public key to GitHub*).
   
   ```
   git clone git@github.com:djhshih/setup-linux.git
   ```

## Local software installation

'patefiant' is a wrapper for common software download without root access. See the [Github repo](https://github.com/djhshih/patefiant) for more information. 

#### Set up 'patefiant' 

To set up `patefiant`, you need to clone the repo and install. 
```bash
# Clone and installation
git clone git@github.com:djhshih/patefiant.git && cd patefiant
./install.sh && . $HOME/.bashrc
```
After your succesful install, `fac` command will be available.

#### Install softwares through 'fac'
To install packages, you can use 'fac install <pkg>'. Avaiable packagese are listed [here](https://github.com/djhshih/patefiant/tree/master/pkg). To install, for example, 'cromwell':

```bash
fac install cromwell
```

For more detailed instructions, please refer to [here](https://github.com/djhshih/setup-linux/blob/main/patefiant.md)


## Setting permissions with 'chmod'

Depending on how the administrators set up the Linux server, read access may be disabled by default for all other users.

Read/write/execute access is controlled for 3 groups: owner, users belonging to the owner's group, and all other users.

To ensure read access and directory access for all users in your group, do the following:
```
chmod -R g+rX $HOME
```
In the above command, the `-R` flag represents recursive and thus applies the change of permissions to all files in the directory and subdirectories.

The `g` on the left hand side of the operator `+` represents `group`, specifying that permissions to be changed are for your group members only.

The operator `+` or `-` specifies whether you are adding permissions or removing permissions from the group specified on the left. In this case, we are adding permissions to our group members to access our files.

The `r` and `X` to the right of the operator represents `read` and `special execute` access. This means read and special execute access are being given to group members.

Lastly, we specify the directory (and subdirectories) in which we want to change permissions, in this case it would be our home directory.

IMPORTANT: After running this command, revert permissions of your SSH private key (e.g. in `$HOME/.ssh/id_ed25519`) back so that only you have read access.
Run the following command to remove read and execute permissions on your private key from your group:
```
chmod go-rX ~/.ssh/id_ed25519
```

You can also set default permissions for all groups by putting the following line of code into your ~/.bashrc:
```
umask 027
```
The first digit sets permissions for the owner, second digit for the group and third digit for others.

`0` gives all access (rw- for files and rwx for directories) to the owner.

`2` gives read access (r-- for files and r-x for directories) to the group.

`7` does not give any access (--- for both files and directories) to others.

## MacOS

MacOS is derived from OpenBSD, which is different Linux. Some MacOS command line tools have similar names as tools in Linux
but they are independently implemented and often have different behaviour.

In the interest of cross-platform compatability, Linux (GNU) command line tools should be preferred over MacOS's native command line tools.

The software `terminal` in MacOS is a commond line tool and can be used to access server.

* Use command+space to search `terminal` and open it
* Use standard commands like `ssh` to access server

#### Mounting remote drives

Do **not** use MacFUSE or sshfs on Mac. The Mac implementation is buggy, creates too many connection requests, and causes instability for the server.
Any software like VSCode that list remote directory structures most likely use MacFUSE and sshfs.

#### Reference
1. https://github.com/osxfuse/osxfuse/issues/45
2. https://github.com/osxfuse/osxfuse/issues/801

Due to the lack of suitable MacFUSE/sshfs alternatives on MacOS, if you want to mount
a remote drive from the Linux server, you should 
1. Use Linux natively or within a virtual environment, or 
2. Use `rsync` to sync specific files.

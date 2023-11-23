# How to setup a newly created Linux account

## Virtual machine
TODO: Jonathan

Here are the steps of setting up Fedora on VirtualBox:

* Download VirtualBox (https://www.virtualbox.org/wiki/Downloads) and Live ISO file for Fedora Workstation (https://fedoraproject.org/workstation/download).
* Open VirtualBox and create a new virtual machine (VM). Choose a custom name for the VM and select the recently-downloaded ISO file.
* Choose base memory, processors and virtual hard disk size you are willing to allocate to the VM (e.g. base memory: 8GB, processors: 8CPU, virtual HDD size: 250GB).  
* Bootup the VM and start Fedora Workstation. Once it boots to desktop, select Install to Hard Drive and choose English (US) for language settings.
* Click on installation destination. Choose the virtual hard disk and custom installation before performing manual partitioning.  
* In the manual partitioning section, select standard partition. Create mount points for /home, /boot, / and biosboot with your desired capacities (e.g. /home: 200GB, /: 20GB, /boot: 0.5GB, biosboot: 1MB).  
* Click Done, Accept Changes and wait for Fedora installation to complete.
* Once complete, turn off the VM and go to Storage settings of the VM to remove ISO file from Controller: IDE.
* Reboot the VM and Fedora will be successfully installed onto the VM.

## SSH key and GitHub/Bitbucket/GitLab
Applies to both local machine and remote server

### Generate SSH keys
reference: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

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

## Git
TODO: Bingqing

```
git clone
git add
git commit
git pull
git push
```

## Bash dot scripts
After you finished previous steps, some configuration on your terminal is recommended. 

#### Copy the default configuration

A version of configuration is avaiable on github. Clone the repository and setup it correctly by run following codes line by line:

```bash
git clone git@github.com:djhshih/dot.git
sh dot/install.sh
echo ". ~/.my.bashrc" >> ~/.bashrc && source ~/.bashrc
```

You will find that the appearance of your shell will be changed. Customized configurations for shell are stored in '$HOME/.my.bashrc'. Other configurations are stored in the home directory. Note that you should **not** delete the 'dot' folder. 

#### Set up conda correctly

After you set up the shell, you also need to set up conda correctly. We should not activate conda environment when we log in as it may conflict with some C++ environments. The idea here is to wrap up a function called `init_conda`. After set up this function, you can activate conda by type `init_conda` directly.

Detailed steps are as follow:
* Run following code to initialize conda. This will change your `.bashrc` by generating something start with `# >>> conda initialize >>>`
```bash
conda init
```

* Define a function called `init_conda` based on the code in `.bashrc`. Store it in file `.init_conda`. This can be done either manually or by the following code:
```bash
# Create .init_conda
new_file_path="$HOME/.init_conda"
touch $new_file_path

# Define the start and end markers for the conda initialization code
start_marker="# >>> conda initialize >>>"
end_marker="# <<< conda initialize <<<"

# Use awk to extract the conda initialization code and write it to the new file
awk -v start="$start_marker" -v end="$end_marker" '
  BEGIN {print "function init_conda() {" > "'"$new_file_path"'";}
  $0 ~ start {flag=1}
  flag {print > "'"$new_file_path"'"}
  $0 ~ end {flag=0; print "}" > "'"$new_file_path"'";}
' ~/.bashrc
```
* Delete the part start with `# >>> conda initialize >>>` in `.bashrc`. This can be done either manully or by the following code:
```bash
awk -v start="$start_marker" -v end="$end_marker" -v new_file="$new_file_path" '
  $0 ~ start {print "source " new_file; flag=1}
  !flag {print}
  $0 ~ end {flag=0}
' ~/.bashrc > ~/.bashrc.tmp
mv ~/.bashrc.tmp ~/.bashrc && source .bashrc
```
When you need to use conda, type `init_conda` and enter it. You will find the `(base)` appeared on the left. This suggested that you have activated conda environment. 

## Tmux
TODO: Jonathan

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

```
passwd
ssh-copy-id # TODO
```

## Conda environment
TODO: Yaofu

Note: The instructions are specific to the GPU server

```
. /home/conda/bin/activate
conda activate pytorch
```

## Jupyter lab on remote server and SSH tunnel

To do so, follow these steps:
* On **server**:
  * Active environment: type `init_conda` to start conda. Type `conda activate <your_target_environment` to activate a conda environment
  * Start Jupyter: type `jupyter lab`. 2 websits will appear. The one with following format `http://<server_port>/?tocken=...` is of interest
* On your **own PC**:
  * Build tunnel: open up a terminal. Type `ssh -L <local_port>:<server_port> <user_name>@<server_name>`. Type in your password. This will leads you to the server
  * Start Jupter:Use the link generated by server, open it in your web browser.

For example, after start Jupyter in the server, you got a link `http://127.0.0.1:8890/?token=xxxx`. When you are building the tunnel, `<local_port>:<server_port>` need to be replace by `8888:127.0.0.1:8890`. Then paste the whole link in web browser and you will get in. Note that you should not close the terminal in your own PC. If you want to open up multiple Jupyter Lab, you need to repeat this process. 

## GitHub
TODO: Bingqing

git clone by HTTPS vs. SSH  
Add collaborators

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
- `id_ed25519` is the private key ~~DO NOT~~ share with anyone
- `id_ed25519.pub` is the public key, which will be added to GitHub/Bitbucket/GitLab

### Adding SSH keys to GitHub/Bitbucket/GitLab
#### Copy SSH public key
We will need to first copy the SSH public key.

The SSH public key locates in the SSH directory (i.e., `~/.ssh/`)

Steps to copy SSH public key
1. Enter the SSH directory -  `cd ~/.ssh/`
2. Open the file that stores your public key - `vim ./id_ed25519.pub`
3. Copy the content (i.e., SSH public key) to your clipboard

#### GitHub
Steps to add SSH keys to GitHub:

1. Login to [GitHub](https://github.com/)
2. Click on your icon on the top right
3. Click "Settings"
4. Click "SSH and GPG keys", which locates on the left side-bar under the "Access" section
5. Click "New SSH key" near the top right
6. Fill in the blanks:
    - "Title": a label for the new key, ex. "school-sever"
    - "Key type": would be "Authentication Key" (default)
    - "Key": the SSH public key
7. Click "Add SSH Key"
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
TODO: Wenhao

`github.com/djhshih/dot`

Applies to both local machine and remote server

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
TODO: Noel

```
passwd
ssh-copy-id
```

## Conda environment
TODO: Yaofu

Note: The instructions are specific to the GPU server

```
. /home/conda/bin/activate
conda activate pytorch
```

## Jupyter lab on remote server and SSH tunnel
TODO: Wenhao

```
ssh -L
```

## GitHub
TODO: Bingqing

git clone by HTTPS vs. SSH  
Add collaborators

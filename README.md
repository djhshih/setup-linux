# How to setup a newly created Linux account

## Virtual machine
TODO: Jonathan

Download VirtualBox and Live Iso file for a Linux distribution (e.g. Fedora Workstation).  
Open VirtualBox and create a new virtual machine (VM). Choose a custom name for the VM and select the recently-downloaded ISO file. Choose base memory, processors and virtual hard disk size you are willing to allocate to the VM (e.g. base memory: 8GB, processors: 8CPU, virtual HDD size: 250GB).  
Bootup the VM and start Fedora Workstation. Once it boots to desktop, select Install to Hard Drive. Select English (US) language and click on installation destination. Choose the virtual hard disk and custom installation before performing manual partitioning.  
In the manual partitioning section, select standard partition. Create mount points for /home, /boot, / and biosboot with your desired capacities (e.g. /home: 200GB, /: 20GB, /boot: 0.5GB, biosboot: 1MB).  
Click Done, Accept Changes and wait for Fedora installation to complete. Once complete, turn off the VM and go to Storage settings of the VM to remove ISO file from Controller: IDE.

## SSH key and GitHub/Bitbucket/GitLab
Applies to both local machine and remote server


reference: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

We will generate the ssh key through the terminal, at the end, you will have two ssh keys: private ssh key and public ssh key.

1. open terminal
2. run `ssh-keygen -t ed25519 -C "your_email@example.com"

There will be a prompt on where to save the files, like the following:
```
Generating public/private ed25519 key pair.
Enter file in which to save the key (some_path/.ssh/id_ed25519):
```

Simply press Enter to store the files in the default file location.


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

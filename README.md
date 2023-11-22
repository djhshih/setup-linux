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
TODO: Noel

Applies to both local machine and remote server

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

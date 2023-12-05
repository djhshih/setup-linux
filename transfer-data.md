# File transfer between servers trough `rsync`

`rsync` have several advantages over other files trasfer method (either by `scp` command or `Filezilla`):
* Allow backup: if your transfer accidentally shut down, just type the same command again and the transfer will reload
* More information are kept, including ownership, group and permission
* Efficient and reproducible
* ...

Use server `ds02` and `ds03` as example, you need to following these 2 steps:
## 1. (Generate) and send key between servers
This step estaiblish links between two servers through ssh key. After generate the key correctly (see [setup linux](https://github.com/djhshih/setup-linux/blob/main/README.md)), you need to send the ssh key to the target server. This step needs to be done in **both server**. Under our example: 
* On `ds02`:
```bash
# Run on ds02
ssh-copy-id <username>@<ds03_address>
```
* On `ds03`:
```bash
# Run on ds02
ssh-copy-id <username>@<ds02_address>
```

## Step 2. File transfer
Suppose we want to transfer a file in `ds02` called `dummy.txt` to a target location `ds03`, two different ways are avaiable: **push** and **pull**

* Push: operate in `ds02` and "send" the file `dummy.txt` to `ds03`
* Pull: operate in `ds03` and "get" the file `dummy.txt` from `ds02`

Cauton: some servers may disable pushing, but most servers would allow pulling

### Via push:
Push can be acheived by following command on **`ds02`**
```bash
# Run on ds02
rsync <path_to_dummy.txt> <username>@<ds03_address>:<path_to_put_dummy.txt>
```

### Via pull:
Push can be acheived by following command on **`ds03`**
```bash
# Run on ds03
rsync <username>@<ds02_address> <path_to_put_dummy.txt> 
```
Caution: some servers may disable pushing, but most servers would allow pulling


## Tips:

### Args:
Some common args are recommended (case sensitive). Typically we use `-avuzn` to test the trasfer and `-avuz` to do the job:
* `-n` or `--dry_run`: for testing
* `-a` or `--archive`: archive mode, short cut of  `rlptgoD`.
  * `-r`: Recursive for directories
  * `-l`: Keep symlinks
  * `-p`: Preserve permissions
  * `-t`: Preserve modification times
  * `-g`: Preserve group
  * `-o`: Preserve owner (super-user only).
  * `-D`: Preserve device files (super-user only) and special files
* `-v` or `--verbose`: increase verbosity, which gives you more information. 
* `-u` or `--update`: skip files that are newer on the receiver
* `-z` or `--compress`: compress file data during the transfer

### Config file:
You can create a config file under `~/.ssh` directory to further shorten your code. For example, in `ds2`, you can write:
```txt
Host ds03
    HostName <ds03_address>
    User <username>
```
Pushing files to dummy.txt `ds03` will be writen as:
```bash
# Run on ds02
rsync -avun <path_to_dummy.txt> ds03:<path_to_put_dummy.txt>
```




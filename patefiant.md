# patefiant
Recall that "patefiant" is a wrapper that allows users to download common softwares without root access. We will be showing how to use patefiant and create a new patefiant installation script below. Please refer to the [patefiant github repository](https://github.com/djhshih/patefiant) for futher information.

## Install patefiant
Please refer to the `Local software installation` section in README.md.
After sucessfully installing `patefiant`, you should be able to use the command `fac` to install packages.

## Using patefiant
You can find available packages in `pkg` directory.
ex. `cmake`, `nix`, `tmux`


To install these packages, simply run:
```
fac install <package_name>
# ex. fac install cmake
```

If there is a package that you wish to download but it is not available in `pkg`, you may create a new patefiant installation script, which is describe in below section.


## Create a new patefiant installation script
We will be using the software `dlazy` as an example. Please refer to [dlazy github repository](https://github.com/djhshih/dlazy) for further information.

1. Move into the `pkg` directory
    - ex. `cd ./patefiant/pkg/`
2. Create a new directory with the package name (not recommended: other random names)
    - ex. `mkdir dlazy`
3. Create an installation script.
    - the script should be a bash script named `install.sh` for consistency
    - the script should  install the software (i.e., `curl`, `gunzip`, ...etc)

Following is an example patefiant installation script to install `dlazy`, which can be used as a template
```
#!/bin/bash
set -e

# Script for installing dlazy which can execute a directory of jobs easily

name="dlazy"
version=""
target_dir=$PATEFIANT_ROOT

tmp_dir=$(mktemp -d) && cd $tmp_dir && echo $tmp_dir

# install dlazy
git clone git@github.com:djhshih/dlazy.git && cd ./dlazy/

make install DESTDIR=${target_dir}
export PATH+=:${target_dir}/bin
```

4. Save the script and change the access permissions to make it executable:
```
chmod +x install.sh
```

5. Done. And now you can install `dlazy`/your package with `fac install <package_name>` as descirbe in above section.

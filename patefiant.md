# patefiant
Recall that "patefiant" is a wrapper that allows users to download common softwares without root access. We will be showing how to use patefiant and create a new patefiant installation script below. Please refer to the [patefiant github repository](https://github.com/djhshih/patefiant) for futher information.

## Install patefiant
Please refer to the `Local software installation` section in README.md.
After sucessfully installing `patefiant`, you should be able to use the command `fac` to install packages.

## Using patefiant


## Create a new patefiant installation script
We will be using the software `dlazy` as an example. Please refer to [dlazy github repository](https://github.com/djhshih/dlazy) for further information.

1. Move into the `pkg` directory
    - ex. `cd ./patefiant/pkg/`
2. Create a new directory with the package name (not recommended: other random names)
    - ex. `mkdir dlazy`
3. Create an installation script.
    - the script should be a bash script named `install.sh` for consistency
    - the script should include codes that install the software (i.e., `curl`, `gunzip`, ...etc)

Following is an example script, which can be used as a template
```

```


# CPU server

HostName dshihlab.sbms.hku.hk

A central `micromamba` is installed in `/home/micromamba`.

Note: `micromamba` is a faster `conda` alternative.

Setup your `micromamba` shell environment by:
```
. /home/mamba/setup.sh
```

By default, no environment is activated, so you will need to
```
micromamba activate base
```
or replace `base` with another environment.

Then, you can install packages by
```
micromamba install
```


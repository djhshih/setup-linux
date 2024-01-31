# GPU server

HostName: `gpu02.sbms.hku.hk`

Access the server by `ssh`.

A central conda is installed in `/home/conda`.

Ensure that you are using the following `conda`:

```
$ which conda
/home/conda/bin/conda
```

The `pytorch` and `tensorflow` packages are already installed:

```
$ conda env list
base                  *  /home/conda
pytorch                  /home/conda/envs/pytorch
tensorflow               /home/conda/envs/tensorflow
```

To use `pytorch`, you need to activate the environment
```
$ conda activate pytorch
```

To see GPU usage, do

```
nvidia-smi
```

As you can see from the output above, this server has 8x NVIDIA RTX 3090 GPU cards.
You should try to select GPU cards that are unused.

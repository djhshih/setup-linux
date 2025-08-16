# GPU server

## Usage

Access the server by `ssh` from within the HKU network:
```
$ ssh gpu02.sbms.hku.hk
```

A central conda is installed at `/home/conda`.

Initialize your shell environment by
```
$ . /home/conda/bin/activate
```

Environments providing `pytorch` and `tensorflow` are available
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

To create new conda environments, see [conda docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

To see the current GPU usage, do
```
nvidia-smi
```

As you can see from the output above, this server has 8x NVIDIA RTX 3090 GPU cards.
You should try to select GPU cards that are unused. Refer to the documentation of `pytorch` or `tensorflow` on how
to select GPU cards.

## Rules

This GPU server is intended for interactive use, so please avoid batch processing with 2+ cards.
[HKU HPC](https://hpc.hku.hk/) has GPU servers for batch processing.

This server is shared resource among multiple users. Please be considerate to other users.
Some software tools use *all* CPU threads by default. Be sure to configure these tools properly so that you
are *not* using all CPU threads! (See **CPU limit** below.)

Users who contribute significantly to GPU server crashes will be banned from server use for a period of 2 days 
following the first offense. Each offense thereafter doubles the ban period.


## Techniques

### Resource monitoring tools

- GPU: `nvidia-smi`
- CPU & memory: `htop`

### CPU limit

You should understand the behaviour and resource usage of code that you are running and configure
the multithread usage properly. If your code uses all threads and you cannot figure it how to configure
thread usage, you can use `taskset` to limit CPU usage.

CPU usage can be limited for a `python` process to threads 0 to 3 using `taskset` by
```
taskset -c 0-3 nice -n 10 python
```

In `python`, you can verify that the CPU limit has been applied by 
```{python}
>>> import os
>>> print(len(os.sched_getaffinity(0)))
4
```

# Terminal Multiplexer (TMUX)?

## Why do we need tmux?
1. Persisten Sessions:  
   * When network connection drops or disconnected from remote server, the processes running inside a tmux session (e.g, bioinformatic pipelines, installations, R sessions etc.) will continue running.
2. Multitasking and Organization:  
   * Tmux allows to run multiple panes...
3. Lightweight Alternative to GUI Tools:  
   * Don't need to use Rstudio server anymore (cannot change conda/mamba environment easily without `sudo`
   root permission). * Tmux consumes fewer resources compared to GUI-based IDEs.

## How to setup tmux?
1. Assume tmux is already [installed](https://github.com/tmux/tmux/wiki/Installing) on your device.
2. The tmux configuration file `.tmux.conf` is already inside in [dot repo](https://github.com/djhshih/dot)
   you have git cloned. When you run `bash dot/install.sh`, a symbolic link to `.tmux.conf` will be created
   into user's home directory.
4. Once linked, tmux will automatically use this `.tmux.conf` file to apply its settings for keybindings,
   pane navigation shortcuts...
   (NOTE: the leader/prefix key is set to "`" by this config)
   (NOTE: the new terminal/pane created will be at the same directory)

## How to use tmux for daily practice?
1. `tmux new -s {session_name}`
2. `tmux ls` or `tmux list-sessions`
3. `tmux attach -t {session_name}`
4. `prefix + %`: open a new pane vertically
5. `prefix + "`: open a new pane horizontally
6. `prefix + arrowkeys`: navigate amoung panes on screen
7. `prefix + x`: kill pane
8. `prefix + d`: detach session (still alive)
9. `prefix + q`: check pane numbers
10. `prefix + [`: enter copy mode, can scrow up for previous results
11. `prefix + ]`: paste the copied contents

## Important Notes
1. Different tmux sessions or panes are independent. For example,
   * need to initiate conda/mamba and activate needed environment again.

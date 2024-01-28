# Use vim plugin `vim-slime`

A handy vim plugin called [vim-slime](https://github.com/jpalardy/vim-slime) will be very helpful if you wish to run your code line by line in `tmux` environment.

## Plugin install:

* Create a `.vimrc` file in your home directory `~`. 
* Copy all contents in [this file](https://github.com/djhshih/dot/blob/main/.vimrc) into `~/.vimrc`, save the `~/.vimrc` (Note: currently a typo on line 17, should be `g:slime_no_mappings`)
* Re-open `~/.vimrc`, type `:PlugInstall`, the install process will start.
* After the install process finished, close all windows

## Plugin useage:

This plugin can be used in a similar way as `tmux` (i.e. `vim-slime-leader + command key`). Default vim-slime-leader is whitespace defined in the `~/.vimrc`. 

Suppose we want to run `R` code line by line under default setting of this plugin defined in `~/.vimrc`:

* Open a tmux session, split your window to different panel 
* Check the panel number by `tmux-leader + q`.
* Use vim to open you R code in panel 0 and open R terminal in panel 1.
* By default, `vim-slime` will move your code from panel 0 to 1 and run it. **In visual mode**, move the cursor in vim to the line you want to run, press `whitespace + d`, the line where cursor is on will be executed in the R console in panel 1.
* The default behaviour of `vim-slime` is to execute code in panel 1. If you want to change the target panel (say you opened your R console in panel 3), first press `whitespace + v` in your vim, you will see a prompt `tmux socket name or absolute path: default`. Press enter, you will see another prompt `tmux target pane:`. Type in `:.<your-target-penel>` (**NB: `:.` cannot be ignored**. In our example, you should type `:.3`) and press enter again. The the code can be moved correctly to panel 3

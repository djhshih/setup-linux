# Use vim plugin `vim-slime`

A handy vim plugin called [vim-slime](https://github.com/jpalardy/vim-slime) will be very helpful if you wish to run your code line by line in `tmux` environment.

## Plugin install:

* Create a `.vimrc` file in your home directory `~`. 
* Copy all contents in [this file](https://github.com/djhshih/dot/blob/main/.vimrc) into `~/.vimrc`, save the `~/.vimrc`
* If you only want to install vim-slime, you can omit the lines between `call plug#begin()` and `call plug#end()` which include other plugins and modify it as below:
```
call plug#begin()
Plug 'jpalardy/vim-slime'
call plug#end()
```
* Re-open `~/.vimrc`, type `:PlugInstall`, the install process will start.
* After the install process finished, close all windows

NOTE: vim-slime may not work with older versions of vim (e.g. version 7.4). 

## Plugin useage:

This plugin can be used in a similar way as `tmux` (i.e. `vim-slime-leader + command key`). Default vim-slime-leader is 'whitespace' defined in the `~/.vimrc`. 

Suppose we want to run `R` code line by line under default setting of this plugin defined in `~/.vimrc`:

* Open a tmux session and split your window by using `tmux-leader + %` to split vertically or `tmux-leader + "` to split horizontally.
* You can navigate between panes by using `tmux-leader + ARROW KEYS`.
* Check the panel number by `tmux-leader + q`.
* Use vim to open your R code in panel 0. Move to the other pane and open R terminal in panel 1.
* By default, `vim-slime` will move your code from panel 0 to 1 and run it. **In visual mode**, move the cursor in vim to the line you want to run, press `whitespace + d`, the line where cursor is on will be executed in the R console in panel 1. You can also highlight multiple lines and execute them with `whitespace + d` using `Shift + v` to enter visual line mode, where you can select multiple lines by moving the cursor up or down.
* Press `whitespace + b` on the vim code to execute a block of code, separated by empty lines, in the R console. Note that function definitions with empty lines will not be fully executed with this command as the empty lines will separate the function code into multiple blocks.
* Press `whitespace + c` on the vim code to execute cells of code, separated by "---", in the R console. In the R script, you can type "#---" between lines of code to execute them separately with this command.
* The default behaviour of `vim-slime` is to execute code in panel 1. If you want to change the target panel (say you opened your R console in panel 3), first press `whitespace + v` in your vim, you will see a prompt `tmux socket name or absolute path: default`. Press enter, you will see another prompt `tmux target pane:`. Type in `:.<your-target-penel>` (**NB: `:.` cannot be ignored**. In our example, you should type `:.3`) and press enter again. The the code can be moved correctly to panel 3

# Tmux

On command-line:
* `tmux a -t [name]` Open a session
* `tmux ls` List available sessions

On session:
* `C-z $` Rename session
* `C-z d` Detach session

Windows

* `S-[left]` Select the next window
* `S-[right]` Select the previous window
* `C-[left]` Move window to left
* `C-[right]` Move window to right
* `C-z c` Open new window
* `C-z x` Close current window
* `C-z C-z`  Open last window
* `C-z :swap-window -t -1` Move current window to left
* `C-z ,` Rename window
* `C-z n` Next window
* `C-z p` Previous window

Status Bar

* `C-z b` Toggle status bar

Other

* `C-z :source-file ~/.tmux.conf` Reload config

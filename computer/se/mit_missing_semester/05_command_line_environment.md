# MIT Missing Semester 分析笔记

## 5 Command-line Environment

- Pausing and backgrounding process
  - `SIGSTOP`: pauses a process
  - `SIGTSTP` (`Ctrl-Z`): the terminal's version of `SIGSTOP`
  - `jobs` lists the unfinished jobs associated with the current terminal session.
  - `Ctrl-Z` followed by `bg`: background an already running program.
    - Note that backgrounded processes are still children processes of your terminal and will die if you close the terminal
    - this will send yet another signal, `SIGHUP`.
  - `kill -l` list all signals

- Terminal Multiplexers
  - all keybindings have the form `<C-b> x` where that means
    - (1) press Ctrl+b,
    - (2) release Ctrl+b,
    - (3) press x.
  - Sessions - a session is an independent workspace with one or more windows
    - `tmux` starts a new session.
    - `tmux new -s NAME` starts it with that name.
    - `tmux ls` lists the current sessions
    - Within tmux typing `<C-b> d` detaches the current session
    - `tmux a` attaches the last session. You can use `-t` flag to specify which
  - Windows - Equivalent to tabs in editors or browsers, they are visually separate parts of the same session
    - `<C-b> c` Creates a new window. To close it you can just terminate the shells doing <C-d>
    - `<C-b> N` Go to the N th window. Note they are numbered
    - `<C-b> p` Goes to the previous window
    - `<C-b> n` Goes to the next window
    - `<C-b> ,` Rename the current window
    - `<C-b> w` List current windows
  - Panes - Like vim splits, panes let you have multiple shells in the same visual display.
    - `<C-b> "` Split the current pane horizontally
    - `<C-b> %` Split the current pane vertically
    - `<C-b> <direction>` Move to the pane in the specified direction. Direction here means arrow keys.
    - `<C-b> z` Toggle zoom for the current pane
    - `<C-b> <space>` Cycle through pane arrangements.

- [SSH Port Forwarding][1]

  [1]: https://unix.stackexchange.com/questions/115897/whats-ssh-port-forwarding-and-whats-the-difference-between-ssh-local-and-remot

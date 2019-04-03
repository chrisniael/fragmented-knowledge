# tmux

## 命令

new-session [-c start-directory] [-s session-name]

attach-session [-t target-session]

kill-server

kill-session [-t target-session]

list-sessions

list-commands

rename-session [-t target-session] new-name

source-file [-q] path


## 快捷键

C-b : default prefix key


#### Session


#### Window
0 to 9      Select windows 0 to 9.

#### Pane

"           split the current pane into two, top and bottom.
%           Split the current pane into two, left and right.
q           Briefly display pane indexes.
C-Up, C-Down
C-Left, C-Right
            Resize the current pane in steps of one cell.
M-Up, M-Down
M-Left, M-Down
            Resize the current pane in steps of five cell.

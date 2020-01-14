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
s           显示 session 列表


#### Window
w           显示 window 列表
0 to 9      Select windows 0 to 9.
l           上一个 window

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
M-o         rotate pane
C-o         rotate pane
o           切换到下一个 pane
z           最大化当前 pane


#### 其他

d           detach
t           big clock
?           list shortcut
:           prompt

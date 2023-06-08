### ThinkPad T14

```shell
root@CD-DZ0104843:/home/hanbabang/1_software/cmake-3.26.4-linux-x86_64/bin# cat ~/.bashrc
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
[ -z "$PS1" ] && return

# don't put duplicate lines in the history. See bash(1) for more options
# ... or force ignoredups and ignorespace
HISTCONTROL=ignoredups:ignorespace

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "$debian_chroot" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
        # We have color support; assume it's compliant with Ecma-48
        # (ISO/IEC-6429). (Lack of such support is extremely rare, and such
        # a case would tend to support setf rather than setaf.)
        color_prompt=yes
    else
        color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
#if [ -f /etc/bash_completion ] && ! shopt -oq posix; then
#    . /etc/bash_completion
#fi

# hanbabang
alias adb='/mnt/d/Adb/platform-tools_r31.0.3-windows/platform-tools/adb.exe'
alias perf='/root/bin/perf'
source ~/.vimrc

alias ga='git add'
alias gc='git commit'
alias gr='git reset'
alias gb='git branch'
alias gl='git log'
alias gs='git status'
alias gd='git diff'
alias gp='git cherry-pick'
alias go='git checkout'
alias re='reset'

alias lvim='/root/.local/bin/lvim'

# Android NDK
export PATH=$PATH:/home/hanbabang/1_software/ndk/21.4.7075529
export ANDROID_NDK_HOME=/home/hanbabang/1_software/ndk/21.4.7075529

# CMake
export PATH=$PATH:/home/hanbabang/1_software/cmake-3.26.4-linux-x86_64/bin

# export PATH=$PATH:/home/mysoftware/nodejs/node-v16.15.0-linux-x64/bin
# export PATH=$PATH:/mnt/d/Adb/platform-tools_r31.0.3-windows/platform-tools
# export PATH=$PATH:/home/hanbabang/mysoftware/adb/platform-tools
# export ADB_SERVER_SOCKET=tcp:172.17.64.1:5037
# 目前感觉好像不需要配置Python3的环境变量，先不配置试试
# export PATH=$PATH:/usr/local/python3/bin
# export PATH=$PATH:/root/bin

# set auto-completion of git
if [ -f "/usr/share/bash-completion/completions/git" ]; then
    source "/usr/share/bash-completion/completions/git"
fi

# samba start
# sudo service smbd start

# X11 for opengl
echo "DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}')"
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0
# export DISPLAY=:172.18.0.1:0 # win的ipv4地址，公司VPN的ipv4地址
# export DISPLAY=:0.0
# export DISPLAY=:127.0.0.1:0.0
# export MESA_GL_VERSION_OVERRIDE=4.5 # 目前不配置好像也没有问题
# unset LIBGL_ALWAYS_INDIRECT # 目前不配置好像也没有问题

echo "root source success!"

# set wsl 中文输入法
LANG=zh_CN.UTF-8
export INPUT_METHOD=fcitx # wayland输入法
export XMODIFIERS=@im=fcitx # x11输入法
export GTK_IM_MODULE=fcitx # gtk输入法

# aarch64-linux gcc g++
export PATH=$PATH:/home/hanbabang/1_software/toolchain_v3_linaro_aarch64_6_3_1_archive/bin/

# cmake 3.25
# export PATH=$PATH:/home/hanbabang/1_software/cmake-3.25.0-rc1-linux-x86_64/bin/

# nvm npm nodejs
nvm use v14.21.3

. "$HOME/.cargo/env"

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```


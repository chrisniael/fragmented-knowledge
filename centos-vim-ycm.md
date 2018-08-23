# CentOS 7 安装 YouCompleteMe

CentOS 7.5.1804

## 安装依赖组建

```bash
yum install -y epel-release
yum install -y gcc gcc-c++ cmake3 ruby ruby-devel lua lua-devel ctags git \
    python python-devel tcl-devel ncurses-devel perl perl-devel \
    perl-ExtUtils-ParseXS perl-ExtUtils-CBuilder perl-ExtUtils-Embed
ln -s /bin/cmake3 /bin/cmake
```

## 安装 Vim 8.1.0320

```bash
wget https://github.com/vim/vim/archive/v8.1.0320.tar.gz
tar xvf v8.1.0320.tar.gz
cd vim-8.1.0320
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib64/python2.7/config \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-cscope \
            --prefix=/usr/local
make
make install
```

## 安装 YouCompleteMe

```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

配置 `~/.vimrc`，内容如下

```vim
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'Valloric/YouCompleteMe'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

下载 YouCompleteMe

```bash
vim +PluginInstall +qa
```

## 编译 YouCompleteMe (支持 C/C++)

```bash
cd ~/.vim/bundle/YouCompleteMe/
./install.py --clang-completer
```

## 配置 YouCompleteMe

编辑 ~/.vimrc，增加以下内容

```vim
let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'
let g:ycm_seed_identifiers_with_syntax=1    " 语法关键字补全
set completeopt=longest,menu
```

`~/.ycm_extra_conf` 文件可以从 YouCompleteMe 中拷贝一份

```bash
wget -O ~/.ycm_extra_conf https://raw.githubusercontent.com/Valloric/ycmd/master/examples/.ycm_extra_conf.py
```

## 配合 CMake 使用

```bash
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON .
```

执行后会生成文件 `compile_commands.json`，确保此文件在项目的根目录下。

或者还可以在 `CMakeLists.txt` 中添加

```cmake
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
```

这样 YouCompleteMe 就可以根据 `compile_commands.json` 文件来做语法提示，语法分析了。

## 参考

[CentOS7.2安装Vim8和YouCompleteMe (cnblogs.com/nidey)](https://www.cnblogs.com/nidey/p/8657016.html)
[YouCompleteMe (github.com/Valloric/YouCompleteMe)](https://github.com/Valloric/YouCompleteMe)
[vundle (github.com/vundlevim/vundle)](https://github.com/vundlevim/vundle.vim)
[vim-cpp-enhanced-highlight (github.com/octol/vim-cpp-enhanced-highlight)](https://github.com/octol/vim-cpp-enhanced-highlight)

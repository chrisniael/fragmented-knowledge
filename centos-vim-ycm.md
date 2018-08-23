# CentOS 7 安装 YouCompleteMe

CentOS 7.5.1804

## 安装依赖组建

```bash
yum install -y gcc gcc-c++ ruby ruby-devel lua lua-devel  \
    ctags git python python-devel \
    tcl-devel ncurses-devel \
    perl perl-devel perl-ExtUtils-ParseXS \
    perl-ExtUtils-CBuilder \
    perl-ExtUtils-Embed
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

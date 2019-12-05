# coc.nvim 配置

## vim-plug

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

```vim
" Specify a directory for plugins
" - For Neovim: stdpath('data') . '/plugged'
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')


" Initialize plugin system
call plug#end()
```


## coc.nvim


#### 依赖

* neovim >= 0.3.1
* vim >= 8.0.1453
* nodejs >= 8.10.0

```bash
pacman -S nodejs
```

#### 使用 vim-plug 安装 coc.nvim


```vim
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

```bash
vim +PlugInstall +qa
```

#### coc.nvim 配置

参考官方仓库推荐配置


## lsp

#### C++

clangd

```bash
pacman -S llvm
```

```json
{
  "languageserver": {
    "clangd": {
      "enable": true,
      "command": "clangd",
      "filetypes": [
        "c",
      "cpp",
      "objc",
      "objcpp"
      ],
      "rootPatterns": [
        "compile_commands.json",
      ".vim/",
      ".git/",
      ".hg/"
      ],
      "args": [
        "-background-index"
      ]
    }
  }
}
```

## neovim 兼容 vim

```bash
ln -s ~/.vim .config/nvim
ln -s ~/.vimrc .config/nvim/init.vim
```

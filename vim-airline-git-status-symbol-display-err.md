# Vim airline git status symbol 显示错误

Unicode : U+0246

## 测试终端是否支持显示

```bash
printf '\u0246\n'
```

#### Windows

XShell，PuTTY 不支持

MinTTY 支持

#### Mac

iTerm 支持

## 解决方案

替换成其他字符

```vim
if !exists('g:airline_symbols')
  let g:airline_symbols = {}
endif
let g:airline_symbols.notexists = '∄'

```

## 参考

* https://github.com/vim-airline/vim-airline/issues/1729
* https://github.com/vim-airline/vim-airline/issues/1374

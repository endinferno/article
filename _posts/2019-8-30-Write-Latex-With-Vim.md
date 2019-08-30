---
layout: post
title: Write LaTex With Vim/NeoVim And Auto Preview On MacOS
---

## 首先安装Mactex

## 在Vim/NeoVim配置文件中添加两个插件

插件vimtex

插件vim-latex-live-preview

## Setting

```vimrc
autocmd Filetype tex setl updatetime=1000
let g:livepreview_previewer = 'open -a TeXShop'
let g:tex_flavor = 'latex'

"let g:livepreview_previewer = 'evince'
"let g:livepreview_previewer = 'open -a Preview'
"这后面两个的优劣在网上其他的地方也有很详细说明
```

## MacTex配置

TeXShop->Preference

源代码->启动时->勾选"配置为外部编辑器"

预览->外部编辑器->勾选"自动更新预览"

每次预览后focus都会改变，所以在shell中运行defaults write TeXShop BringPdfFrontOnAutomaticUpdate NO

this will disable the focus-stealing behavior and leave the window in the background so that it doesn't disrupt continuous editing.

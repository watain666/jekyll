---
layout: post
title: "[Ubuntu] vim sync system's clipboard"
image: images/unsplash-image-1.jpg
date: 2017-08-03
excerpt: ""
tag:
- Ubuntu 16.04
- Tips
- OS
- Vim
- Clipboard
---

如何將Vim和系統的剪貼簿同步？碰到這個問題好多次了

這次終於好好處理這個問題了，就順便做個筆記吧！

> 測試環境
>
> OS：Ubuntu 16.04 LTS
>
> Editor：VIM - Vi IMproved 7.4

1. `$ vim --version | grep clipboard`查看vim是否支持clipboard功能

2. 如果`+clipboard`則跳過這一步;

如果顯示的是`-clipboard`說明不支援此功能，需要安裝vim-gtk

`$ sudo apt install vim-gtk`，

因為默認安裝的vim有些功能不支持，

安裝`vim-gtk`包可以`get the extra features`

3. 使用`+`暫存器與系統粘貼板互通數據，`"+yy`等操作

參數資料: [How to make vim paste from (and copy to) system's clipboard?](https://stackoverflow.com/questions/11489428/how-to-make-vim-paste-from-and-copy-to-systems-clipboard)

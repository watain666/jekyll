---
layout: post
title: "[PHP] PHPBrew Note"
image: images/
date: 2018-08-29
excerpt: "PHPBrew "
tag:
- PHP
- PHPBrew
- Note
- Tips
- Ubuntu 18.04
---

目錄
* toc
{:toc}

---

因為公司的測試機上的 PHP 版本為5.4.x

為了在本機可以重現公司測試機的環境，避免掉一些錯誤

在網路上找了很多部屬多個版本的 PHP 的方法，

最後決定使用現代一點的工具來做這件事，使用 [c9s大神](https://github.com/c9s) 所開發的 [PHPBrew](https://github.com/phpbrew/phpbrew) 來解決多版本控制的問題

PHPBrew 除了可以安裝多個版本的 PHP ，並且做切換以外

還可以讓 PHPer 像 Node.js/Python 開發者一樣使用 npm/pip

來安裝開發所需要用到的套件，裝 xdebug 一行指令就搞定了不需要在照著手冊一步一步來啦，免得還會碰到和我一樣[預料外的狀況要排除](https://watain666.github.io/Ubuntu-16.04-installing-Xdebug-for-PHP7/)

執行

`phpbrew install 7.2.9 +default`

輸出

`configure: error: Cannot find OpenSSL's libraries`


2. 安裝 5.4.45 版時碰到的問題

`phpbrew install 5.4.45 +default`

`configure: error: Please reinstall the libcurl distribution -    easy.h should be in <curl-dir>/include/curl/`

reference :

* [使用PHPBrew管理PHP版本](https://medium.com/%E6%8A%80%E8%A1%93%E5%AE%85%E5%A0%B1/%E4%BD%BF%E7%94%A8phpbrew%E7%AE%A1%E7%90%86php%E7%89%88%E6%9C%AC-4a7d3c845690)

* [PHPBrew：編譯 PHP 的各種踩雷紀錄](http://goodjack.blogspot.com/2018/06/phpbrew-php.html)

* [configure: error: Cannot find OpenSSL's libraries](http://blog.51cto.com/linuxzj/1632132)

* [unable to install php. 5.3.29 getting error](https://github.com/phpbrew/phpbrew/issues/826#issuecomment-334173596)









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

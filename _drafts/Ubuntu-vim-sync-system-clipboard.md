---
layout: post
title: "[Ubuntu] vim sync system's clipboard"
image: images/Ubuntu-vim-sync-system-clipboard/vim.png
date: 2017-08-03
excerpt: ""
tag:
- Ubuntu 16.04
- Tips
- OS
- Vim
- Clipboard
---

目錄
* toc
{:toc}

---

如何將 vim 和系統的剪貼簿同步？

平常沒在使用 vim 開發，但是透過 CLI 修改檔案的時候常常會碰到這個問題

平常都是繞路走過去假裝沒這件事，這次終於願意好好處理這個問題了，就順便做個筆記吧！

> 測試環境
>
> OS：Ubuntu 16.04 LTS
>
> Editor：VIM - Vi IMproved 7.4

1. `vim --version | grep clipboard` 確認 vim 是否支援 `clipboard` 功能

2. 如果顯示 `+clipboard` 則跳過這一步

    但如果顯示的是 `-clipboard` 代表不支援此功能，

    需要安裝 `vim-gtk` 才能讓 vim 和系統的剪貼簿同步

    `sudo apt install vim-gtk`

3. 使用 `"` Registers 來和系統剪貼簿同步數據

    選取好你要的部份後使用 `"+y` 就可以將選取的資料存到 `"+` Registers 並且同步到系統剪貼簿

4. 修改 `.vimrc`

    但是每次都要 `"+y` 豈不是煩死人？ 這個時候就要來修改 `.vimrc`

    `vim ~/.vimrc`

    在任意位置加入 `set clipboard=unnamedplus`

    存檔後，你的 `y`, `d`, `x`, `p` 就能夠和系統層的 `Ctrl+c` / `Ctrl+v` 一起用啦！


reference :

* [How to make vim paste from (and copy to) system's clipboard?](https://stackoverflow.com/questions/11489428/how-to-make-vim-paste-from-and-copy-to-systems-clipboard)

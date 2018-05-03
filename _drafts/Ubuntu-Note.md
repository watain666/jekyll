---
layout: post
title: "[Ubuntu] Note"
image: images/.jpg
date: 2018-04-10
excerpt: "Miscellaneous note"
tag:
- Ubuntu
- Note
- Tips
---

目錄
* toc
{:toc}

CompizConfig
Unity Tweak Tool

### Guake show desktop disappears issue
Open `Compiz Config Settings Manager` and uncheck the option at `General > General Options > Hide Skip Taskbar Windows`
This solved this issue for me, even without using the hide on focus loss option of guake.

### 計算目錄有多少檔案
`find DIR_NAME -type f | wc -l`

### root權限開檔案總管
sudo nautilus

ls -1
請注意 ls 後加上的是數字 1 ，只顯示檔名，且每行顯示一個。

wc -l 檔案
請注意 wc 後加上的是小寫 l ，會輸出檔案中有多少行數。

兩個指令結合
ls -1 | wc -l
所得的數字就是目前路徑下的檔案數量(含子資料夾、連結)。

ls -l | grep -v ^l | wc -l
請注意 ls 後加上的是小寫 l ，所得數字就是目前路徑下的檔案數量(含子資料夾)。

ls -la | grep ^- | wc -l
請注意 ls 後加上的是小寫 l ，所得數字就是目前路徑下的檔案數量(含隱藏檔)。

### 安裝字型
mv PowerlineSymbols.otf ~/.fonts/

### 更新字型快取
fc-cache -vf ~/.local/share/fonts/

### 查詢有沒有這個字形
fc-list | grep "Source Code Pro"

### 只更新Chrome
sudo apt-get --only-upgrade install google-chrome-stable

### 重新下載Chrome公鑰匙
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

### Gnome初始啟動程式
gnome-session-properties

### 乾淨移除
sudo apt-get remove --auto-remove --purge google-chrome-stable
sudo apt-get purge google-chrome-stable
sudo apt-get autoremove

### 使用composer安裝
composer global require fabpot/php-cs-fixer
composer global require friendsofphp/php-cs-fixer

### 使用composer移除
composer global remove fabpot/php-cs-fixer
composer global remove friendsofphp/php-cs-fixer

### scp下載遠端檔案
scp -P 22 -r rex.liu@172.16.1.41:/data/sites/***/ /***/
scp -P 22 -r rex.liu@172.16.1.41:/data/sites/puppets/ /opt/lampp/htdocs
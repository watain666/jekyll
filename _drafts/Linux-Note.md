---
layout: post
title: "[Linux] Note"
image: images/Linux-Note/CliFit.jpeg
date: 2018-04-08
excerpt: ""
tag:
- Linux
- Ubuntu
- Note
- Tips
---

目錄
* toc
{:toc}

---

### Setting Tool

CompizConfig
Unity Tweak Tool

---

### Guake show desktop disappears issue

Open `Compiz Config Settings Manager` and uncheck the option at `General > General Options > Hide Skip Taskbar Windows`
This solved this issue for me, even without using the hide on focus loss option of guake.

---

### chmod改變權限

`chmod [mode] FILE_NAME`

其中m o d e是一個8進位數。

在絕對模式中，許可權部分有著不同的含義。

每一個許可權位用一個8進位數來代表

>0 4 0 0 文件屬主可讀
>
>0 2 0 0 文件屬主可寫
>
>0 1 0 0 檔屬主可執行


>0 0 4 0 屬組用戶可讀
>
>0 0 2 0 屬組用戶可寫
>
>0 0 1 0 屬組用戶可執行


>0 0 0 4 其他用戶可讀
>
>0 0 0 2 其他用戶可寫
>
>0 0 0 1 其他用戶可執行

在設定許可權的時候，只需按照上面查出與檔屬主、屬組用戶和其他用戶所具有的許可權相對應的數字，並把它們加起來，就是相應的許可權表示。

可以看出，檔屬主、屬組用戶和其他用戶分別所能夠具有的最大許可權值就是7。

再來看看前面舉的例子：

代碼:

-rwxr–r–  1   root            0 10月 19 20:16 temp



相應的許可權是：

代碼:

rwx-：0400 + 0200 +0100 (檔屬主可讀、寫、執行) = 0 7 0 0

r–：0 0 4 0 (屬組用戶可讀) = 0 0 4 0

r–：0 0 4 0 (屬組用戶可讀) = 0 0 4 0

0 7 4 4



有一個計算八進制許可權表示的更好辦法，如下：

文件屬主：r w x：4 + 2 + 1

屬組用戶：r w x：4 + 2 + 1

其他用戶：r w x：4 + 2 + 1



這上面這相，更容易地計算出相應的許可權值，只要分別針對檔屬主、屬組用戶和其他用戶把相應許可權下面的數位加在一起就可以了。

temp檔具有這樣的許可權：

代碼:

r w x     r – – r – –

4+2+1  4     4



把相應許可權位所對應的值加在一起，就是7 4 4。

如：

代碼:

chmod 666 rw- rw- rw- 賦予所有用戶讀和寫的許可權

chmod 644 rw- r– r- – 賦予所有檔屬主讀和寫的許可權，所有其他用戶讀許可權

chmod 744 rwx r– r- – 賦予檔屬主讀、寫和執行的許可權，所有其他用戶讀的許可權

chmod 664 rw- rw- r- – 賦予文件屬主和屬組用戶讀和寫的許可權，其他用戶讀許可權

chmod 700 rwx — — 賦予檔屬主讀、寫和執行的許可權

chmod 444 r– r– r- – 賦予所有用戶讀許可權

http://linux.vbird.org/linux_basic/0210filepermission.php#chmod


> 3770意思是
>`$ sudo chmod 3770 /AlphaTeam`
>　　　　　　　3>SGID + Sticky bit
>　　　　　　　   　　$2^1　+　2^0　　$
>SGID(Set group ID)
>具有sticky bit屬性的該"目錄"下的檔案，其檔案/目錄只有owner/root才有權力刪除
>若不為目錄設置sticky bit，任何具有該目錄寫和執行權限的用戶都可以刪除和移動其中的文件。
>
>$SGID=2^1=2$ 產生的檔案目錄與上一層的檔案相同名稱
>+
>$Sticky bit=3=2^0=1$ 別人無法刪我的東西
>∥ 上面2行解出來的2+1就等於3700的3
>$3$
>$7 = owner$
>$0 = group$
>$0 = other$
>SGID詳細可參考鳥哥：[SetUID, SetGID, Sticky bit 與 file 指令](http://linux.vbird.org/linux_basic/0220filemanager/0220filemanager.php#suid_sgid_sticky)

>要加上setfacl(不讓別人改自己的檔案)
>setfacl(Set File System Access Control List)
>　　　　　　　　　　　　　　↗r–(-號等於戴面具遮掉原本的權限)
>`$ setfacl -m "default:mask::r--" /AlphaTeam/`
>　　　　　　↘modify　　↘不想看的地方遮掉
>setfacl詳細可參考鳥哥：[setfacl 指令用法介紹及最簡單的『 u:帳號:權限 』設定](http://linux.vbird.org/linux_basic/0410accountmanager.php)

---

### root權限開檔案總管

`sudo nautilus`

---

### 計算目錄有多少檔案

`find DIR_NAME -type f | wc -l`

`ls -1`
請注意 ls 後加上的是數字 1 ，只顯示檔名，且每行顯示一個。

`wc -l FILE_NAME`
請注意 wc 後加上的是小寫 l ，會輸出檔案中有多少行數。

兩個指令結合
`ls -1 | wc -l`
所得的數字就是目前路徑下的檔案數量(含子資料夾、連結)。

`ls -l | grep -v ^l | wc -l`
請注意 ls 後加上的是小寫 l ，所得數字就是目前路徑下的檔案數量(含子資料夾)。

`ls -la | grep ^- | wc -l`
請注意 ls 後加上的是小寫 l ，所得數字就是目前路徑下的檔案數量(含隱藏檔)。

---

### 安裝字型

`mv PowerlineSymbols.otf ~/.fonts/`

---

### 更新字型快取

`fc-cache -vf ~/.local/share/fonts/`

---

### 查詢有沒有安裝這個字形

`fc-list | grep "Source Code Pro"`

---

### 只更新Chrome

`sudo apt-get --only-upgrade install google-chrome-stable`

---

### 重新下載Chrome公鑰

`wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -`

---

### Gnome初始啟動程式

`gnome-session-properties`

---

### 乾淨移除

`sudo apt-get remove --auto-remove --purge PROGRAM_NAME`

or

`sudo apt purge --auto-remove PROGRAM_NAME`

### 僅移除無用的安裝包

`sudo apt-get autoremove`

---

### 使用 composer 全域安裝

`composer global require friendsofphp/php-cs-fixer`

### 使用 composer 全域移除

`composer global remove friendsofphp/php-cs-fixer`

---

### scp下載遠端檔案

`scp -P 22 -r USER_NAME@IP_OR_URL:/DIR_NAME/ /TARGET_DIR_NAME/`

### 支援 exFAT(FAT64) 檔案系統

`sudo apt-get install exfat-utils exfat-fuse`
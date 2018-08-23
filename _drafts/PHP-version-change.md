---
layout: post
title: "[PHP] Installing two versions of php with xampp on Ubuntu 16.04"
<!-- image: images/.png -->
date: 2018-05-18
excerpt: "Using XAMPP 7.2.5 on Ubuntu 16.04"
tag:
- Ubuntu 16.04
- Xdebug
- PHP
- XAMPP
- LAMPP
- PhpStorm
---

目錄
* toc
{:toc}

---

以前在學校學Java的時候，老師讓我們使用eclipse這款IDE來開發，並一再強調使用IDE的debug功能和看errorMsg有多重要，除此之外，一直以來寫我寫code都是用Sublime / Atom這種輕量級的editor來開發，並沒有深入的去研究IDE。

最近發現PhpStorm這款IDE的公司JetBrains有[學生免費方案](https://www.jetbrains.com/student/)(而且是所有產品)，我就想說可以趁這個機會來試試看看IDE，便馬上申請並下載了PhpStorm。

才想說終於可以開始學習使用IDE了，結果要安裝xdebug就一直撞牆...
不管我怎麼改就是會出現這個錯誤訊息。
```bash=
Xdebug requires Zend Engine API version 320160303.
The Zend Engine API version 320151012 which is installed, is newer.
```

浪費了一堆時間，最後發現只是因為我的電腦裡有不同版本的PHP...
因此整理一篇筆記，看能不能幫到需要幫忙的人，像是未來的我。

### 開始安裝

>測試環境
>
>OS：Ubuntu 16.04 LTS
>
>PHP開發環境：XAMPP 7.1.1

### 1. 匯出你的php info到家目錄
`$ php -i > ~/php-info.txt`

>如果沒辦法匯出就加上`sudo`試試看

### 2. 使用Xdebug Wizard
打開剛才產生的php-info.txt，將內容複製到[Xdebug Wizard](https://xdebug.org/wizard.php)並點選Analyse my phpinfo() output按鈕
>Xdebug Wizard這個工具可以解析你的PHP版本、Zend API版本諸如此類安裝所需要的資訊。

### 3. 取得說明
你會得到這樣的說明

> 1. Download [xdebug-2.5.3.tgz](http://xdebug.org/files/xdebug-2.5.3.tgz)
> 2. Unpack the downloaded file with `tar -xvzf xdebug-2.5.3.tgz`
> 3. Run: `cd xdebug-2.5.3`
> 4. Run: `phpize` (See the FAQ if you don't have phpize.
>
>    As part of its output it should show:
 ```bash
 Configuring for:
 ...
 Zend Module Api No:      20160303
 Zend Extension Api No:   320160303
 ```
>
> If it does not, you are using the wrong phpize. Please follow this [FAQ entry](http://xdebug.org/docs/faq#custom-phpize) and skip the next step.
>
> 1. Run: `./configure`
> 2. Run: `make`
> 3. Run: `cp modules/xdebug.so /opt/lampp/lib/php/extensions/no-debug-non-zts-20160303`
> 4. Edit `/opt/lampp/etc/php.ini` and add the line
```bash
zend_extension = /opt/lampp/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so
```

### 4. 不要完全照著Xdebug Wizard的說明做

先照著Xdebug Wizard說明1~3步，然後停一下

1. 下載Xdebug

2. 解壓縮

3. `$ cd xdebug-2.5.3`進入解壓縮後的資料夾內。

再來這步就很重要了，我會一直裝不起來就是死在這
首先要確認你執行phpize是不是在你要佈署的環境

4. 執行phpize

`$ which phpize`

>回傳結果
>```bash
>/usr/bin/phpize
>```

這意味著我輸入`phpize`的時候是執行`/usr/bin/phpize`的phpize

但是我要佈署的是xampp的phpize才對呀！

那xampp的phpize在哪呢？

如果你不知道xampp的phpize在哪裡可以問問whereis

`$ whereis phpize`

>回傳結果
>```bash
>phpize:
>/usr/bin/phpize
>/usr/bin/phpize7.0
>/opt/lampp/bin/phpize
>```

回傳的結果顯示我的系統內有3個phpize，我要使用的是最下面的xampp的phpize

接著就可以開始說明的第4步了，只不過要把`phpize`換成`/opt/lampp/bin/phpize`

> <span style="color:red">注意！以你的路徑為主，我的路徑可能和你的不一樣</span>

`$ /opt/lampp/bin/phpize`

>回傳結果
>```
>Configuring for:
>PHP Api Version:         20160303
>Zend Module Api No:      20160303
>Zend Extension Api No:   320160303
>```

5. configure它並帶上php-config路徑

如果你不知道php-config路徑一樣使用`whereis php-config`

>回傳結果
>```bash
>php-config:
>/usr/bin/php-config
>/usr/bin/php-config7.0
>/opt/lampp/bin/php-config
>```

一樣我要使用的是xampp的php-config

`$ sudo ./configure --enable-xdebug --with-php-config=/opt/lampp/bin/php-config`

結果太長就不附上了

6. 產生文件

`$ make`

7. 將產生好的文件複製到你要放xdebug.so的目錄

`$ cp modules/xdebug.so /opt/lampp/lib/php/extensions/no-debug-non-zts-20160303`

8. 修改php.ini加入這行就安裝完成了。

```bash
[xdebug]
zend_extension = /opt/lampp/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so
```

>如果你不知道php.ini在哪裡...知道怎麼做了吧？

9. 再來只要把Apache Server重開再去看看你的phpinfo()或`$ php -v`驗收

`$ sudo service apache2 restart`

`$ php -v`

>回傳結果
>```bash
>PHP 7.1.1 (cli) (built: Feb  1 2017 01:39:46) ( NTS )
>Copyright (c) 1997-2017 The PHP Group
>Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
>    with Xdebug v2.5.3, Copyright (c) 2002-2017, by Derick Rethans
>```

有看到`with Xdebug v2.5.3, Copyright (c) 2002-2017, by Derick Rethans`就代表成功了。

參考文件
* [現在PHP版本那麼多，編譯出屬於自己的xdebug才是王道](http://blog.crazyphper.com/?p=3477)
---
layout: post
title: "[Linux] Moving efficiently in the CLI"
image: images/.jpg
date: 2018-04-10
excerpt: "Remove useless items"
tag:
- Ubuntu 16.04
- Tips
- OS
- Nautilus
---

目錄
* toc
{:toc}

---

![Nautilus](../images/Ubuntu-remove-items-from-Nautilus-sildbar/Nautilus1.png)

Ubuntu沒辦法直接刪除用不到的預設書籤？

因為Ubuntu這些書籤是由`~/.config/user-dirs.dirs`來控制的，

直接用editor開啟並用#註解掉你不需要的書籤。

> 測試環境
>
> OS：Ubuntu 16.04 LTS
>
> GNOME nautilus 3.14.3

e.g. 我不需要圖片就改

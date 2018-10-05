---
layout: post
title: "[Applications] Best Git Client GitKraken"
image: images/Best-Git-Client-GitKraken/gitkraken-vs-cli.jpg
date: 2018-10-05
excerpt: ""
tag:
- Applications
- GitKraken
- Git
- Ubuntu 18.04
---

目錄
* toc
{:toc}

---

![](/images/Best-Git-Client-GitKraken/gk-merge-edit.gif)

今天要來介紹一款功能強大又美觀的 Git Client 叫 [GitKraken](https://www.gitkraken.com/)

是說其實我近幾年挑選軟體的原則很簡單，漂亮/開源/跨平台

以上 3 樣有中 2 樣我就會想裝來用用看了

而且 GitKraken 的功能遠比你所想像的強大(有多強大就自己摸索啦XD)

簡單來說就是只要按幾下精美的圖形界面就能輕鬆完成許多繁瑣的指令

而其實 GitKraken 在安裝和使用上沒什麼難度

主要在使用上碰到一個小問題才促使我來寫這篇文章的

接下來就進入正題吧

---

### 安裝

>測試環境
>
>OS：Ubuntu 18.04 LTS
>
>GitKraken：4.0.5

這邊要特別提醒一下

因為 [Ubuntu security policy](https://wiki.ubuntu.com/SecurityTeam/Policies#Execute-Permission_Bit_Required) 的關係

從 Ubuntu Software / Snap 安裝的 GitKraken 是沒有權限開啟 root 所擁有的資料夾的

Apache2 放檔案的資料夾 `/var/www` 是沒辦法用 GitKraken Open Repo 的

**所以不要從 Ubuntu Software / Snap 安裝 GitKraken**

乖乖到 [GitKraken](https://www.gitkraken.com/download) 的下載頁面載來安裝

或是開 Terminal 下這兩行指令就安裝完啦

```
wget https://release.gitkraken.com/linux/gitkraken-amd64.deb
sudo dpkg -i ~/gitkraken-amd.deb
```

---

reference :

* [I can't navigate owned directories on root](https://github.com/mmtrt/gitkraken/issues/4)

* [ubuntu gitkraken unable to access var](https://stackoverflow.com/questions/49378270/ubuntu-gitkraken-unable-to-access-var)

* [Permission of a .desktop file](https://askubuntu.com/questions/419610/permission-of-a-desktop-file)

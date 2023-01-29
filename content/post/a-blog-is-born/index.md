---
title: "A Blog is Born: 一個部落格的誕生"
description: 本文紀錄我在 GitHub Pages 上利用 Jekyll 架設部落格的歷程。
date: 2020-02-20
slug: 
image: blog.jpg
categories:
    - blogging
    - coding
tags:
    - notes
    - jekyll
---

## 緣起
---
這個部落格誕生於 2020 年 2 月，在我碩士一年級的寒假。原本不覺得自己有辦法做出一個部落格，一方面缺乏實作經驗，另一方面我並不擅長寫文章。然而在寒假的某天，當我一如往常打開電腦點進 YouTube 時，看到了這部[**<u>影片</u>**](https://www.youtube.com/watch?v=U0idtvxVo9I)。它清楚的步驟介紹讓我有了「我也可以做到！」的錯覺。為什麼說是錯覺呢？因為接下來實作的過程中可說是困難重重，我費了一番心力才完成網頁架設及整理。當我對製作部落格還存有顧慮時，意外地讀到了 GitHub 創辦人之一 Tom Preston-Werner 所寫的[**<u>文章</u>**](https://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)。內容實在太感人又有說服力了！因此加強了實作部落格的動機。

熟悉了製作 GitHub Pages 的流程後，我另外建立了 [**<u>Homepage</u>**](https://andreashih.github.io/)，並將部落格連結到 Homepage 上。架設網站的主要目的是記錄自己在研究所期間所累積的成果，並留下曾經努力過的足跡。

以下的步驟說明我如何網路上開闢一片疆土。筆者使用之電腦為 Windows 系統，故將以在 Windows 上的做法為例。若內容有任何需要修改的地方，歡迎在文章下方留言，或[**<u>寫信</u>**](mailto:r08142004@ntu.edu.tw)告訴我。

&nbsp;

## Preparation
---
### 1. GitHub 帳號
在開始之前，必須先[**<u>創一個 GitHub 帳號</u>**](https://github.com/)。

### 2. 檢查電腦中是否已載有 Ruby
可以先在 command line 上輸入 `ruby -v` 檢查電腦中是否已經載有 Ruby。如果沒有，請跳到步驟 3。若電腦中已有 Ruby，將會回傳它的版本號碼。

接著，輸入 `gem -v` 檢查 RubyGems。如果很幸運地兩個 command 都成功了，請輸入 `sudo gem install jekyll` 開始安裝 Jekyll。

最後，輸入 `jekyll -v` 檢查 Jekyll 是否安裝成功。

[*<u>資料來源</u>*](https://onextrapixel.com/start-jekyll-blog-github-pages-free/)

### 3. 下載 Ruby
請前往 [**<u>RubyInstaller</u>**](https://rubyinstaller.org/downloads/)，並點選 **Ruby+Devkit 2.6.5-1 (x64)** 開始下載。（我第一次下載了 **Ruby+Devkit 2.7.0-1 (x64)** ，但後來版本不相容無法運作）。

執行下載時 RubyInstaller 會打開一個 command prompt，安裝時請遵照 default options，如此一來就會成功了。

最後，請輸入 `ridk install` 以完成最後一個步驟。

### 4. 安裝 Jekyll
請打開一個新的 command prompt，並輸入`gem install jekyll bundler`。接著，輸入 `jekyll -v` 檢查是否安裝成功。

如果電腦上有 [**<u>Windows Subsystem for Linux</u>**](https://docs.microsoft.com/en-us/windows/wsl/about?redirectedfrom=MSDN)，請參考 [**Jekyll on Windows**](https://jekyllrb.com/docs/installation/windows/#installation-via-bash-on-windows-10) 裡詳細的安裝步驟。

Windows 電腦特別會有 Timezone 的問題，[**<u>Jekyll on Windows</u>**](https://jekyllrb.com/docs/installation/windows/#time-zone-management) 也提供了解決辦法。

&nbsp;

## Get Your Hands Dirty
---
接下來的步驟是參考這部[**<u>影片</u>**](https://www.youtube.com/watch?v=U0idtvxVo9I)撰寫而成。

&nbsp;

### 1. Jekyll Themes
到 [**<u>Jekyll Themes</u>**](http://jekyllthemes.org/) 上挑選一個喜歡的模板。點進縮圖後可以點選 **Demo** 進行預覽。

決定模版之後，點選 **Homepage**，進入模板的 repo (repository)。以下將以本部落格的模板 [**<u>Lagrange</u>**](https://github.com/LeNPaul/Lagrange) 為例進行說明。

&nbsp;

### 2. Repository Settings

進入模板的 repo 後，請點選右側的 **Fork**，將模板複製到自己的 repo。此時畫面中，repo 的名字會變成 **你的帳號/Lagrange**。

接著要更改 4 個設定。

(1) 將左方的 **Branch** 設為 **Master**。如果下拉式選單中沒有這個選項，在搜尋欄位中打 "Master" 就可以搜尋到了。

(2) 在右方 **Settings** 中點選左側的 **Branches**，將 **Default branch** 設定為 **Master**。請記得點選 **Update** 以完成變更。

(3) 在 **Settings** 中點選左方的 **Options**，將 **Repository name** 設定為**你的帳號.github.io**。也可以設定別的名字，但最後 GitHub Page 的網址會長得不一樣，可以改改看。

(4) 滑到頁面下方，看到 **GitHub Pages** 的欄位後停下來，把 **Source** 改成 **master branch**。上方的網址就是新建立的部落格的網址，如果點進去顯示 404，可能要稍後片刻（我曾經等過 20 分鐘）。

&nbsp;

### 3. GitHub Desktop

安裝 [**<u>GitHub Desktop</u>**](https://desktop.github.com/) 並完成設定。

回到自己的 repo，點選右側綠色的 **Clone or download**，再點選 **Open in Desktop**，repo 中的內容就會下載到自己的電腦上新增一個資料夾。同時 **GitHub Desktop** 中左上角的 **Current Repository** 會顯示自己的 repo 名稱。在電腦上對資料夾中檔案進行的修改會顯示在 **GitHub Desktop** 上。

&nbsp;

### 4. Local Installation

在 command prompt 中 cd 到資料夾，再輸入 `bundle install`。接著，輸入 `bundle exec jekyll serve`，就可以在瀏覽器上輸入 `localhost:4000` 進行預覽。（有時須依照 command prompt 出現的提示加新指令到資料夾裡的 `Gemfile` 中。）

我的 Windows 電腦曾遇過數次 `TZInfo::DataSourceNotFound` 錯誤訊息。此時只要在 `Gemfile` 中新增 `gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw]`，就可以成功運作。

&nbsp;

## Personalize Your Blog
---

接著依照 repo 中 `README.md` 的說明修改各檔案成自己的內容。我使用的編輯器是 [**<u>Visual Studio Code</u>**](https://code.visualstudio.com/)。介面右方可以開啟 markdown preview，覺得很方便！在編輯過程中，與其直接刪除不需要執行的 lines ，在它們前面加上 `#` 對我來說是比較保險的做法。

修改完並儲存後，重新整理 `localhost:4000`，就可以看到更新的內容。根據我的經驗，`_config.yml` 需花費較長時間更新。

回到 **GitHub Desktop**，輸入 **Summary** 後，點選左下角 **Commit to master**，再點選右上角的 **Fetch origin**，就可以將更新的檔案上傳到 GitHub 中的 repo，以更新正式的網頁。

&nbsp;

## And That's It!
---
接下來就可以開開心心地用 [**<u>Markdown</u>**](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet) 撰寫內文了！如果要預覽 blog，可以依照 `4. Local Installation` 的方法執行，但不需要再 run 一次 `bundle install`。

上述過程讓我感受最深的是，你必須試了才知道結果會如何。不知道怎麼做就試一下，再依結果去調整。不斷地找到問題，再不斷地解決問題，我認為這就是學習新事物困難但有趣的地方。

&nbsp;

<span>Photo by <a href="https://unsplash.com/@jessbaileydesigns?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Jess Bailey</a> on <a href="https://unsplash.com/s/photos/blog?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
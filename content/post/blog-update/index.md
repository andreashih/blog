---
title: 部落格的小更新：Tag Page, RSS, CSS...
description: 調色調上癮了，應該可以發現頁面上多了一些顏色。
date: 2021-05-03
slug: 
image: table.jpg
categories:
    - blogging
    - coding
tags:
    - notes
    - jekyll
---

```
*2022/01/29 更新*

調色調上癮了，應該可以發現頁面上多了一些顏色。整理了 menu bar，把多餘的資訊拿掉，加一個 home 按鈕可以回到主頁。另外，為了版面乾淨，把 posts 和 tags 兩頁中的文章標題底線拿掉了。

*2021/09/06 更新*

把 read time 和它的 icon 都拿掉了，因為現在的計算方式是英文的 token，我找不到怎麼改算中文的。blog 首頁的預覽 truncate 也減成 250 字。原本是 350，對於中文來說有點太長了。
```

&nbsp;

今天~~因為不想寫計算語言學作業~~更新了 blog 的 [**<u>tag page</u>**](https://andreashih.github.io/blog/menu/tags.html)，還有打開 [**<u>RSS</u>**](https://andreashih.github.io/blog/rss-feed.xml)，在此做些紀錄。

## Tag Page
---
隨著文章越來越多，分類就更顯重要。我用的這個 jekyll 模板本來就可以在各篇文章加入 tags，但是沒有一個獨立的 tag page，所以打算自己幫它加一個。我參考的是[**<u>這篇文章</u>**](https://nk910216.github.io/2017/08/11/UsingTagsForJekyll/)的 code，只改了 css 讓按鈕變成我喜歡的顏色，顏色是在 [**<u>NIPPON COLORS</u>**](https://nipponcolors.com/) 挑的。

原本在本機一切順利，但是 push 上去卻發現我的 tags 按鈕不能顯示顏色。後來找到[**<u>解決方法</u>**](https://stackoverflow.com/questions/49743535/jekyll-static-page-css-not-rendering)才終於成功！

## RSS Feed
---
其實我一直都知道這個模板可以用 RSS feed，但就是沒有把它打開，因為不知道可以幹嘛XD

直到最近才發現 RSS 其實蠻好用的。[**<u>RSS</u>**](https://zh.wikipedia.org/wiki/RSS) 的全名是 Really Simple Syndication，可以讓你訂閱喜歡的 blog、podcast，甚至是 YouTube 頻道。當訂閱的網站有更新，就可以獲得通知。再也不用一個一個加到我的最愛，最後因為懶得點開看有沒有更新而遺忘他們的存在。

> **要怎麼開始呢？**

很多 blog 的頁面上都找得到 RSS 的 icon (長得很像 wifi 圖示)，點進去之後會出現一堆亂七八糟的文字，請不要害怕，複製最上方的網址就對了。如果沒有 RSS 圖示的話，在頁面上按右鍵再點選 View page source 通常也找得到，只是要 ctrl+F 搜一下 RSS 網址在哪裡。

> **連結複製好了，然後呢？**

現在有許多管理 RSS 的平台，最多人使用的應該屬 [**<u>Feedly</u>**](https://feedly.com/)，直接將 RSS feed 複製貼上即可，但免費版有資料夾數量限制。Mac 用戶推薦使用 [**<u>Vienna</u>**](https://www.vienna-rss.com/)，介面簡潔好用，資料夾數量沒有限制。

&nbsp;

以上就是這次的小更新，也歡迎大家用 RSS 訂閱這個 blog！

Photo by <a href="https://unsplash.com/@krisatomic?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kris Atomic</a> on <a href="https://unsplash.com/s/photos/cafe?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
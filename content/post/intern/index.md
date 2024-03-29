---
title: 台達電子實習心得 - 後端工程師 (Backend Engineer)
description: 結束了越級打怪的暑期實習，一瞥日曆居然已經到了九月。
date: 2021-09-04
slug: 
image: computer.jpg
categories:
    - working
tags:
    - intern
---

結束了越級打怪的暑期實習，一瞥日曆居然已經到了九月。整個熾熱的暑假都泡在資料海裡，鍵盤和秒針滴滴答答把時間送走。實習這兩個月，雖然因為資質駑鈍過程有點辛苦，但現在回想起來還是一段很充實的學習過程。

&nbsp;

## 如何找實習

懷著對未來的不安，我一心想著要找實習確定畢業後的方向。但是關於要找哪一種實習工作，卻沒有篤定的想法。正好去年參加了 ROCLING 研討會，就把手冊上所有贊助公司名字 key 到 104 搜尋實習職缺，才發現台達的暑期實習計畫。因為非本科系，程式能力也非頂尖，原本只是抱著試試看的心情投履歷，後來會進到後端面試甚至拿到 offer 完全是我始料未及的 (還記得面試時主管問會不會寫 Java，知不知道 python 底層架構，我都說不會...)

&nbsp;

## 工作內容

主要的工作項目是 data migration。簡而言之，就是把資料從舊的資料庫搬到新資料庫。為了實現這個過程，在兩個月內認識了許多新工具：

1. **mongoDB**: 舊系統使用的 database
1. **PostgreSQL**: 新系統使用的 database
1. **Apache Nifi**: 原本要使用它來做 migration，但最後採用 python
1. **Redis**: 存放在記憶體 (而非硬碟中) 的資料庫，主要使用到它的 bitmap

在實習一開始，mentor 教導了關聯式資料庫與資料庫正規化的概念 (歡迎參考我的[**<u>筆記</u>**](https://docs.google.com/document/d/1j1lkrHKfbvHMRdb3o663HYAehCeUufgYA4i5_Q7QMuU/edit?usp=sharing))。這些名詞對我來說十分陌生，花了不少時間查資料，並且做中學不斷犯錯後才漸漸理解。由於對資料庫的理解很粗淺，只會幾個基本的 SQL query，突然要處理 mongoDB 資料還要一邊注意複雜的關聯，對我來說簡直難如登天。真的要感謝 mentor 和同事耐心解惑，透過螢幕分享手把手教會我許多指令，才能在一次次的撞牆期中慢慢撞出一些成果。

> 我的工作流程大致如下：

1. 與主管討論舊表和新表的欄位關聯
1. 在舊表 (mongoDB) 中寫 aggregation，取出需要的欄位
1. 如果舊表與新表資料型態不同，會先在 mongoDB 裡面轉換 (例如 `ObjectId` 轉字串/`int` 轉字串/字串轉 `date` 等等)
1. 必要的話會在 python 裡面處理資料或新增欄位
1. 在 python 裡面將 mongoDB 的舊表塞到 postgreSQL 的新表裡

資料搬遷的過程常常會遇到髒資料，而關聯式資料庫牽一髮而動全身的特性不容許髒資料的污染。一遇到 duplicate key value，馬上 error 給你看。這時候需要土法煉鋼找出重複的資料，然後跟主管確認是否移除。常常還沒搬資料，光是清資料就已經花上一整天。有時候覺得明明已經清乾淨了，卻還搬不過去，或是開心的搬過去了，但是關聯沒寫好資料有一半都不見！這種時候整個很洩氣。但很神奇的是，往往吃完午餐或隔天上班就會找到問題了。

&nbsp;

## 實習和學校的不同

以往學程式時並不會處理到太複雜的資料，在這次實習也驗證了真實資料可能產生的各種問題，例如髒資料、target 和 source DB 的資料型態不符等等。由於實習期間寫的程式不只有自己看，還會交給其他同事使用，所以也更注意該如何寫得容易維護。

在寫程式或是分析問題時，我常常落入見樹不見林的思考謬誤中，殊不知掌握複雜系統必須適時從脈絡中離開，直接「抓重點」觀察事物的本質。這讓我想到語言的複雜系統...頭又昏了@@

&nbsp;

## 如何解決問題

最快的方式就是請教 mentor，但是 mentor 常常需要開會並不是隨時有空，如果評估可以自己解決，我就會先查資料試試看。最重要的就是拆解問題，也就是了解問題背後的問題。例如，我一直搞不懂 redis 的 `SETBIT` function，就必須先去了解 `bit`。不知道資料怎麼搬，就先搬一筆試試看。一步一步往前，在問題中找到問題，接著求助 google 通常都會找到解法。~~真的找不到就是資料本身的問題啦。~~

&nbsp;

## 最大挑戰

在實習的尾聲，我碰上一個很難的問題。在舊表裡面，有一個「影片觀看紀錄」的欄位，每一筆資料都是一個像 `[1,1,1,1,0,0,1,1,0,0]` 的 array，其中每一個 1 代表影片播放了 5 秒。看起來很合理，但有一個很嚴重的問題。總共有 30 多萬筆資料，也就是 30 多萬個 array，而且每個 array 都比剛剛的例子長好幾倍，整個非常龐大。Mentor 希望我將觀看紀錄透過 redis 轉成 `bitmap`，用 `gzip` 壓縮後，再用 `base64` encoding。聽完講解我只有一頭霧水。必須很慚愧地承認，我根本連 `bit` 是什麼都不大了解。雪上加霜的是，因為我配到的電腦容量不足，沒辦法裝 redis GUI 介面，所以一切只能在 command line 進行，而 command line 印出的結果是十六進制 (hex) 的樣子，不是熟悉的二進制 (binary)。所以我就硬著頭皮學了幾個 redis 指令，再把結果貼到計算機裡面驗證 (此時我才知道 windows 裡面的計算機有 programmer 模式)。剛好同事幫我找到在 python 裡面使用 redis function 的方法，第一階段終於成功把 array 轉成 `bitmap`。

當我信心滿滿地 demo 給同事看時，同事問：「那你要不要跑全部資料看看？」我頓時寒毛直豎。對啊！剛才用的是前幾筆資料，我還沒跑過全部 30 多萬筆資料...但也只能硬著頭皮給他跑了下去。

然後就卡住了。

透過螢幕分享，感覺時間過得特別的慢。我忍不住打破沉默：「呃...好像有點慢，可能是我哪裡寫錯了...」

同事幫我檢查程式後，發現 mongoDB aggregation 跟 `SETBIT` 的地方都花了很多時間。aggregation 的部分卡在 `$lookup`，這部分我把資料拿出來，用 python 處理倒是蠻快就解決了。重頭戲在 `SETBIT`。

同事：「不然你不要透過 redis，直接寫個 python function 轉 `bitmap` 吧」

這意味著我必須完全了解 redis `SETBIT` function 裡面在做什麼，再思考怎麼用 python 做出一樣的效果...光想就頭皮發麻。接下來就開始連續好幾天的瘋狂研究。所有能找的資料，能看的影片都被我翻了出來。最後，我用了有點複雜的方式做出了類似的結果，但是 array 後面多餘的好幾個 0 (表示沒看完影片) 卻不知道如何處理。我苦著臉打電話問同事，同事看了我的 code 之後說：「你被 `SETBIT` 的概念綁住了。」然後給了一個我從沒想過的簡單提議。

登時茅塞頓開。

接下來寫得無比順暢，程式馬上少了好幾行，順利趕在實習的最後一天寫好了。本來要跑超過兩小時的 migration 程式，現在只需不到兩分鐘，終於放下了心裡一顆大石頭。

&nbsp;

## Work from home

Work from home 的小確幸就是 8:30 上班可以 8:00 再起床，悠悠哉哉地開電腦。壞處就是沒有看到 mentor 本人，會有不知道工作做得如何的不安感。想一直回報進度又怕對方正在忙其他事情。後來終於回到辦公室，雖然大家都是各忙各的，但有人在旁邊真的會比較有動力。

{{< figure src="desk.jpg" title="我的辦公桌 (雖然只進公司兩天)、識別證和證書" width="60%" height="auto">}}

&nbsp;

## 自我反省

雖然實習期間的確充實無比，但我算是外行人，對領域涉獵不深又缺乏自信，比較不是「帶著問題」去實習。這真的蠻可惜的，如果事先準備好問題，一定可以向前輩們請教更多知識和經驗。信心不足也反映在另一個小事件上，我總是覺得程式寫得不夠好 (不夠 elegant)，想一改再改，code 都推上去了但遲遲不敢發 MR，直到同事問我不是寫好了嗎為什麼 gitlab 上沒看到...

&nbsp;

## 結語

回想起來，我的打工或實習似乎總是離不開資料：升大學的暑假在補習班管理學生資料，大二在教育局整理學校資料，碩班在 lab 的研究還有 NTU cool 的工讀也都在碰資料。兩個月的實習很像跑步，剛起步的時候春風得意，好像什麼事都難不倒。跑一段時間後氣喘吁吁，開始有撞牆的感覺。習慣了之後又找回步調，穩定前進。快到終點時好像有道無法突破的檻，覺得看不到希望。不過堅持到最後就輕鬆了，應該說比較不擔心了。小時候學鋼琴，老師說我彈琴看起來很怕，好像琴鍵會咬我一樣。長大後學程式也總是怕怕的，戒慎恐懼敲著鍵盤，好像 error message 會讓電腦爆炸一樣。希望自己可以好好善待心裡莫名的恐懼，反正只要穩紮穩打大步慢走就好了 (Lopers 內梗，get it?)

{{< figure src="card.jpg" title="HR 辦實習超用心，每個實習生都收到一張主管寫的小卡" width="60%" height="auto">}}

&nbsp;

Photo by <a href="https://unsplash.com/@laurenmancke?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Lauren Mancke</a> on <a href="https://unsplash.com/s/photos/computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
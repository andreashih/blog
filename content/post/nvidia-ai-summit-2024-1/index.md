---
title: "2024 NVIDIA AI SUMMIT 紀錄 - 智慧製造與其他"
description: "今年很幸運有機會參加 NVIDIA AI Summit，參觀現場展示的最新 NVIDIA AI 技術，並聆聽 11 場精彩的演講。內容豐富又精實，讓人對 AI 的未來充滿熱血沸騰的期待，確切呼應了本次會議的大標語 -- 「探索 AI 時代的無限可能」。"
date: 2024-06-05
slug: 
image: ai-summit.jpg
categories:
    - working
tags:
    - talks
---

## Demo Booth

會議開始前，在現場的 Demo Booth 與 NVIDIA 的各位專家交流。很佩服他們能夠清晰地講解 AI 產品的特點，並以簡明易懂的方式回答聽眾的各種問題。

{{< figure src="demo_booth/demo-booth.jpg" title="Demo Booth" width="60%" height="auto">}}

{{< figure src="demo_booth/demo-booth-2.png" title="現場展示的酷東西" width="80%" height="auto">}}

### NVIDIA Avatar Cloud Engine (ACE) for Games

{{< youtube id="uryeFhnNzEs" title="NVIDIA ACE | NVIDIA x Inworld AI - Pushing the Boundaries of Game Characters in Covert Protocol">}}

玩家可以透過語音和 AI NPC 進行互動。自動語音辨識 (ASR) 模型將語音轉換成文字，再由大型語言模型 (LLM) 生成 NPC 的回覆，最後再通過文字轉語音 (TTS) 技術將回覆播放出來。角色說話時的嘴型和表情都能與語音搭配，提供了更加沉浸式和細緻的遊戲體驗。

使用到的生成式 AI 技術有：
- [NVIDIA NeMo](https://www.nvidia.com/zh-tw/ai-data-science/products/nemo/)：是一款 end-to-end cloude-native LLM 框架，可運用遊戲中的人物特色客製化調整 LLM，並且使用 NeMo Guardrails 來保護生成內容安全性。
- [NVIDIA Riva](https://www.nvidia.com/zh-tw/ai-data-science/products/riva/)：用於自動語音辨識及文字轉語音，實現即時對話。
- [NVIDIA Omniverse Audio2Face](https://www.nvidia.com/en-us/ai-data-science/audio2face/)：為遊戲角色建立臉部表情動畫。

### Nvidia Inference Microservices (NIM)

{{< figure src="demo_booth/nim.jpg" title="Gen AI Inference with NIM" width="60%" height="auto">}}

💻 [**Demo 連結**](https://build.nvidia.com/explore/discover)

NIM 是專為管理和部署大型語言模型 (LLM) 而設計的微服務，提供快速穩定的框架，支援許多主流的 LLM，也包括最新加入的 [Llama 3](https://llama.meta.com/llama3/)。

除了雲端模型，NIM 也可以管理地端 fine-tuned 的模型。使用者可以一次生成多達 30 次的結果，並且能夠替換不同的參數，讓調參和監測生成結果更加便利。此外，NIM 也具備監控 latency 和 token usage 的功能，方便管理資源。

## 人工智慧引領下一波工業數位化
***Deepu Talla**, 機器人和邊緣運算副總裁, NVIDIA*

在 AI 蓬勃發展的趨勢下，重工業也開始引入軟體，加快了工業數位化的進程。台灣正處於工業數位化的核心地帶，多家製造商 (如鴻海、台達電、和碩、緯創) 正在建設工廠的數位孿生 (Digital Twins)。

NVIDIA 目前主要有兩大機器人平台：[Isaac](https://developer.nvidia.com/isaac) 和 [Metropolis](https://developer.nvidia.com/metropolis)，本演講著重介紹 Isaac 的框架和實際應用場景。

{{< figure src="digital_twin/isaac.gif" title="NVIDIA Isaac (source: https://developer.nvidia.com/isaac)" width="70%" height="auto">}}

NVIDIA Isaac 是用於構建 AI 機器人的開發平台，[NVIDIA Isaac Sim](https://developer.nvidia.com/isaac/sim) 則是用來設計、測試和驗證機器人的平台。Isaac 機器人平台的最新功能有以下三項：

1. [Isaac Perceptor](https://developer.nvidia.com/isaac/perceptor): 利用多重鏡頭及 3D 環繞視野，使機器人能勝任製造業生產線及物流配貨中心的工作。
1. [Isaac Manipulator](https://developer.nvidia.com/isaac/manipulator): 提供多款基礎模型，讓機器人手臂完成更多任務。
1. [Project GR00T](https://developer.nvidia.com/project-gr00t): 用來生成文字和圖像的模型，讓人形機器人能夠與人類互動。

## 利用數位孿生建造未來工廠
***呂佳翰**, 廠長, 緯創資通*

🎬 [**影片連結**](https://www.youtube.com/watch?v=OAdqXZGUb70)

在建造未來工廠的過程中，ESG (環境、社會、治理) 是關鍵點。導入 NVIDIA 的解決方案，可以提升能源利用率，減少資源及溝通成本浪費，甚至可以克服時差問題進行遠端協作。

緯創基於 [NVIDIA Omniverse](https://www.nvidia.com/en-us/omniverse/) 建立了 WiDT，將 IoT 數據整合到環境中，並透過視覺化 dashboard 進行監控。[NVIDIA CloudXR](https://www.nvidia.com/zh-tw/design-visualization/solutions/cloud-xr/) 則提供了強大的 XR 體驗，可以觀測未來的工廠建造。建造數位孿生，可以透過數據的 simulation 考量所有狀況，例如工廠內的熱流、功耗、空間運用等，將工廠 layout 產出最大化。

## 創建數位孿生優化生產線
***彭志誠**, DSM 先進運營技術處長, Delta*

🎬 [**影片連結**](https://www.youtube.com/watch?v=K5gbmr3I5O4)

台達以環保節能為特色，專注於 power chip/device、手機被動元件等產品，涵蓋從印刷電路板 (PCB) 到半導體，再到數據中心和基礎設施的完整產業鏈。在接下來的 50 年中，台達致力於創建自動化和無碳環境，並提供智慧製造解決方案。

面臨全球分散製造的挑戰，如何確保生產線的可持續性 (sustainability) 成為重要課題。過去需要在設計完成後才能進行現場模擬，但現在可以透過數位孿生 (digital twins) 解決方案，在虛擬環境中進行預先模擬。

台達使用 NVIDIA Omniverse 建立了數位孿生解決方案平台，並獲得了顯著的好處：
1. 加速 NPI (New Product Introduction) 團隊的開發速度：透過訓練每個設備的 AI recipe，將 NPI (新產品導入) 的前置時間縮短了 10%。
1. 目標零缺陷 (zero defects) 的品質管控：通過歷史數據分析，提高 25% 的 repair/debug efficiency，並能透過資料找到問題的 root cause，從而提升產品品質。
1. 創新協作：通過 e-learning 系統，將作業員的培訓時間減少 30%。

## 賦能高效萬億參數的 AI Enabling Efficient Trillion Parameter AI
***Marc Hamilton**, 解決方案架構與工程副總裁, NVIDIA*

> Efficiency is in our DNA.

現今 AI 計算需求呈爆炸式增長，最新模型的能耗也不斷增加中。NVIDIA 致力於應對此一挑戰，透過加速計算技術節省了時間和能源。

AI 的發展循環有以下步驟：

1. 訓練模型（極限壓縮數據）
1. 部署到雲端、機器人等
1. 生成更多數據
1. 微調模型
1. 返回第一步，重新訓練

AI 的安全性與效率同樣重要。30 年前，人們認為軟體不安全，但隨著技術的進步，軟體的安全性也隨之提升。現在開發者與研究者也致力於使 AI 變得更加安全。

## 建造未來可持續的人工智慧工廠 Building Sustainable AI Factories of the Future
***彭志誠**, DSM 先進運營技術處長, Delta*  
***Simon Chang**, Senior Group Director, Regional System Solution, Asia Pacific & Japan, Cadence*  
***Aditya Ramkrihna**, General Manager, Digital Industries, Siemens Taiwan*  
***Dion Harris**, Director, Data Center & HPC, NVIDIA*  

### Delta
自 2010 年以來，台達一直致力於智慧製造和自動化，提前規劃並為未來做好準備。NVIDIA Omniverse 加速了智慧製造的進程，在 AI 工廠中，機器可以自動捕捉關鍵特徵（如參數和 signals），並運用智能技術進行自我調整。

### Cadence
Cadence 專注於降低功耗，致力於打造高效率且環保節能的 AI 工廠。透過 simulation 優化設計，不僅為客戶節省了成本，還改善了環境和 community 的整體品質。

### Siemens
Siemens 構建數位孿生模型，資源使用更少，且能實現逼真且實時的 simulation。此外，生成式 AI 也可以應用於 PLC編程，通過自然語言替代傳統的 PLC 程式。

## AI 開發藥物新境界：如何加快 PROTAC 的設計
***Chien-Ting Kao**, 人工智慧副研究員, 安宏生醫*

PROTAC（Proteolysis Targeting Chimeras）是一種設計用於降解目標蛋白質的技術。PROTAC 會透過辨識目標蛋白，將其標記並引導至降解機制。

NVIDIA 為新藥開發提供了便捷的 AI 工具：
- NVIDIA Inference Microservice (NIM)
- [BioNeMo Microservice](https://www.nvidia.com/zh-tw/clara/bionemo/)
- BioNeMo Framework

這些框架和微服務提供了許多模型，用於表徵蛋白質和生成蛋白質結構。

在設計 PROTAC 時，需要考慮以下要素：
- 合理性（validity）：確保設計出的結構是合理的。
- 唯一性（uniqueness）：確保生成的結構不重複。

成功的藥物分子需要能夠與兩端的蛋白質結合，以確保藥效的達成。藉由 AI 的幫助，有望在早期藥物開發階段減少研發時間和成本。
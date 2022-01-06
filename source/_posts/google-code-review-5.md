---
title: Google Code Review - Reviewer 篇 (4)
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR
  - translation
  - 翻譯
disqusId: google-code-review-5
keywords:  code review, google, note, PR, pull-request, author, guideline, 翻譯, 筆記
date: 2021-12-14 00:41:28
categories:
  - Note
cover: gallery/cover/lagos-techie-kwzWjTnDPLk-unsplash.jpg
thumbnail: gallery/cover/lagos-techie-kwzWjTnDPLk-unsplash.jpg
---

這篇主要整理如何加速 code review 的速度, 以及 code review 速度對於整體開發流程的影響，為針對 reviewer 系列的第四篇文章，為 google code review 筆記系列的的六篇文章。

<!--more-->

# Why Should Code Reviews Be Fast?
應該優化整體團隊開發產品的效率，並非單獨開發者的開發效率。

code review 速度很慢的話可能會引發的問題
1. **整體團隊開發速度下降**
2. **開發者抗議 code review 的流程**
若 reviewer 幾個天或是幾周才 review 一次，且每次都要求更改很多地方，這會讓 developer 很沮喪，進而降低開發的速率，且大多數的對於 code review process 的抱怨都可以透過加速 review process 來得到解決。

3. **code health 被影響**
緩慢的 code review 會影響 code 的 cleanups, refactorings 以及一些對現有系統的改進。同時也會增加 developer 的壓力。

# How Fast Should Code Reviews Be?
- **若您不是在需要很重要的任務上，你都應該優先去 review CL(PR)**
- **一個工作天是最長可以被忍受的時間(第二天早上的第一件事)**
- **一天應該對一個CL(PR)進行多次review直到被合併進repo**

# Speed vs. Interruption
若當前正在寫 code 則請繼續完成，不要被 code review 打斷，研究表明 developer 在被中斷後可能需要很長時間才能恢復並進入狀態，因此若在開發過程中，請先完成手邊的工作或使其進行到一段落在進行別人請求的 code review, 就跟電腦 CPU一樣，做 context switch 多少都會浪費掉時間對吧?!

# Fast Responses
即便 code reivew process 可能拖很長的時間，還是必須盡量快速的響應 developer 所提出的 code review 請求，個人的快速回應可以大大降低 review 時間拖很長的挫敗感。

若你手邊有很忙的事情，可以先通知 developer 讓他知道大約何時 code review 會完成，或者先留下一些比較 critical 的 comment 讓 developer 可以先進行修正，抑或是請對應的人先幫忙 review。

**LGTM** 表示已經可以達到 merge master 的標準，此時 developer 可以選擇繼續把細微的問題修正或是直接 merge。

# Cross-Time-Zone Reviews
因為疫情的關係越來越多 remote 以及跨國跨時區的工作型態，盡量在 developer 時區工作時間回覆 comment, 假使 developer 已經回到家, 確保在他們第二天回到辦公室之前完成您的 review & comment。

# LGTM With Comments
為了加速流程，以下兩種情況可以先留下 **LGTM/Approval**  的評論，即便還有地方要修正:
1. reviewer 確信 developer 會適當地解決審閱者的所有剩餘評論
2. 剩下的修改很小，不一定需要修改只是 reviewer 給予的建議

由於跨時區的關係，有時等待一整天只是為了得到 **Approval/LGTM** 確實會浪費掉不少時間，請多採用 LGTM with Commens 方式讓 developer 知道哪些部份修正後測過確定沒有問題就可以自行合併了。

# Large CLs
太大的 CL(PR) 很難 review, 且通常會拖慢整個 review 流程。{% post_link  google-code-review-1 '可以請 developer 依照不同功能切成小一點的 CL(PR)。' %}

若無法將CL(PR) 切小，可以採取上述的做法，先快速看過點出問題請 developer 先進行修改，並在手邊事情告一段落時再進行完整 reveiw, 作為 reviewer 主要的目標之一為協助 developer 可以快速得到回應並修正改善 codebase quality.


# Code Review Improvements Over Time
若你按照上述的準則進行 code review, 應該能感覺到 review 的流程越來越快，同時 developer 也會學習到哪邊是應該要避免的錯誤，慢慢的 developer 的 CL(PR) 需要更動的地方也會越來越少，reviewer 盡量的快速回應 CL(PR)，達成正向的循環。

# Emergencies
若有非常緊急的問題需要修正，則可還是必須要走過完整的 review process, 但可以 code quality 要求的寬鬆一些，以下為 [Emgergency](https://google.github.io/eng-practices/review/emergencies.html#what) 的定義。


# Conclusion
感謝您的收看，此為第六篇 google code review 的筆記，應該還剩下最後兩篇 XD，下一篇將會講述 Review Comments 應該如何撰寫~
[可以點擊這邊 Google Code Review 全系列筆記瀏覽 code review guideline 全系列筆記文章 :)](/collections)
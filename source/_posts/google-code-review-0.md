---
title: Google Code Review - Overview 篇
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR
disqusId: google-code-review-0
keywords:  code review, google, note, PR, pull-request, author, guideline
date: 2021-11-28 20:55:57
categories: [Note]
cover: 'gallery/cover/john-schnobrich-2FPjlAyMQTA-unsplash.jpg'
thumbnail: 'gallery/cover/john-schnobrich-2FPjlAyMQTA-unsplash.jpg'
---
此篇為 Google Code Review Overview 的介紹, 主要擷取自 [Google Code Review Guideline](https://google.github.io/eng-practices/review/) 的內容, 後續會陸續分為 Reviewer 以及 Author 兩部分文章紀錄，若內容有誤歡迎大大們指正，感激不盡 d(`･∀･)b

<!--more-->

# 介紹
![](code-quality.png)
*reference: https://blog.claudiupersoiu.ro/2011/10/04/code-quality-and-development-time/lang/en/*

大家都知道開發系統時系統的 code quality 以及健康度會隨著時間下降，為了避免這種問題 code review 就顯得非常重要，藉由多一些人把關檢查來提升品質，而 Google 也提出了內部的一些 review, author 的準則，以下就簡單整理一下 XD

# 應該要被 Review 的事項
1. Design: 提交的 code 是否有更好的設計? 設計是否會跟現有系統造成衝突，作法是否符合原本系統的 convention 等等
2. Functionality: 確認提交的 code 行為符合作者的預期? 行為是否對使用者造成問題等等?
3. Complexity: 是否可寫的更簡潔? 未來的開發者是否能直接讀 code 就知道在幹嘛，寫法是否方便往後修改或是 reuse ?
4. Tests: 修改部分對應的測試是否有一併被加上呢?
5. Naming: 類別、方法、變數的命名是否遵循規範? 可讀性及代表涵義是否清楚?
6. Comments: comments 是否清楚且有幫助?
7. Style: coding style 是否有符合規範?
8. Documentation: 對應的文件是否有一併更新?

## 挑選適合的 Reviwer
請挑選最合適的 Reviewer, 挑選了解該代碼的人, 可能是過去的 owner, 有時一個 CL (PR) 會需要請不同人去 review 不同段的代碼, 請找到最適合的 reviewer, 若該人無法進行 review 至少也要 CC 他們, 通知他們你所進行的更動。

## In-Person Reviews
若是跟 Reviewer 一起進行開發，則該段代碼可以視為已 review, in-personal review, reviewer 提出問題, 開發者只在 reviewer 提出問題時回答並進行修改。

## Conclusion 
感謝您的收看, 此篇為較粗略的介紹, 將在後續文章詳述細節的部份 (つ´ω`)つ

[歡迎點擊這邊 Google Code Review 全系列筆記瀏覽 code review guideline 全系列筆記文章 :)](/collections)

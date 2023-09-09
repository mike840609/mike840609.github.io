---
title: Google Code Review - Reviewer 篇 (5)
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - pr
disqusId: google-code-review-6
keywords: code review, google, note, PR, pull-request, author, guideline, 翻譯, 筆記, 中文
date: 2021-12-22 01:32:05
categories:
  - Note
cover: gallery/cover/christina-wocintechchat-com-OW5KP_Pj85Q-unsplash.jpg
thumbnail: gallery/cover/christina-wocintechchat-com-OW5KP_Pj85Q-unsplash.jpg
---

正如封面的照片一樣，code reviewer 的氛圍應該是要開心愉悅的，而不是針鋒相對，接續{% post_link  google-code-review-5 '上篇 Google Code Review - Reviewer 篇 (4)' %}，本篇住要講述 reviewer 的 comments 應該如何撰寫，以及一些應該注意的事項 ლ(╹◡╹ლ)

<!--more-->

# Summary
- 友善交流
- 解釋您的看法
- 在點出問題以及給予問題解答讓開發者決定兩者之間找到平衡
- 鼓勵開發者簡化代碼或是添加註解在code中，而不是單純向您解釋

# Courtesy
[**尊重&禮貌**](https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/cr_respect.md)為code review 中很重要的事情，且評論請針對 code 而不是針對 developer 舉例如下:

> Bad: “Why did you use threads here when there’s obviously no benefit to be gained from concurrency?”

> Good: “The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there’s no performance benefit, it’s best for this code to be single-threaded instead of using multiple threads.”

# Explain Why
解釋您留下 comment 的原因，讓 developer 了解 **為何** 你會留下comment, 並不是所有地方都需要留下 comments & 原因，而是針對 developer 可能不理解的地方留下原因，例如這樣做符合 desing pattern, 這樣做可能有哪些 side effect, 或是這樣未來比較好維護等等的原因。

# Giving Guidance
**一般而言修正 CL(PR) 為 developer 的責任，而非 reviewer 的責任**，reviewer 沒有義務去做細節的 design 或是直接幫 developer 寫 code。

但這並不代表 review 沒有幫助，reviewer 應該在**指出問題點**以及**直接指導**間取得平衡，單純指出問題點讓 developer 做決定可以幫助 developer 學習，同時對 reviewer 也會比較輕鬆，同時因為 developer 對自己寫的 code 比較清楚，通常 reviewer 點出問題點讓 developer 做決定也會比直接由 reviewer 直接給出解法效果要來的好。

不只是問題應該被點出，若 reviewer 看到 CL(PR) 中有很棒的地方應該也要點出來讓 developer 知道，。

> 舉例而言: 當看到 developer 清理原本雜亂的 algorithm, 提升 test coverage, 或者任何你從 reviewe 過程中學習到的事情，也都應該留下評論藉此鼓勵 developer 讓 developer 在未來繼續保持良好的實踐。

# Accepting Explanations
若 reviewer 要求開發者解釋一段不清楚的 code, 通常 developer 會選擇直接重寫讓那段 code 變得比較易讀，有些時候比起整段重寫加一些註解可能會更適當，當然前題是原本的 code 沒有過於複雜。

**若只在 code review tool (Github) 留下 comment 對未來的 developer 沒有太大的幫助**(除非他跑來翻 PR 看過去的討論串才能知道一些 context)，應優先考慮讓 code 變得易讀，或是在一些關鍵的地方加上註解。

# Conclusion 
感謝您的收看，這篇主要筆記了 reviewer 的 comments 應該如何撰寫，以及那些東西應該被 comments，接下來就是最後一篇了，會講述一些在 code review 中 comment 的來回應對 :)

[歡迎點擊這邊 Google Code Review 全系列筆記瀏覽 code review guideline 全系列筆記文章 :)](/collections)
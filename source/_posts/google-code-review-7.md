---
title: Google Code Review - Reviewer 篇 (6)
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR
  - 翻譯
disqusId: google-code-review-7
keywords: code review, google, note, PR, pull-request, author, guideline, 翻譯, 筆記, 中文
date: 2021-12-25 19:23:28
categories:
  - Note
cover: gallery/cover/christina-wocintechchat-com-OW5KP_Pj85Q-unsplash.jpg
thumbnail: gallery/cover/christina-wocintechchat-com-OW5KP_Pj85Q-unsplash.jpg
---

code review 中 developer 以及 reviewer 意見不和是常常發生的事情，有時 developer 會不同意 reviewer 的觀點，有時候 developer 會覺得 reviewer 太過嚴格，這時候應該要如何解決呢?  這篇筆記會記錄 google code review 中給出的一些建議 (´◉‿◉｀) 


# Who is right?


# Upsetting Developers


# Cleaning It Up Later
盡量避免之後開另一個 CL 修正一些相關的錯誤，可以的話盡量把在 PR 中被點出的錯誤修正，如果需要修改的範圍太大一定要開另外一個 CL(PR) 來修正的話，一定要記得開一張對應的 Ticket 並且寫好 description 並且 assign 給自己，並且在 Code 中加上對應的 TO-DO comment，才不會問題越滾越多然後都忘記要修正 ( •́ω•̩̥̀ )

# General Complaints About Strictness
如果過去 code review 相當鬆散，突然變的嚴格，會導致 developer 抱怨。加快 review 的速度會讓情況緩解。

有時抱怨的情況可能會持續長達幾個月，但隨著時間推進 developer 會逐漸了解的嚴格 code review  所帶來的效益，可能是 code 變得易讀或是 bug 變少等等之類的效益。

# Resolving Conflicts
若遵照上面提出的準則還是無法解決，請參閱{% post_link  google-code-review-2 'The Standard of Code Review' %}解決衝突。

# Conclusion 
感謝您的收看，到目前為止為 google code review 的完整筆記, overview 1 篇, author(developer) 1篇, reviewer 5 篇，可以點擊這邊瀏覽 google code review guideline 全系列文章 。
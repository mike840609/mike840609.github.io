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
通常 developer 相比 reviewer 而言會更熟悉自己修改的 code, 若 developer 不同意您的建議，需要跟 developer 釐清，若 developer 是對的必須必須讓他們知道，並關閉提出的問題以及修改建議。

但若您很確定您的評論是正確的，應該詳細解釋讓 developer 知道，並且禮的指出怎麼做可以提升 code quality, 有時候一個建議需要經過幾輪的討論，切記要保持禮貌，並且讓 developer 知道自己提出的意見有被收到，只是有其他更好的建議作法可以採用。

# Upsetting Developers
作為　reviewer 可能會擔心過度嚴格的標準會導致 developer 不開心，有時候確實會使 developer 感到沮喪，但通常只是短暫的，之後 developer 更有可能會感謝您幫他們提高 code quality, 若是出於好意且用詞禮貌的提醒基本上都不會讓 developer 不開心。

# Cleaning It Up Later
盡量避免之後開另一個 CL 修正一些相關的錯誤，可以的話盡量把在 PR 中被點出的錯誤修正，如果需要修改的範圍太大一定要開另外一個 CL(PR) 來修正的話，一定要記得開一張對應的 Ticket 並且寫好 description 並且 assign 給自己，並且在 Code 中加上對應的 TO-DO comment，才不會問題越滾越多然後都忘記要修正 ( •́ω•̩̥̀ )

# General Complaints About Strictness
如果過去 code review 相當鬆散，突然變的嚴格，會導致 developer 抱怨。加快 review 的速度會讓情況緩解。

有時抱怨的情況可能會持續長達幾個月，但隨著時間推進 developer 會逐漸了解的嚴格 code review  所帶來的效益，可能是 code 變得易讀或是 bug 變少等等之類的效益。

# Resolving Conflicts
若遵照上面提出的準則還是無法解決，請參閱{% post_link  google-code-review-2 'The Standard of Code Review' %}解決衝突。

# Conclusion 
感謝您的收看，到目前為止為 google code review 的完整筆記, overview 1 篇, author(developer) 1篇, reviewer 5 篇，可以點擊這邊瀏覽 google code review guideline 全系列文章 。
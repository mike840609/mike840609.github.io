---
title: Google Code Review - Reviewer 篇 (3)
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - pr
categories:
  - Note
cover: gallery/cover/fatos-bytyqi-Agx5_TLsIf4-unsplash.jpg
thumbnail: gallery/cover/fatos-bytyqi-Agx5_TLsIf4-unsplash.jpg
disqusId: google-code-review-4
keywords: code review, google, note, PR, pull-request, reviewer, developer, guideline
date: 2021-12-14 00:37:31
---


接續{% post_link  google-code-review-3 '上篇 Google Code Review - Reviewer 篇 (2)' %}本篇為 reviewer 相關的第三篇，上篇為 reviewer 在 code review 中應該要注意的細節，而本篇主要會筆記一下 Reviewer 的 review 順序建議 ( • ̀ω•́ )

<!--more-->

# Summary
從{% post_link  google-code-review-3 '上一篇' %}我們知道了作為 reviewer 時應該要 review 的細節, 然而應該要如何進行才能比較有效率的 review 多個檔案呢?

文中建議的 Review 順序
1. CL (PR) 是否合理? developer 寫的 Pull-Request {% post_link  google-code-review-1 'description' %} 清楚嗎?
2. 先審查 CL(PR) 中最重要的部分，並且確定整體的設計是良好的。
3. 查看剩餘的 CL(PR) 部分。

# Step One: Take a broad view of the change
參照{% post_link  google-code-review-1 'description' %}中的建議檢查 Description，並且確保此次的 CL(PR) 合理，一旦發現 CL(PR) 不符合要求請立馬通知 develpoer, 並告知原因, 藉此避免 developer 浪費時間進行不必要的開發，必且建議或跟開發者討論後續應該進行的方向，也節省團隊的時間

當發現developer CL 出現了不合乎預期的狀況，文中給出的範例回覆如下
> Looks like you put some good work into this, thanks! However, we’re actually going in the direction of removing the FooWidget system that you’re modifying here, and so we don’t want to make any new modifications to it right now. How about instead you refactor our new BarWidget class?`

從上述的範例我們**禮貌**的拒絕了此次的 CL (PR), 同時也提供了 developer 對應應該努力的方向，文中一直提到了 **禮貌** & **尊重** 的重要性，畢竟不會有人希望自己的努力被說的一無是處對吧?

若 CL (PR) 中出現了太多不預期的狀況，可能必須考慮修正 Code Review 流程，與其在需求不明確時就實作，更應該在需求明確且團隊成員認知相同時再進行實作，這樣可以避免 developer 寫了一堆 code 結果發現不符合需求，得要全部砍掉重練的情況也就是大家常說的**預防勝於治療** (*´ω`)人(´ω`*)

# Step Two: Examine the main parts of the CL(PR)
找出 CL(PR) 中主要的部分優先進行 review, 通常會是 CL(PR) 中改動最多的部分，若改動的部分太多，難以找到主要的 CL(PR) 部分，可以求助 developer 詢問那邊是重點的部分應該先被 review, 並且可以要求 developer 將一個太大難以 review 的 CL(PR) 依照功能或是改動部分切為數個小一點的 CL(PR) 以方便 review.

若有看到 CL(PR) 中有明顯的錯誤，即便還有許多剩餘的部分還未 review,，應該先留下 comment 讓 developer 知道，甚至如果您先進行review 還有可能是在浪費時間，因為後續的部分有很大的機率會跟著修改。

以下為兩個當主要設計出現問題時您應該要立刻提出的主要的原因:
1. 由於開發者可能基於此 CL(PR) 繼續往下開發，但設計問題可能導致後續的 CL(PR) 需要一併做修改，因此為了幫助 developer 節省時間，應該要先告知他們有問題的部分，避免後續 CL(PR) 需要全部修改一輪。
2. 主要的設計問題修改會比小地方的修正需要花費更多的時間，而開發往往都會有壓期限，為了趕上在期限內完成，請盡速通知 developer 主要部分的問題，讓他們有更多的時間進行修改並提高程式碼的品質。


# Step Three: Look through the rest of the CL in an appropriate sequence
當確認設計沒有問題且完成了主要部分的 review 後，接續進行剩餘檔案的 review，請確保您的對改動部分完全理解，有時候也可以從 test 下手，先看 test 的測項對於 review 也有一定的幫助，可以從 test 中去推斷功能的預期的邏輯為何。
[歡迎點擊這邊 Google Code Review 全系列筆記瀏覽 code review guideline 全系列筆記文章 :)](/collections)
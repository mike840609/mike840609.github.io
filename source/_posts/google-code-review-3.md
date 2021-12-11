---
title: Google Code Review - Reviewer 篇 (2)
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR
categories:
  - Note
cover: gallery/cover/lala-azizli-cBUTPbTeDB0-unsplash.jpg
thumbnail: gallery/cover/lala-azizli-cBUTPbTeDB0-unsplash.jpg
disqusId: google-code-review-3
keywords: code review, google, note, PR, pull-request, author, guideline
date: 2021-12-11 10:18:11
---


本篇接續{% post_link  google-code-review-2 '上篇 Google Code Review - Author 篇 (1)' %}為 reviewer 相關的第二篇，主要會敘述 code review 中應該要被 review 的事項以及詳細的細節，特殊情況下的應對等等，若有寫錯或是表達不清楚的地方，也請大大們鞭小力一點 (✪ω✪)

<!--more-->

# Design 
---
這部分是最重要的一環，必須確保 CL (PR) 整體的設計沒有問題，包含以下條列事項
1. 此次的變動是否合理? 
2. codebase 中是否已有相同的 library 可以直接呼叫使用? 
3. 此次的變化應該修改到共用的 library 中嗎? 
4. 這次的修改跟系統整合後會不會出問題? 
5. 現在是添加功能的好時機嗎?

# Functionality
---
這部份則是功能性相關的檢查，
1. 此次的變更是否符合開發者一開始的意圖?
2. 這次的修改對 developer 以及 end-users 的影響?

大部分的情況開發者都會實作對應的 test case 去確保功能性正常，但 edge case 或者 corner case 可能會被忽略，這時候就需要借助 reviewer 來幫助做多一層的把關，concurrency problems、async、sync 等等的相關問題也可以在 review 的過程中再做多一層的把關，並試圖站在 user 的角度思考哪些操作可能會造成問題等等，並確保最後 deliver 的 code 為bug free 且高可讀性。

若牽扯到 UI 的變動，有時候無法直接從 CL (PR) 中看出修改造成的影響，此時可以請 developer Demo 給您看，確保修改合理。

另一類很難被發現的問題像是 parallel programmin, deadlocks, 或是 race conditions 等等所造成的問題也很難在 review 時候被發現，必須多留意

# Complexity
---
應該要避免 CL (PR) 太過複雜，應該讓邏輯盡量保持簡單，避免太多的語法糖，然而如何定義太複雜呢，文中給出了一個衡量標準

> *can’t be understood quickly by code readers.*

> *developers are likely to introduce bugs when they try to call or modify this code.*

若出現以上兩種情況，則有可能代表你寫的太複雜了，通常若是開發者想要將 code 弄得非常 generic 而導致 	**over-engineering** 的情況，或者添加了一些當前不必要的功能，這都會導致 code 變得複雜、可讀性差，Reviewer 應該對此提出問題，並且鼓勵 developer 先解決當前問題，而不是推測未來問題而將 code 過度模組化。

# Tests
---
Reviewer 應該要求 Developer 在 CL (PR) 中加上對應的測試，包含 unit test, integration test, or end-to-end test 等等，除非此次 CL (PR) 處在緊急的狀況，並且確保撰寫的測試有效，同時應該確保代碼發生變化導致邏輯發生問題時測試應該要失敗。 以下唯一些準則 :

1. code run-time failed 時測試會如預期般的失敗嗎? 
2. 當邏輯改變時 是否會有 false postives 的情況產生? 
3. 測試中的 assert 是否有用，且覆蓋率足夠高? 
4. 是否洽當的在不同 function 間進行測試?
5. test case 在未來也會需要被維護，也要注意複雜度不要過高。

# Naming
---
是否有挑選洽當的命名? 應該在一定的長度內盡可能的讓讀者知道這個變數、方法、類別是用來做甚麼的。

# Comments
---
這邊指的 comments 為 codebase 中所留下的 comments 而非 CL (PR) 討論中來回的 comments，怕會搞混先寫在前頭 XD

1. developer 留下的英文 comment 是否足夠清楚的說明想要表達的事項?
2. 是否有多餘的 comment 
3. 通常 comment 用來說明為何這段 code 會存在，而不應該用來說明這段程式碼在做甚麼事情，或者是選擇此作法的背後原因，大多時候應該藉由可讀性高的code 來讓讀者知道這段 code 在幹嘛，而不是利用額外的 comment 來詳述其邏輯（有些例外：regular expression 和 較難讀懂的演算法 通常還是會藉由 comment 來傳遞訊息）。
4. 也可以看一下先前的 comments，找尋一些上下文的關係，有可能前人有留下 comments 來說明一些可能會遇到的問題等等。

# Style
---
此部分為 coding style 的規範，通常每間公司都會有一套自己的 coding convention, 若沒有的話也可以參照 google 提出的 [style guideline](http://google.github.io/styleguide/)

1. 使用 `Nit:` 引導開發者可以修正的變數、方法以及類別命名 
2. 不要因為個人的命名偏好而 block 住 code review 的流程
3. 盡量不要在有其他目的 CL (PR) 同時進行變數命名的修改，應該另外發一個 CL (PR) 去修改變數，並且將變數修改的 CL (PR) merge 進去 master 後，將目前的 CL(PR) rebase master branch 後再繼續進行修改，這樣可以簡化 review 流程，且較不容易出錯

# Consistency
---
1. 若當前的 code review 跟既有的 style guideline 不一致應該怎麼做呢? 請以 [style guideline](http://google.github.io/styleguide/) 最為最高指南

2. 有些時候，若有原本的 coding style 應該遵循既有的 coding style, 盡量與周圍的程式碼風格保持一致，但若遵照 [style guideline](http://google.github.io/styleguide/) 不會導致不一致性，則應該遵照指南

3. 若沒有其他規則遵照，則應該保持與現有的規則一致
4. 建議可添加 TODO　來記錄未來需要修正的 coding style 部分

# Documentation
---
若 CL (PR) 的修正部分包含了 build, test, interact 或是 release process, 請一併檢查對應的文件是否更新，包含 READMEs, google doc, g3doc page 以及任何相關的文件，若文檔缺失也請補上對應文檔。

# Every Line
---
請掃過 CL(PR) 中的每一行，且不要預設裡面是正確的，若因為 CL (PR) 太大而導致 review 需要較長的時間也應該讓 developer 知道，如果你看不懂 developer 寫的東西，那麼之後閱讀同一段程式碼的人也會遇到相同的問題，應該要求開發者說明該段程式碼的用意，並且討論是否有更簡易的作法方便未來閱讀。

若認為自己對該段程式碼不理解，或是需要更多的 context 補助，則應該請過去相關功能的開發者一起進行 review。

## Exceptions
如上面的例子，你可能是某方面的專家所以被要求協助 review，有時候你只被要求 review 其中一小段程式碼抑或是整體的架構，其餘的細節交由其他人負責，這時請在你 review 過的 part 留下對應的要求，並且在您認為達到標準後留下[LGTM](https://google.github.io/eng-practices/review/reviewer/speed.html#lgtm-with-comments)等 comment，讓開發者知道你 review 的部分沒有問題.

# Context
---
若使用 Github 作為 code review 工具會發現往往只會顯示包含修改內容的上下幾行相關程式碼，有時候你需要往上或這往下多看一些，確保你了解 context。

有時也需要更宏觀的去評斷這次的 CL (PR) 是否改善 codebase 的健康狀況? 還是會使整個系統變得更加複雜?是否需要更多的測試? 應該避免會使整個系統變得更加複雜的 CK(PR)，就跟堆雪球一樣，若每次 CL(PR) 都變得複雜一點點，則到最後整個 codebase 會變得超級複雜且難維護，因此在每次的 CL(PR) 中防止細小的複雜邏輯被引入到現有的 codebase 是很重要的。

# Good Things
---
若在 CL(PR) 中看到一些很棒的東西，請告訴開發者，讓他們知道，雖然 review 常常都是為了避免錯誤，但如果 developer 做的很棒應該也要給予鼓勵跟讚賞，教學相長，作為相互學習的目的而言，告訴他們做對甚麼有時甚至比告訴他們做錯甚麼有價值~ 

# Summary
總結來說 Review 重點可以歸納為以下幾點，並請確保以下事項
- Code 是否設計良好?
- 功能對使用者來說是否合理且完善?
- UI 的改變是否合理且美觀?
- Parallel programming 是否安全?
- Code 是否不會太複查，複雜度是否可以接受?
- 有沒有不必要的部分被一併提交?
- 對應的 Unit Test 有被補上嗎?
- Tests 是否測到所有應該被測試的情況?
- Naming 是否清楚?
- Comments 是否清楚且有用? 且請多使用 why 而不是 what 來撰寫 comments
- 對應的文件有被更新嗎?
- Coding style 符合規定嗎?

確保看過每一行或者被要求 review 的部分，多看 context 理解前因後果，確保 CL(PR) 提升 code health 並且對於 developer 做的好的部分給予鼓勵。

# 心得
感謝看到這邊的大大們，這部分的內容比較龐大，原本想說用三篇文章的篇幅來筆記一下 Reviewer 的部分，看起來應該失算了，為了避免文章過長，應該會超過三篇文章 QAQ 
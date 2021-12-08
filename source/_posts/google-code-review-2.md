---
title: Google Code Review - Reviewer 篇
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR
   
disqusId: google-code-review-2
keywords: code review, google, note, PR, pull-request, author, guideline
date: 2021-12-07 11:15:57
categories: [Note]
cover: gallery/cover/john-schnobrich-FlPc9_VocJ4-unsplash.jpg
thumbnail: gallery/cover/john-schnobrich-FlPc9_VocJ4-unsplash.jpg
---
如同{% post_link  google-code-review-1 '上篇 Google Code Review - Author 篇' %} 所述，此篇將整理 Reviewer 相關的筆記，因為 Reviewer 相關的內容較多，預計將分為三篇文章來記錄，一樣主要整理自 [Google Code Review Guideline](https://google.github.io/eng-practices/review/) 的內容 ლ(・´ｪ`・ლ)


<!--more-->


# The Standard of Code Review
Code review 的目的是要確保 code 的品質不會隨著時間而越來越差，但若是力求完美而將 review 的時間拖得很長又會拖慢開發的效率，以下有一些 trade-off 準則必須考量。

首先開發人員應該在每次 CL (PR) 都確保 code 能得到提升，若是完全不對過去的 code 進行 refactor 或是修正，雖然會加速 review 的速度，但 codebase 就永遠不會得到提升，反之若是 reviewer 非常嚴格，將每次都力求完美，則 developer 會因為挫折而不敢對過往的 code 進行修正。

因此 Reviewer 應該以 code health 作為首要條件，確保每次 code merge 後不會造成影響，同時確保 codebase health 不會隨著時間而下降，這其實非常的困難，因為通常的情況下 codebase health 必定會隨著時間的推移而緩速下降，尤其是在有時間壓力時，為了趕在 deadline 前上線，會利用短解趕快讓功能上線等等的情況都會造成 codebase health 下降。

而 Google 提出的 review 準則如下

>*In general, reviewers should favor approving a CL once it is in a state where it definitely improves the overall code health of the system being worked on, even if the CL isn’t perfect.*

上述的準則也是最高級的準則，任何情況下跟此準則有衝突，都應該以此準則為最高原則

>*No such thing as “perfect” code—there is only better code.*

上述解釋了為何 Reviewer 不應該要求 Author 把每次 CL (PR) 都用得非常完美，相較而言 Reviewer 應該要確保的是持續的改進　*continuous improvement*、提升系統的可維護性、程式碼的可讀性、程式碼的可理解性，同時不應為了一些不完美而推遲發布時間。

Reviewer 可以留下任何的評論來幫助 author 一起提升 code 的品質，但若是一些無關緊要的建議可以在前面加上 `Nit:`, 我一開始看到 comment 中出現 nit 時也一頭霧水，後來才知道原來是 nitpick (吹毛求疵) 的縮寫 XD

## Mentoring 
Code review 時可以盡量盡到教學相長的用意，留下你認為更好的 design、語法、設計原則、設計模式等等，reviewer 應該留下任何能夠幫助 developer 的評論，藉著共享知識來提高 codebase 的健康度，並且若只是出於提醒或是教育意義的評論，而不是一定要修改的評論可以如上述所說，在評論前面加上 `nit:`作為 prefix 來讓 developer 知道這則評論只是出於提醒的用意，並非一定要修正。

## Principles
- 技術事實以及數據應該凌駕於個人的偏好之上
- coding style 應該遵照既有的規則，若 reviewer 部分沒有既有的規則，可以透過 reviewer 跟 developer 討論而制定相關規則
- 對於系統設計或是架構相關的問題，不應單純使用個人偏好進行 review，而是應該透過一些共用的規則或是遵照某種設計模式來實作，若有多種解法則 development 應該提出來讓 reviewer 知道，並且說明選用該解法的原因以及跟其他解法相比的優點。
- 如果沒有規則可以遵照，則 reviewer 應該建議 developer 遵照當前的 codebase 中類似區塊的做法，並確保其不會造成 codebase 健康度下降。

## Resolving Conflicts
若在 review 的過程中發生意見的衝突，應該透過 [The CL Author’s Guide](https://google.github.io/eng-practices/review/developer/) 以及 [Reviewer Guide](https://google.github.io/eng-practices/review/reviewer/) 的準則來達成共識。

若還是無法達成共識應該擺脫 github comment 方式，藉由視訊軟體或是面對面來討論，藉此加速 review 的過程，同時要記得將討論結果記錄在 CL(PR) 的 comment 或是 description 上面，以此來讓後續的讀者知道過去討論的最終定案，以及選用此解法的原因。

然而經過上述的討論有時候還是會無法得到共識，此時應該藉助 team lead 或是 manager 甚至是邀請其他團隊中熟悉此功能開發者一起進來討論並衡量優劣，並尋求 team lead 或是 manager 做最終的決定。

# References
- https://google.github.io/eng-practices/review/reviewer/standard.html
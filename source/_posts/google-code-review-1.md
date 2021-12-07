---
title: Google Code Review - Author 篇
toc: true
tags:
  - google
  - guideline
  - code-review
  - pull-request
  - github
  - PR

disqusId: google-code-review-1
keywords: code review, google, note, PR, pull-request, author, guideline
date: 2021-11-29 01:58:05
categories: [Note]
cover: 'gallery/cover/alvaro-reyes-fSWOVc3e06w-unsplash.jpg'
thumbnail: 'gallery/cover/alvaro-reyes-fSWOVc3e06w-unsplash.jpg'
---

多人軟體開發流程中除了開發及測試外，另一相對重要卻常常被忽略掉的應該就是 code review process, 專案的開發過程中為了讓 code 品質可以更好，通常在功能開發完成要合併到 master branch 前都會需要至少一位相關的同事給予授權 (approval) 才能將修改的 code 合併進 master branch 中而在審核的過程就稱為 code review，然而事否有一套統一的準則能加速 code review 的過程並且提高 code review 的品質呢? 在網路上看了一些文章後有幸找到 Google 提出的 code reivew guideline，而當中分為 Reviewer 以及 Author 兩個部分，打算用兩篇文章分別筆記一下 XD(若有寫錯的部分也請大大們鞭小力一點)，本篇文章為 Author (提出修改者) 相關的筆記~ 

<!--more-->

# 何謂 Code Review (What)
code review 又稱作 changelist, change, patch, pull-request, 泛指開發者在本地做完變更後將修改內容合併到 master branch 前的審核工作，在審核批准後 code change 就會合併到 Master branch 並且部署到正式產品服務中。

示意圖
![](review_process.png)
*reference: https://dev.to/saymy__name__/git-workflow-for-periodic-jenkins-builds-801*



# 為何需要 Code Reivew (Why) 

1. 多一個人把關, 確認語法,架構,功能沒有問題
2. 確保功能符合預期
3. 確認 coding convention 符合規範
4. 藉由資深同事 review 來告訴你哪邊可以寫得更好, 以及提點你可能遺漏的部分
5. performace improvement

# 何時需要 Code Reivew (When)
可以藉由上圖得知在 code review 通常發生在 merge code 到 master branch 之前，但其實即便是單獨開發的 project 只要能標出特定範圍都可以進行 code review XD

# 在哪邊進行 Code Review(Where)
通常發生在 github 上面的 File Change 中， bitbucket 或是其他的開發整合工具應該也有對應的頁面但自身並沒有嘗試過，就不在此進行詳細討論(́◉◞౪◟◉‵)

# 誰需要進行 Code Review(Who)
1. project 主要 contributors
2. 過去對此 feature 有過相關開發經驗的開發者
3. Team 內此專案的負責人

然而在上述的第1, 2 點提到的 reviewer 可能不會有時間幫你 review, 但應該藉由 cc 讓他們知道你此次的修改，若有幸也可以得到過去相關 developer 的建議，一定可以少走一些冤旺路～


# 一些準則(how)
這邊才是主體，以下整理 Google code review guideline 中 Author 建議注意的一些事項 (^u^)

## Terminology
兩個術語，後續相關詞彙會使用縮寫代表~

- CL: “changelist” 的縮寫, 代表希望能 merge 進 master branch 而正在 review 的 code block. 也被稱做 “change”, “patch”, “pr“ or “pull-request”.

- LGTM: “Looks Good to Me” 的縮寫，Reviewer 講出此言論時通常 PR 即可 Merge 進 Master.

- LG: “Looks Good” 的縮寫

## Write Good CL Description 
CL 的描述可以分為 First Line 以及剩餘的 Body 兩部分
- First Line
  - 應該盡量簡短的描述這次的 CL 做了哪些事情。
  - 請使用完整的句子進行描述。
  - 在最後請加上一行空行。

- Body
  - 請詳細的描述修改的內容
  - 請詳述為何選用使用此種方式實作，使用其他方式的 pros, cons
  - 若此次的解法只是短解，請在 CL 中提及，並且標注出短解的 code block, 並考慮開啟對應的 ticket 追蹤
  - 若有背景知識需要讓 reviewer 知道請在 CL 中說明 (ex. bug numbers, benchmark results, link to design document)
  - 考慮到未來會有開發者來參照此次修改，請補足 context 供未來讀者查閱時能更快瞭解修改內容
  - 即便是很小的修改，也應該要有詳細的說明。

以下分別為一些好的例子以及不好的例子
### 不好的例子
- “Fix build.”
- “Add patch.”
- “Moving code from A to B.”
- “Phase 1.”
- “Add convenience functions.”
- “kill weird URLs.”

上述的 CL 其實都有些模糊，單看描述會不知道在做什麼事情，Fix Build 的哪一個部分？ 新增了哪些 patch? 為什麼要把 code 從 A 處搬到 B 處？ 什麼東西的 phase 1? 等等......

### 好的例子
以下節錄自[Author's Guideline](https://google.github.io/eng-practices/review/developer/cl-descriptions.html#firstline) 範例

Functionality change Example:
> rpc: remove size limit on RPC server message freelist.
> 
> Servers like FizzBuzz have very large messages and would benefit from reuse. Make the freelist larger, and add a goroutine that frees the freelist entries slowly over time, so that idle servers eventually release all freelist entries.

Refactoring Example:
> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which was only used by OOMCandidate to call borglet’s Now method). This replaces the methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on Borglet. Eventually, collaborators that depend on getting Now from the Task should be changed to use a TimeKeeper directly, but this has been an accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

Small CL that needs some context Example:

> Create a Python3 build rule for status.py.
> 
> This allows consumers who are already using this as in Python3 to depend on a rule that is next to the original status build rule instead of somewhere in their own tree. It encourages new consumers to use Python3 if they can, instead of Python2, and significantly simplifies some automated build file refactoring tools being worked on currently.

最後在 送出 & merge 前應該再次檢查 CL 的描述有符合本次的修改。

## Small CLs
為何應該讓程式碼維持多次小量的修改而不是一次大量的修改呢？ 除了比較好 Review 外也有眾多的原因，條列如下

- 因為涵蓋內容少，Reviewer 可以更快的進行 review
- 確保 reviewer 能看得更仔細，且思考的更全面
- 因為修改範圍小，bug 會更容易被找出
- 因為你只改了一點點，一有方向錯誤便能很快地察覺，反之若是花了一週弄一個很大範圍的 Code Change, 結果發現方向根本不對，這一週的時間就白白浪費掉了 QQ
- merge 若發生問題可以更快的 debug 因為修改範圍較小
- 小片段的程式碼更容易被 Reviewer 最佳化
- 避免 blocking, 在 review 的同時你可以繼續進行其他部分的 CL, 而不會被當前 review 的部分 block 住
- 發生錯誤時更容易 roll back 回穩定的版本
- 確保每次的 commit 可以成功 build 才能 merge 
- 確保修改包含對應的 test code
- Refactor 的部分應該獨立開一條 branch 來處理，不要跟 bug fix / fetaure changes 放在同一次更動

## How to Handle Reviewer Comments
這部分比為面對 Reviewer comments 時的心態調整及相關建議 XD

1. 不要帶著憤怒的情緒面對 reviewer 所留下的 Comments, Reviewer 也是為了提升 code 品質才花時間 review 並留下評論, 並竟應該沒有人想要故意把事情搞砸對吧？
2. 若 Reviewer 不理解您修改的 code, 大多時候你應該補充更多的上下文讓 reviewer 看懂你的 code，因為未來看這段 code 的讀者大多也會遇到一樣問題
3. 若是對 reviewer 的 comment 不清楚，也應主動詢問 Reviwer 所提出的問題，確保雙方的認知一致
4. 若堅決認為自己是正確的, reviewer 留下的 comment 存在著某些問題，請提供更多 context 給 reviewer，同時主動聯繫進行確認
5. 若無法跟 Reviwer 達成共識，請參照 [The Standard of Code Review](https://google.github.io/eng-practices/review/reviewer/standard.html) 並確保最終達成共識


# 結論
這篇大多就是集結 [Google author guideline](https://google.github.io/eng-practices/) 中所提到的一些準則，若有漏掉重要的訊息非常歡迎留言讓我知道，看完後才發現原來送出一個 PR 裡面還存在著很多眉眉角角要注要，而不是簡短寫一下了事，也警惕自己未來的 PR 應該要更加注意，本身也還是小菜鳥還在學習的路上，未來有其他關於 Author 的心得也會一併更新在這篇文章中～

感謝您的收看，下一篇預計會寫 Reviwer 需要著要的重點整理筆記。


# Reference 
- https://google.github.io/eng-practices/
- https://dev.to/saymy__name__/git-workflow-for-periodic-jenkins-builds-801
- https://medium.com/@ryanyang1221/%E8%AE%93-google-%E6%95%99%E4%BD%A0-code-review-be251d4d81b4


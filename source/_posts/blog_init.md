---
title: ' 部落格的誕生'
author: Mike Tsai
tags:
  - blog
  - django
  - python
  - gcp
  - gae
  - google cloud platform
  - google app engine
  - mysql
toc: true
categories: [Life]
keywords: Keywords, 部落格, Django, 當兵, 畢業, Yahoo, 新鮮人
# cover: "https://i.imgur.com/x84rxps.jpg"
# thumbnail: "https://i.imgur.com/x84rxps.jpg"
cover: gallery/cover/library.webp
thumbnail: gallery/cover/library.webp
date: 2019-10-31 17:22:00
---

## 退伍後的生活

回想起兩年前的今天，我還是個剛上研究所兩個月的碩一新生，而兩年後的今天我已從碩班畢業，並且完成兵役，說來實在非常幸運,我在論文口試日期都還有確定日期的情況下，便申請了提前入伍，而也如願在 7/18 入伍，並在 10/30 順利的結束兵役，真的非常感謝教授，而在當兵的這段期間其實我也一直在思考未來的方向。

退伍後距離答應公司到職日其實還有一個月左右的時間，於是就利用這個月的時間到新竹找女友，大約一週三天，每天的行程就是起床載她去上班然後在自己到圖書館唸書，雖然已經在工作的朋友都建議應該要出去玩的,因為上班後可以利用的自由時間會變得非常短，但想想之後短時間內應該沒有機會能跟女友一起住，所以就利用這一個月的時間體驗一下外宿生活，畢竟除了去年暑假到台中的實習在台中住了兩個月外從小到大我都是住家裡XD
<!-- more -->

![Imgur](https://i.imgur.com/x84rxps.jpg)
> 正式上班前的圖書館日常


<br/>


## 建立網站原因
當然讀書、刷題其實說不上枯燥乏味，雖然題目跟書中的內容都不同，但每天都一樣的生活其實還是蠻容易膩的，於是想起過去曾學過 django, css, html 等等，所以就決定利用空閒時間做個Blog 可以記錄一下生活點滴，過去大學時期記得班上有個女生作文很厲害並且常常看到她分享一些自己的文章，當初只覺得字好多，但現在回頭想想如果能用文字記錄生活何嘗不是一件壞事呢，畢竟有些事情不記錄下來可能時間久了就忘了~

## 網站部署環境
雖然現在有很多服務像是 WEEBLY, WORDPRESS 等等，都可以幫助使用者快速地建立一個網站，但是在眾多因素的考量下我還是決定自己從頭弄一個，也算是另類的side project !? 

最後也很慶幸自己能生在這樣的年代，因為網路的普及如果想要學習任何新知識都變得非常容易，網站的部署，後端伺服器，網域名稱註冊，等等都已經變得非常容易。網站後端不需要像過去自己用一台電腦，甚至連到 AWS, GCP 上面租用一台Server去做部署 都可以省掉，因為這樣還要去部署Server 作業的環境，而最終選用 Serverless 的架構，減少了維護成本與時間，利用 Google App Engine 來部署網站，因為過去學習的經驗曾經租過 Google 的 VM Instance 說實在話環境的設定真的蠻繁瑣的，而也在部署的當天購買了網域名稱 mikeTW.com，也因為這些方便的服務從開始做到實際上線只花了5天的時間，至於網站還有很多功能不完整會在未來慢慢的補齊，但至少已經可以開始寫一點生活的大小事了～









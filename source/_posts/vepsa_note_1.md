---
title: Vespa ai 筆記 (一)
author: Mike Tsai
tags:
  - Vespa
  - Yahoo
  - Opensource
  - Search engine
  - Real time
  - Java
toc: true
cover: >-
  https://image.slidesharecdn.com/vespa-190522070501/95/big-data-serving-the-last-frontier-processing-and-inference-at-scale-in-realtime-1-638.jpg?cb=1558508775
thumbnail: >-
  https://image.slidesharecdn.com/vespa-190522070501/95/big-data-serving-the-last-frontier-processing-and-inference-at-scale-in-realtime-1-638.jpg?cb=1558508775
categories: []
date: 2020-08-02 15:57:00
---

# Vespa ai 筆記 (一)
![](https://lh3.googleusercontent.com/NO5yMo6U2uvERXR9aqsAx39P8sSiFV85a5ocAPNYNPOM65vi1PoVG_RxIyiW9RJr3A7rrH-veZSzznSh2pabuG9k-2sAQvZQ4jwhmjRbrTxsXfKT9fFDljz_fADqaItjZa8hSOYhNlw=w1200)

## Vespa 是什麼
一般講到[vespa](https://vespa.ai/) 通常第一個聯想到的往往是某個機車品牌XD，然而除了機車品牌外它同時也是一個[開源](https://github.com/vespa-engine/vespa)的搜索引擎，Vespa 由 Yahoo! ( verizon media ) 於 2017年9月發布， Vespa 用於對海量數據集進行低延遲計算的引擎，它負責存儲和索引數據資料。同時 Vespa 中也提供了: Indexing, Searching, Ranking, Grouping，等等許多自定義的擴展功能。

來看看官方的描述：
![](https://lh3.googleusercontent.com/0AI2Cirz3tGEEGa-KmmbBUUNjtrtiN-GlRacGY6X4SRkzK6AcWXaz0jsMd_WleQrQAPw23tXf0jFiec7GqBv-WUUjQrq81ezZbhanYtAk16hn1LJvIOyT8dr7icliOAvJ9K87YwT_0M=w1200)

> 第一次看到是不是會有種不明覺厲的感覺XD

<!--more-->

而也因為這些特性我們常常利用vespa 來建立:
* 搜尋引擎 
* 個人化推薦系統
* 需要 Realtime 數據顯示的地圖，標籤，圖形...等等

而 Vespa 團隊因為近期因為 CORD-19 (新型冠壯肺炎)的快速傳染，利用Allen Institute for AI 所釋出的公開資料集，建立了新型冠壯病毒的搜尋[網站](https://cord19.vespa.ai/)，而該專案也是完全開源的[(點這裡查看)](https://github.com/vespa-engine/cord-19)。
<br>
## Vespa 的索引概念以及運作原理
Vespa 的主要架構圖如下![](https://lh3.googleusercontent.com/v67Jh-F8l98f3EzYZGmNUFfxlPQB-KiKrmoeVHTUgxxpvfQc0mPUQKGv6KuPRnkwZS-qaeB8KCiLqDlRonXsekIdgYB6TgjEap3Hids3WYU5m6gQiwAESSNKTYU433qoR662loy6LzQ=w1200)

主要可以分為三塊
1. Stateless Container Cluster
2. Content Cluster
3. Admin and config clusters


### Stateless Container Cluster 
為架構圖中藍色的部份，主要負責 Document 的 get, put, update, remove 等操作，當有外部的 request 打進來時，Container cluster 會自動將操作送到對應的 content node 中進行。自定義的排序方法、文件處理、其他功能也在此 cluster 中進行 。

### Content Cluster
相較於前者，Content Cluster 負責的業務則相對簡單，負責資料的儲存，會將同一份資料複製到多個節點上，以及執行從 Container Cluster 所要求的操作，當所有 Cluster 中對應的節點執行完操作後，content Cluster 會自動匯總結果。

而該 cluster 會自動平衡節點中的數據量，並且維持 Redundancy 已提高容錯性，針對壞掉的節點自動進行故障轉移，保證高可用行並自動恢復。

### Admin and config clusters
除了上述兩種外還有第三種主要負責一些節點設定等等。

<br>


## 利用 Vespa 動手實做一個簡單的搜尋引擎吧！！

### 介紹
利用 WorldPress 的資料集建立一個部落格文章推薦系統，實做用戶文章搜尋，以及個人文章推薦的功能，而該文章由Vespa Team 所發布可以點這裡查看[原文](https://docs.vespa.ai/documentation/tutorials/blog-search.html)。

### Prerequisites
* [Docker](https://docs.docker.com/docker-for-mac/install/)
* [Git](https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-Git-%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8)
* OS : macOS or Linux(Ubuntu, CentOS .....)
* Architecture: x86_64
* Minimum 6GB memory dedicated to Docker (the default is 2GB on Macs) - 10G for monitoring section.

### Dataset 
[kaggle dataset ](https://www.kaggle.com/c/predict-wordpress-likes/data)

Post 的基本屬性
| Column  | Description  |
| ----------------- |:----------------------- |
| post_id     | unique numerical id identifying the blog post     |
| date_gmt     | 	string representing date of blog post creation in GMT format yyyy-mm-dd hh:mm:ss     |
| author     | 	unique numerical id identifying the author of the blog post |
| url     | 	blog post URL|
| title     | 	blog post title|
| blog     | 	unique numerical id identifying the blog that the blog post belongs to|
| tags     | 	array of strings representing the tags of the blog posts|
| content     | 	body text of the blog post, in html format|
| categories     | 	array of strings representing the categories the blog post was assigned to|

### Requirements 
> 在開始前必須要先建立環境，利用官方所提供的 docker image 可以快速的把環境建好～



建立 & 切換 工作目錄 
```
$ mkdir blog
$ cd blog
```
建立 Docker 環境 
```
$ docker run -m 10G --detach --name vespa --hostname vespa-tutorial \
    --privileged --volume `pwd`:/app \
    --publish 8080:8080 --publish 19092:19092 vespaengine/vespa
```
若上述步驟遇到 docker memory limit 解法參考 [link](https://blog.csdn.net/CSDN_duomaomao/article/details/78567859)


確認 server 建立成功，會得到 200 OK 的 response 
```
$ docker exec vespa bash -c 'curl -s --head http://localhost:19071/ApplicationStatus'
```
Clone Git Repo ，會利用當中的 script 產生 data
```
$ git clone --depth 1 https://github.com/vespa-engine/sample-apps.git
```

<br>


下載Feeding 時所需的資料[點這裡](https://www.kaggle.com/c/predict-wordpress-likes/download/q5iqpPaOzadMgmYFEGmv%2Fversions%2Fp5evQDmqvlDqpq9UwsGL%2Ffiles%2FtrainPosts.zip)

<br>


至此恭喜您已經完成所有的環境建立步驟~ 

<br>



### 加入設定檔
> 加入必要的設定檔

在剛剛空的資料夾中建立對應資料夾 application
```
$ mkdir application
```

在 application 目錄中建立 services.xml，用來定義需要多少 server 的基本配置。

```
<?xml version='1.0' encoding='UTF-8'?>
<services version="1.0">

  <container id="default" version="1.0">
    <search></search>
    <document-api></document-api>
    <nodes>
      <node hostalias="node1"></node>
    </nodes>
  </container>

  <content id="blog_post" version="1.0">
    <redundancy>1</redundancy>
    <search>
      <visibility-delay>1.0</visibility-delay>
    </search>
    <documents>
      <document mode="index" type="blog_post"></document>
    </documents>
    <nodes>
      <node hostalias="node1" distribution-key="0"></node>
    </nodes>
    <engine>
      <proton>
        <searchable-copies>1</searchable-copies>
      </proton>
    </engine>
  </content>

</services>
```
* <container> 用以定義上述架構圖中的 container cluster 
* <search> 設定 query endpoint ， 預設為 8080 port
* <document-api> 設定 Feeding 文件的 endpoint
* <nodes> 設定該 cluster 中需要多少節點
* <content> 設定 content cluster 
* <redundancy> 設定需要多少份複製文件以供節點錯誤時進行自動回復
* <documents> 指定 node 中的 document schema (sd 檔)
* <nodes> 設定 cluster 中的 node

<br>

在 application 目錄中建立 hosts.xml，由於我們使用docker 在 local host 建立，只需要定義為如下即可。

```
<?xml version="1.0" encoding="utf-8" ?>
<hosts>
  <host name="localhost">
    <alias>node1</alias>
  </host>
</hosts>
```

<br>

建立 application 目錄中建立 blog 要被搜尋的文件的 blog_post.sd ， 路徑 application/schemas/blog_post.sd

```
schema blog_post {
    document blog_post {
        field date_gmt type string {
            indexing: summary
        }
        field language type string {
            indexing: summary
        }
        field author type string {
            indexing: summary
        }
        field url type string {
            indexing: summary
        }
        field title type string {
            indexing: summary | index
        }
        field blog type string {
            indexing: summary
        }
        field post_id type string {
            indexing: summary
        }
        field tags type array<string> {
            indexing: summary
        }
        field blogname type string {
            indexing: summary
        }
        field content type string {
            indexing: summary | index
        }
        field categories type array<string> {
            indexing: summary
        }
        field date type int {
            indexing: summary | attribute
        }
    }
    fieldset default {
        fields: title, content
    }
    rank-profile post inherits default {
        first-phase {
            expression:nativeRank(title, content)
        }
    }
}
```
當中 indexing 設定了vespa 會如何 indexing 該欄位
* index : 對該欄位界建立 index 供搜尋時使用
* attribute : 會將該欄位存在 memory 中，供排序、搜尋、合併時使用
* summary : 定義使否出現在 summary 中，搜尋的結果是否會將該欄位顯示


建立完成後application 目錄下應該會長這樣 

![image alt](https://lh3.googleusercontent.com/uGzvw8JZDXFTnIQ5it7oUFiFrSwqBhwS0xL-MzSVM_hIEBdXJaAaAaxMSzJ51Tc8drbym5QAgtyY7ztK_yswYQ_8xTtvbNOl_yoJMJZkvwsvyLJjn2e0EAx3yu-zu0xI4D1bJTlbvQI=w1200)



### 部屬應用到本機端
```
$ docker exec vespa bash -c '/opt/vespa/bin/vespa-deploy prepare /app/application && \
    /opt/vespa/bin/vespa-deploy activate'
```

接著去打 http://localhost:8080/ApplicationStatus 就能看到一些基本資訊，說明應用已經成功部屬。

### Feeding Data 
> 接著我們將必要的資料 Feeding 到搜尋引擎中。

將剛剛下載的[文檔](https://www.kaggle.com/c/predict-wordpress-likes/download/q5iqpPaOzadMgmYFEGmv%2Fversions%2Fp5evQDmqvlDqpq9UwsGL%2Ffiles%2FtrainPosts.zip)解壓縮

擷取前10000 筆資料(也可以跳過這步驟使用整個dataset XD) ，並利用script 轉成 對應的 JSON 格式，以降低處理時間。

```
$ head -10000 trainPosts.json > trainPostsSmall.json
$ python sample-apps/blog-tutorial-shared/src/python/parse.py trainPostsSmall.json > tutorial_feed.json
```

利用 Vespa Team 提供的 JAVA Feeding API 將資料打進 Vespa 搜尋引擎中

```
$ docker exec vespa bash -c 'java -jar /opt/vespa/lib/jars/vespa-http-client-jar-with-dependencies.jar \
    --verbose --file /app/tutorial_feed.json --host localhost --port 8080'
```

利用 Metrics API 確認 feeding 結果，若 Feeding 成功則會看見對應的 feeding 筆數。
```
$ curl -s "http://localhost:19092/metrics/v1/values" | tr "," "\n" | grep content.proton.documentdb.documents.active
```

現在我們可以用對應的 Doc ID 去要資料。
```
$ curl -s 'http://localhost:8080/document/v1/blog-search/blog_post/docid/507823' | json_pp
```

### Query 
> 用自訂的 query 去搜尋引擎拉東西

通常 vespa 利用 HTTP GET, HTTP POST 的 request 會長得像下面格式。
```
<host:port>/<search>?<yql=value1>&<param2=value2>...
```

我們可以用以下兩種形式的Query 去要資料，而使用的為[YQL](https://docs.vespa.ai/documentation/query-language.html) 的Query 語法 。

```
curl -s -H "Content-Type: application/json" --data '{"yql" : "select * from sources * where default contains \"music\";"}' \
http://localhost:8080/search/ | python -m json.tool
```

```
$ curl -s 'http://localhost:8080/search/?yql=select+*+from+sources+*+where+default+contains+%22music%22%3B' | python -m json.tool
```

以上兩種都是利用搜尋 trump 出現在 default 欄位中的 item， 而這邊的 defaut 指的是我們在 sd 中所建立的 field set : default，當中包含了 title, content 兩個欄位，因此會對這兩個欄位進行 filter。


### 自定義排序功能
> Relevance and Ranking，我們可以藉由自定義排功能，根據不同欄位計算相對應的權重，計算文章的相關性，用以實現自己想要的排序結果。

首先我們在先前定義好的SD 檔中新增 popularity 欄位，以及新的排序公式

```
field popularity type double {
    indexing: summary | attribute
}
```
```
rank-profile post_popularity inherits default {
    first-phase {
        expression: nativeRank(title, content) + 10 * if(isNan(attribute(popularity)), 0, attribute(popularity))
    }
}
```

我們新增了一條公式，繼承原本的rank-profile，並且覆寫掉第一階段的排序，將原本計算的分數加上 10 * popularity 欄位的值作為新的排序依據。

將新的應用部屬
```
$ docker exec vespa bash -c '/opt/vespa/bin/vespa-deploy prepare /app/application && \
    /opt/vespa/bin/vespa-deploy activate'
```

Feeding 含有popularity 的文件
```
$ python sample-apps/blog-tutorial-shared/src/python/parse.py \
    -p sample-apps/blog-tutorial-shared/sample_posts.json > tutorial_feed_with_popularity.json

$ docker exec vespa bash -c 'java -jar /opt/vespa/lib/jars/vespa-http-client-jar-with-dependencies.jar \
    --verbose --file /app/tutorial_feed_with_popularity.json --host localhost --port 8080'
```

完成後我們再進行 curl ，比較新舊query profile 的差異

原本的返回結果
```
curl -s -H "Content-Type: application/json" --data '{"yql" : "select title, content, popularity from sources * where default contains \"music\";"}' http://localhost:8080/search/ | json_pp
```

使用新的popularity rank profile 的結果 
```
curl -s -H "Content-Type: application/json" --data '{"yql" : "select * from sources * where default contains \"music\";", "ranking" : "post_popularity"}' \
http://localhost:8080/search/ | json_pp
```


我們可以發現套用了post_popularity 的 rank-profile 排序變成給予popularity 的 item 較高排序權重，即便 content 跟 title 中都沒有出現相對應的搜尋文字。
![](https://lh3.googleusercontent.com/Ol766J2Mj5t_PwIUVqgqlWIhp_F1KxkMzKe_uAjnnic7l40x3bapyy8xR2NyLE2Fs0GaHpj8zrTYjB7PjNGaPArStUpNbePqgmzXS_gQqRwPEZnMZNeJD1AaIc50WWcZWko_yTv9nd8=w1200)
> 左:default rank profile  右:使用popularity rank profile


至此我們已經完成了
* 環境搭建
* Vespa 引擎設定
* 部屬應用
* Feeding 資料
* 利用 YQL 進行簡單的搜尋
* 自訂義排序


下篇文章會繼續實做個人化的推薦系統~


<br>

## 結論
沒意外的話應該會將剩餘的內容切分到下幾篇文章 XD，本身對 Vespa 的用法也只是摸到皮毛，當中內部許多功能的實現方法也還沒有深入的研究，一樣還在持續的學習中，若文章中有錯誤的地方希望能鞭小力點XD，現今開源引擎較廣為人知的是 Elasticsearch, SOLR ， 然而 Vespa 的出現也提供了開發者一個新的選擇 ~ 

## References
* https://vespa.ai/
* https://cord19.vespa.ai/
* https://towardsdatascience.com/vespa-ai-and-the-cord-19-public-api-a714b942172f















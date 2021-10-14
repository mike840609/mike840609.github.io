title: 解除 Mega 單日流量限制
author: Mike Tsai
toc: true
tags:
  - Java
  - Mega
  - Limit
  - Downloader
  - Tool
  - Api
  - Hack
categories: []
cover: 'gallery/mega.jpeg'
thumbnail: 'gallery/mega.jpeg'
date: 2021-10-13 17:11:00
---
# 解除 Mega 流量限制 (2021/04)

## 問題描述
Mega 每日有 5GB 流量限制，若要下載更大的檔案則需要付費升級。

## 針對大檔案下載解法
若要下載超過 5 GB 檔案可以使用以下方式完成下載

1. 等待 6 小時冷卻時間  (免費, 耗時間)
2. 升級付費會員 (付費)
3. 透過 proxy 繞過 下載限制 (免費)

本篇文章會針對第三種方式進行大檔案下載，
並使用國外大大所開源的專案 `megabasterd` 進行 Proxy 設定, 透過幾步驟簡單設定即可繞過檔案限制。

<!-- more -->

## Megabasterd 使用方式
### 安裝環境  (若電腦有安裝過可以跳過該步驟)
由於作者是使用 java 刻的，所以必須安裝此環境程式可以順利跑起來～
下載網址: https://java.com/zh-TW/

### 下載主程式 
下載網址: https://github.com/tonikelope/megabasterd/releases/tag/v7.40
這邊可以看到多種版本, 請下載 .jar 檔結尾的 (25.1MB 那個)
![](https://i.imgur.com/UCCa8Sp.png)


### 設定 API Key
運行主程式
```
# 切換到主程式所在路徑 這邊假設放在桌面下
$ cd ~/Desktop

# 運行主程式
$ java -jar test.jar 
```
這時應該會跳出請您設定 api key 的界面
![](https://i.imgur.com/AMZVzdQ.jpg)

這邊可以隨便打只要把隨機產生的 App key 記下來即可
![](https://i.imgur.com/0yY0eB9.png)

這時回到主程式設定對應的 App key,
Edit -> Settings -> Advanced key -> Mega api key -> 填入剛剛產出的 key
![](https://i.imgur.com/RRsuqHG.png)

### 設定 proxy 
* https://us-proxy.org/
* http://free-proxy.cz/en/proxylist/country/TW/all/ping/all

透過上方網址可以拿到許多可以用的 proxy。

EDIT -> Settings 往下拉可以看到 smart proxy,
勾選 Use SmartProxy, 
並將上面得到的proxy 網址按照 IP:Port 格式填入即可。
![](https://i.imgur.com/63IzFSA.png)


### Let's Dance, Baby
終於完成所有設置，之後下載檔案只須執行 Let's Dance, Baby 這步驟即可XD

點擊 File -> New Download -> 填入需要下載的 mega 檔案網址 -> 按下 Let's dance, baby XD

![](https://i.imgur.com/p6FUIqk.png)

可以看到即使是大於 5GB 檔案也能完成下載
![](https://i.imgur.com/cIvUbYl.png)


感謝收看～


## References
- https://github.com/tonikelope/megabasterd
- https://us-proxy.org/


---
title: 解題常用排序演算法 (附上動圖)
author: Mike Tsai
toc: true
tags:
  - Leetcode
  - Sort
  - Algorithm
categories: []
date: 2019-11-20 15:44:00
keywords: Keywords, sort, sorting, 演算法, Algorithms, 筆記, Note
cover: >-
    https://cdn-ssl-devio-img.classmethod.jp/wp-content/uploads/2021/09/sorting-960x540.jpeg
thumbnail: >-
    https://cdn-ssl-devio-img.classmethod.jp/wp-content/uploads/2021/09/sorting-960x540.jpeg
---
>排序演算法是許多題目的基礎概念，解題時有許多技巧也是由排序演算法所衍生，使用 python3 實作，並且附上網路的動態圖片。

## 簡單排序 - O( N^2 )
---
### Bubble Sort

```python=1
# 兩兩相比, 將大的放到後面， 每一回合會把一個key 放到正確位置(最後方的key)
def bubble_sort(nums):
    l = len(nums)
    for i in range(l):
        for j in range(i-1):
            if nums[i] < nums[j]:
                nums[i] , nums[j] = nums[j], nums[i]
```

<!--more-->

GIF
![link text](https://thepracticaldev.s3.amazonaws.com/i/m4zwhvxf6ujdrvt9xoq5.gif)
> 圖片來源： https://wangonya.com/blog/js-sort-1/


---
### Insertion Sort

```python class:'lineNo'
# 從 idx 0 開始一路往下走，並每輪把當前 pivot 插入先前已排序的數組中的正確位置
def insert_sort(nums):
    for i in range(len(nums)):
        pos, cur = i, nums[i]
        while pos > 0 and nums[pos-1] > cur:
            nums[pos] = nums[pos-1]  # move one-step forward
            pos -= 1
        nums[pos] = cur
```
GIF
![](https://thepracticaldev.s3.amazonaws.com/i/g01s69r1ppo9kifien2v.gif)
> 圖片來源 : https://dev.to/wangonya/sorting-algorithms-with-javascript-part-1-4aca
---

### Selection Sort

```python=1
# 每次當前回合最小的和最左邊未排序的數字(index: i)交換
def selection_sort(nums):    
    for i in range(len(nums)):
        pivot = i         
        for j in range(i+1,len(nums)):
            if nums[j] < nums[pivot]:
                pivot = j
                
        nums[i-1],nums[pivot] = nums[pivot] , nums[i-1]
```
GIF
![](https://codepumpkin.com/wp-content/uploads/2017/10/SelectionSort_Avg_case.gif)
> 圖片來源 : https://codepumpkin.com/selection-sort-algorithms/


<br/>
 

## 高等排序 - O( NLogN )
---
### Merge Sort
```python=1
# divide and conqure 技巧, 每次把串列對半切，並且串列長度<=1 時,開始 merge
def merge_sort(nums):
    if len(nums) <= 1 : return nums
    m = len(nums)//2
    l = merge_sort(nums[:m])
    r = merge_sort(nums[m:])
    
    res = []
    while l and r :
        if l[0] < r[0]:
            res.append(l.pop(0))
        else:
            res.append(r.pop(0))
    res += l or r 
    return res

```
GIF
![](https://codepumpkin.com/wp-content/uploads/2017/10/MergeSort_Avg_case.gif)
> 圖片來源 : https://codepumpkin.com/selection-sort-algorithms/

### Quick Sort
```python=1
# Lomuto Version 
# 每一 run 將第最後一個元素當比較值 pivot, 
# 用 idx 紀錄pivot 應該放的位置
# 並且依序 <= pivot 的放右邊, > pivot 的放左邊
def quick_sort(nums):
    if len(nums) <= 1:
        return nums
    
    idx = 0
    pivot = nums[-1]
    
    for i in range(len(nums)-1):
        if nums[i] <= pivot :            
            nums[i] , nums[idx] = nums[idx] , nums[i]
            idx += 1
            
    nums[idx] , nums[-1] = nums[-1] ,nums[idx]
    
    l = quick_sort(nums[:idx])
    r = quick_sort(nums[idx+1:])
    return l + [nums[idx]] + r
```
GIF
![](https://www.codesdope.com/staticroot/images/algorithm/quicksort.gif)
> 圖片來源 : https://www.codesdope.com/course/algorithms-quicksort/

---

Merge sort 以及 Quick sort 部份為了簡潔所以把 divide, conquer 兩部份寫在一起, 而quick sort 用的是Lomuto 的版本(私心認為比較好理解XD),Hoare 的版本可以參考[這裡](https://en.wikipedia.org/wiki/Quicksort) ,謝謝收看(ﾉ>ω<)ﾉ ～～
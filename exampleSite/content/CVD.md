---
title: "使用 Cividis 色盤繪圖"
date: 2019-10-29T10:07:47+06:00
draft: false

# post thumb
image: "images/default.jpg"

# meta description
description: "this is meta description"

# taxonomies
categories:
  - "Tutorial"
tags:
  - "Data"
  - "Visualization"
  - "Python"

# post type
type: "post"
---
科學繪圖過程中色調的選用若不夠謹慎，很有可能會造成誤導的結果，甚至影響有色覺辨認障礙 (Color vision deficiency, CVD) 的人知的權益，因此選用 Cividis 這個色盤也是一種對知識的尊重ＸＤ

---
### 前言

去年夏天看到[這篇文章](https://doi.org/10.1371/journal.pone.0199239)，強調科學繪圖過程中色調的選用若不夠謹慎，很有可能會造成誤導的結果，甚至影響有色覺辨認障礙 (Color vision deficiency, CVD) 的人知的權益，因此他們開發了一個python 套件 cmaputil 用以產生 CVD 最佳化的色盤。

![https://res.cloudinary.com/rna-sick/image/upload/v1557417950/CVD/1_xqf4zv.png](https://res.cloudinary.com/rna-sick/image/upload/v1557417950/CVD/1_xqf4zv.png)

愛拖延如我，一直到這週氣溫降到二十度以下了才下載了套件想要試用看看，這才發現他的運作方式好複雜。似乎因為他原本的應用場景主要是替資料上色，所以有一套模擬 CVD 與顏色轉換的過程，過程基本上完全看不懂。

![https://res.cloudinary.com/rna-sick/image/upload/v1557417949/CVD/2_a1ykhh.png](https://res.cloudinary.com/rna-sick/image/upload/v1557417949/CVD/2_a1ykhh.png)

### 套件修改以供 python 3 使用

雖然如此，單純用個套件應該不會很難吧，沒想到剛裝完還是不能用，因為原本是寫給 python 2.7 用的，有兩個地方要自己去修改成 python 3 的 print 語法。而且他的文件跟一般的套件比起來比較簡陋，網路上討論也不多，所以老實說完全不知道怎麼用，我只是想要畫個簡單的熱圖而已啊ＱＱ～

![https://res.cloudinary.com/rna-sick/image/upload/v1557417948/CVD/3_t5jhlb.png](https://res.cloudinary.com/rna-sick/image/upload/v1557417948/CVD/3_t5jhlb.png)

### 下載色調值客製化 seaborn/matplotlib 色盤

在他們的 [github](https://github.com/pnnl/cmaputil) 上翻著翻著找到了附上的[色調值](https://github.com/pnnl/cmaputil/blob/master/colormaps/cividisHexValues.txt)，便有了下列的簡單解法：

1. 先下載[色調值](https://github.com/pnnl/cmaputil/blob/master/colormaps/cividisHexValues.txt)並另存成 CVD.txt
2. 讀取檔案載入成 matplotlib 的 cmap

    ```
    with open('CVD.txt') as f:colors = f.readlines()colors = [j[:-1] for j in colors]cmap = matplotlib.colors.ListedColormap(colors)
    ```

3. 繪圖時把自己客製化的 cmap 傳入就好囉

    ```
    sns.clustermap(dataFrame, cmap=cmap)
    ```

以上就是使用 python 三步驟輕鬆畫幅 CVD 友善的圖～

![https://res.cloudinary.com/rna-sick/image/upload/v1557417947/CVD/eg_ojwvz8.png](https://res.cloudinary.com/rna-sick/image/upload/v1557417947/CVD/eg_ojwvz8.png)

雖然顏色看起來有點黯淡，但是想到背後的意義就覺得有股

> 『啊～我又堅持了沒什麼人會在意的細節了呢～真是讚讚！』

的感覺～嘻嘻

---
layout: post
title:  "去交錯(De-interlacing), 以Motion Adaptive De-interlacing為例"
categories: Software Technical Note
---

> 去交錯(de-interlacing)的定義:

```一個將交錯式(interlace)影像轉為漸進式(progressive)影像輸出的程序。```

&nbsp;

Interlace的影像源可以是一般的攝影機, DVD或者1080i 的藍光碟(blu-ray disc),在這裡就不解釋interlace與progressive的定義了, 而因為interlace(2*n)影像的資訊含量為progressive(2n)的一半, 硬體速度與buffer大小就相較可以降低須求(如陰極射線管顯示器(Cathode Ray Tube, CRT)) 。


odd field+even field成為 one frame 如圖下：

![2field1frame](/assets/images/2field1frame.jpg)

&nbsp;

> 去交錯(de-interlacing)的原因:

```現今的顯示器(monitor)設備已有足夠的能力即時處理漸進式(progressive)影像, 雖然現在很多影音公司會先在販售前將錄好的interlace影像轉為progressive,但對於單純interlace影像, 這些monitor直接撥放的話會有閃爍(flicker)的現象, 因此必須擁有de-interlacing的能力才行。```

簡單來說, 你將會看到影像一直在發抖…哈  
&nbsp;

![hemib_a](/assets/images/hemib_a.png)
        (訊源HDMI 1080i) 左: BEFORE 右: AFTER 

&nbsp;

但是, 永遠不能非常完美的 de-interlacing…..
舉例來說, 一台每秒50場(field per sec)的攝影機, 第一行跟第三行在第1/50秒被拍攝, 就是奇數在1/50, 偶數在2/50秒, 他是有時間差距的(2/50–1/50)兩field被合為frame時, 如果物體是動態的, 你將會看到有鋸齒的效果。
&nbsp;

> 去交錯(de-interlacing)的時機:

 + NTSC, PAL, SECAM 類比廣播系統
 + HDMI (480i/576i/1080i), DTV(480i/576i/480i/1080i), YPbPr (480i/576i/480i/1080i), etc. 就是那些interlace 訊號源

&nbsp;

De-interlacing 的演算法很多, 這裡以MADi為例:
> MADi ( Motion Adaptive De-interlacing)

```結合Intra-field 與 Inter-field 的優點來實現的演算法，利用 field 之間的像素差來判斷動態區域與靜態區域，動態區域用 Intra-field de-interlacing，靜態區域使用 inter-field de-interlacing。```

&nbsp;
介紹一下Intra-field de-interlacing 跟 Inter-field de-interlacing的定義:

&nbsp;
> Intra-field de-interlacing

```單一場去交錯, 適用於動態畫面, 基於spatial filtering (2D),將一個field 放大成一個frame大小, 雖然硬體的成本因此降低, 但用在靜態畫面看起來鬆散, 如果動態影像有橫向的細線, 畫面看起來就會閃爍。```

&nbsp;

## _**那為什麼放大會閃爍(flickering)?**_


![intra_fiel_deinterlacing_bob](/assets/images/intra_fiel_deinterlacing_bob.png)
        [Intra-field deinterlacing (Bob)](https://www.slideshare.net/ramesh130/de-interlacing-techniques-wid-ref)


左圖為intra-field的其中一種演算法, 叫做Bob, 假設現在是even field(紅色部分), 而黑色部分的空缺則由上一條複製下來，而右圖假設有在odd field有一條黑色細線, 但由於我們是用even field作複製的動作, 導致odd field才有的黑色細線不見了, 因此合成一個frame時會看到閃爍的現象。

&nbsp;
> Inter-field de-interlacing

```場間去交錯, 適用於靜態畫面, 基於temporal filtering (1D), 將連續兩個field結合為一個frame, 在垂直方向保留全部分辨率, 用在動態畫面則可以能有鬼影或鋸齒。```

&nbsp;

## 然後再來張MADi 的示意圖:

![MADi示意圖](/assets/images/madi.png)
        MADi 示意圖

&nbsp;

MADi 翻成中文就是動態自適應去交錯, 藉由偵測影像的靜態與動態, 希望能夠做到高分辨率與無閃爍,
因此在Motion Detect 的步驟必須精確(很重要的意思), 否則會產生較多的artifacts。
圖中的3DDi的3D參考了空間(2D, intra-field)+時間(1D, inter-field)保留了最多資訊, 代價是需要額外的記憶體空間。

Motion Detect會透過觀察pixel的值在兩個以上的field是如何的motion, 藉以分配利用在inter-field或者intra-field, 
通常會設個門閥值(threshold), 如果pixel 大於threshold則判斷使用intra-field de-interlacing。

```F_i (x ⃗,n)=αF_st (x ⃗,n)+(1-α) F_mot (x ⃗,n)```

---

F_st是靜態影像的內差結果, F_mot是動態影像的內差結果, α是權重。

---

關於de-interlacing還有其他的東西需要注意, 比如Erode(侵蝕)/Dilate(擴張), 
是屬於Morphology形態學的範疇, 
在影像二值化後為了凸顯影像的feature, 如連通區域與邊界,去做消除雜訊的動作。

或者是利用邊界導向(Edge-Oriented)的去交錯方式, 這是屬於2D的去交錯, 
主要是為了解決intra-field de-interlacing的問題 (jagged effect in the oblique edge)。

以及在電視系統上如果要撥放電影也必須去交錯, 那又是另外一回事了。(Hint: Pull-down) 😛
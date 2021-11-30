---
layout: post
title:  "USB Protocol Layer (協定層)"
categories: Software Technical Note
---

通常包含三個packet: Token packet, Data packet, Status packet (Handshake), 依據傳輸的型態決定要包含一個兩個三個packet。 

ps: packet是usb傳輸的最小單位 

&nbsp;&nbsp;&nbsp;
![USB Transaction](/assets/images/usb_transaction.png)
*USB Transaction*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

資料傳輸時，由Token packet中決定要從Host往Device，或從Device往Host。Handshake可以判斷此次傳輸是否成功(ACK, NAK, STALL)。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

以在USB 3.0為例，協定層 (Protocol layer)將來自上層的功能層 (Functional layer)的請求(request)轉換成資料傳輸(Transaction)，並管理host與device端對端的資料流程，如：

> 端對端資料傳輸封包的可靠性、有效率地利用頻寬、有效率地電源管理  


![USB Transaction](/assets/images/usb_trascation_2.jpg)
pic: [source is here](http://www.techdesignforums.com/practice/files/2013/09/USB-University-diag-4-lrg.jpg*) 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

### Reference
  1. [成大資工Wiki 標準 USB 2.0 介面 實體層](http://wiki.csie.ncku.edu.tw/embedded/USB#實體層)
  2. [USB 3.0 protocol layer – part 1](http://www.techdesignforums.com/practice/technique/usb-3-0-protocol-layer-1)
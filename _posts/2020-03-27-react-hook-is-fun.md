---
layout: post
title: Đào sâu vào React Hooks
date: 2020-03-27 13:32:20 +0300
description: 
img: hooklove.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ReactJS]
---

Xin chào các bạn, Series này không hướng cacds bạn đến việc sử dụng React Hooks như thế nào.  

Mở đầu cho series này sẽ là đào sâu về việc Re-render khi bạn dùng React-Hook. 

## Re-Render Master
Trong thực tế nói chúng, chúng ta cũng biết rằng khi code React thì việc gặp phải các vấn đề về hiệu năng luôn là những vấn đề mà một lập trình viên cần phải chú ý. Còn khi sử dụng React Hook nói riêng, chúng ta cũng cần nên biết những vấn đề về hiệu năng đó là đến từ đâu.
Một trong những issue nổi cộm nhất khi sử dụng React đó là việc render các component không cần thiết.

Hãy xem ví dụ dưới đây nhé

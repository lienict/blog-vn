---
layout: post
title: Đào sâu vào React Hooks
date: 2020-03-27 13:32:20 +0300
description: 
img: hooklove.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ReactJS]
---

Xin chào các bạn, Series này không hướng các bạn đến việc sử dụng React Hooks như thế nào.  

Mở đầu cho series này sẽ là đào sâu về việc Re-render khi bạn dùng React-Hook. 

## Re-Render Master
Trong thực tế nói chúng, chúng ta cũng biết rằng khi code React thì việc gặp phải các vấn đề về hiệu năng luôn là những vấn đề mà một lập trình viên cần phải chú ý. Khi đó, chúng ta cũng cần nên biết những vấn đề về hiệu năng đó là đến từ đâu. 
Một trong những issue nổi cộm nhất khi sử dụng React đó là việc render các component không cần thiết.

Hãy xem ví dụ dưới đây nhé :

{% highlight js %}
const Incrementor = () => {
  const [, setA] = useState(0);
  const [, setB] = useState(0);

  const incrementA = () => setA(a => a + 1);
  const incrementB = () => setB(a => a + 1);

  const incrementAB = () => {
    incrementA();
    incrementB();
  };

  const incrementABLater = () => {
    setTimeout(() => {
      incrementA();
      incrementB();
    }, 1000);
  };

  console.log("Re-rendered");

  return (
    <div>
      <button onClick={incrementA}>a++</button>
      <button onClick={incrementB}>b++</button>
      <button onClick={incrementAB}>a++, b++</button>
      <button onClick={incrementABLater}>a++, b++ after 1s</button>
    </div>
  );
};
{% endhighlight %}

Component trên có 2 stage là **A** và **B**, và ở phần render chúng ta có 4 event để cộng giá trị của **A** và **B** lên 1 đơn vị.
Và bên trong component, mình có đặt dòng console.log để in ra rằng component này đã render bao nhiêu lần khi thao tác với các button.

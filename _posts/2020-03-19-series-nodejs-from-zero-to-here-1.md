---
layout: post
title: Node.js from zero to hero ##1
date: 2020-03-19 13:32:20 +0300
description: 
img: unnamed.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Node.js, Javascript]
---

Xin chào các bạn, đây là bài đầu tiên trong series "Node.js from zero to hero". 
Trong series này, mình sẽ đi từ cơ bản đến chuyên sâu các kiến thức và thực hành về Node.js. 
Mục đích của series này là giúp cho các bạn có kiến thức về Node.js và đảm bảo rằng các bạn có thể vận dụng nó để viết những ứng dụng sử dụng Node.js, phục vụ cho công việc của các bạn.
Các bạn cũng đừng lo lắng nếu các bạn đang ở vạch số 0.

Bài viết đầu tiên này ở mức độ cực kỳ basic, cực kỳ zero, nên bạn nào đã có kiến thức rồi có thể bỏ qua nhé!
Trong bài này các bạn sẽ hiểu được Node.js là gì, cách để install (cài đặt) nó và làm thế nào để bắt đầu với nó. Let's go!

## Node.js là gì nhỉ?
Túm lại thì có mấy khái niệm thế này nhé
  * Node.js là một open-source framework, miễn phí hoàn toàn
  * Node.js là một cross-platform runtime enviroment (có thể chạy trển các môi trường khác nhau như Window, Linux, Mac OS..) dùng cho phát triển server-side
  * Node.js là một Javascript runtime xây dựng trên [Chrome's V8 Javascript engine](https://en.wikipedia.org/wiki/V8_%28JavaScript_engine%29)
  * Node.js thực thi mã theo mô hình event-driven, non-blocking I/O, điều đó làm Node.js trở nên nhẹ và hiệu quả
  * Node.js sử dụng [libuv](https://github.com/libuv/libuv), là một thư viện hỗ trợ multi-platform trọng tâm hướng vào xử lý bất đồng bộ I/O.
  * Node.js là đơn luồng và chỉ sử dụng một core CPU duy nhất, nó cũng không tự động sử dụng nhiều hơn một core trong các máy chủ multi-core.

Node.js thực sự mạnh ở các ứng dụng cần tốc độ nhanh và cần tới khả năng mở rộng vì Node.js có khả năng xử lý một lượng rất lớn các request với tốc độ nhanh. Mình tin rằng Node.js là một trong những sự lựa chọn tốt nhất cho các ứng dụng real-time như là game online, chat rooms, hoặc là những ứng dụng nào đó mà một user (robot hoặc sensor..) có thể làm gì đó (xem thông tin tức thì, tương tác...) với những user khác mà không cần reload lại trang, hoặc các ứng dụng về Internet of Things, Single-Page Applications, Stream Apps, ứng dụng cần kiến trúc Microservices.

Node.js không phải là toàn năng để đánh đổ tất cả các nền tảng để viết back-end trước đó. Node.js chỉ phù hợp trong một số hoàn cảnh nhất định mà nó thích hợp. Bạn vẫn có thể dùng .NET, Laravel, Rails, Java hay Django... như thường. Mình chỉ nhấn mạnh là Node.js chỉ phù hợp trong hoàn cảnh là project của bạn cần dùng tới nó thôi. Có ý kiến cho rằng, Node.js không phù hợp với các ứng dụng mà cần thực thi tính toán nhiều và nặng như là việc xử lý ảnh hay là thao tác gì đó với BigData. Khi đó chúng ta cần đến những ngôn ngữ thích hợp khác như là CPP hay Java...

Tuy Node.js là đơn luồng, nhưng chúng ta vẫn có thể chạy mọi thứ song song (trong code bạn có thể dùng Promise.all nhé) bởi vì máy ảo hoặc là hệ điều hành đã run I/O song song cho chúng ta rồi. 

## Tại sao lại phải chọn Node.js?
  * Node.js thì cho phép các lập trình viên từ front-end chuyển sang back-end dễ dàng tiếp cận hơn vì cùng là Javascript với nhau. (Trước mình cũng toàn code .NET, front-end thì code jquery thuần).
  * Như đã nói thì Node.js là "tool" hoàn hảo cho những ứng dụng server-side có lưu lượng truy cập cao
  * Việc Scale với Node.js rất linh hoạt, nên nó có thể giúp bạn tiết kiệm được tiền vào việc chi tiêu cho cơ sở hạ tầng.
  * Vì là open-source (mã nguồn mở) nên là có sẵn rất nhiều các công cụ hỗ trợ, các module phù hợp. Bạn chỉ cần kéo chúng về và dùng ngay lập tức bằng cách dùng npm.
  

Tham khảo : 
 - [Getting Started With Node.js Tutorial](https://blog.risingstack.com/node-hero-tutorial-getting-started-with-node-js/)
 - [Node.js multithreading: What are Worker threads, and why do they matter?](https://blog.logrocket.com/node-js-multithreading-what-are-worker-threads-and-why-do-they-matter-48ab102f8b10/)

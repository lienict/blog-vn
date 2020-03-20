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
  * Node.js là một cross-platform runtime enviroment (có thể chạy trên các môi trường khác nhau như Window, Linux, Mac OS..) dùng cho phát triển server-side
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
  
## Install Node.js

Tại thời điểm viết bài này thì version hiện tại của Node.js là 12.16.1. Bạn nào đang dùng Node 8 thì update nhé vì từ năm 2020 Node 8 sẽ không được update nữa.

Việc cài đặt Node.js cũng rất đơn giản thôi. Vì là cross-platform (đa nền tảng) nên bạn có thể cài đặt nó ở các môi trường khác nhau như Window, Linux, Centos, MacOS... Trong phạm vi bài này, mình sẽ chỉ hướng dẫn các bạn cài đặt trên môi trường window. 

## Step 1: Download Node.js Installer
Bạn vào trang web này (https://nodejs.org/en/download/) và click vào **Window Installer** để download version mới nhất của NodeJS.
Trong Node.js installer thì đã bao gồm NPM package manager.

![Macbook](https://phoenixnap.com/kb/wp-content/uploads/2019/06/donwload-nodejs-installer-windows-1.png)

Sau khi download Node.js Installer về, bạn chỉ việc chạy nó next next để cài đặt.

## Step 2 : Kiểm tra cài đặt
Sau khi cài đặt thành công, bạn mở command prompt hoặc PowerShell ra, và kiểm tra node version và npm version bằng các câu lệnh sau.

* Dùng câu lệnh node -v để kiểm tra phiên bản Node.js
* Dùng câu lệnh npm -v để kiểm tra phiên bản npm

À đó, quên mất không nói về npm. **NPM** là viết tắt của Node package manager là công cụ tạo và quản lý các thư viện lập trình của Javascript nói chung và Node.js nói riêng. Các bạn cứ hình dung có cả nghìn thư viện được tạo ra, bạn thấy chúng phù hợp và muốn kéo về project của mình, thì npm sẽ giúp bạn kéo nó về bằng 1-2 câu command đơn giản. Trang chủ của nó đây nhé (https://www.npmjs.com/).
Bạn dùng các framework hay thư viện khác trong hệ sinh thái của Javascript (Reactjs, Vuejs..) thì cũng dùng npm nhé hoặc là [yarn](https://yarnpkg.com/)

## Hello World
Để bắt đầu, chúng ta hãy thử một ví dụ đơn giản nhất nhé. Đó là in ra dòng chữ "Hello World" trên console.
Mở command prompt hoặc PowerShell của các bạn và gõ **node* : 
{% highlight js %}
$ node
>
{% endhighlight %}

Okay, giờ chúng ta in ra dùng chữ "Hello World"
{% highlight js %}
$ node
> console.log('Hello World')
{% endhighlight %}

Ấn **Enter**, kết quả in ra sẽ như sau
{% highlight js %}
$ node
> console.log('Hello World')
Hello World
undefined
{% endhighlight %}

Dành cho bạn nào thắc mắc về console.log. **Console.log** là một chức năng để viết các message ra console. Bạn nào code Front-end thì rất quen thuộc rồi, nó sẽ in thông tin mà bạn cần ra DevTools, rất hữu ích cho debug hoặc là in ra thông tin cần thiết. Tuy vậy dùng console.log trong Node.js không phải điều tốt cho performance, thậm chí bạn không nền dùng nó trong ứng dụng thực tế (mình sẽ giải thích trong các bài sau).

## Ví dụ thực tế với Modularization (module hóa)
Ok cùng nhảy vào ví dụ thực tế nhé, trong ví dụ này chúng ta sẽ tính tổng 1 dãy số và in nó ra console. 

Các bạn cần chuẩn bị những kiến thức sau: 
  * Các bạn cần một IDE cho riêng mình để code. Có thể đó là Visual Studio Code (VSC), Sublime, Webstorm, Atom... Mình đang dùng VSC
  * Nữa là cần trang bị kiến thức cơ bản về ES6 như var/let/const, ESModules,Arrow function và Template Literals (Tham khảo ở [đây](https://lienict.github.io/blog-vn/prepare-js-for-react/) nhé!).
  * Biết sử dụng một số hàm với array trong Javascript như reduce/map/find/filter (Tham khảo ở [đây](https://lienict.github.io/blog-vn/prepare-js-for-react/) nhé!).

Good luck!
Tham khảo : 
 - [Getting Started With Node.js Tutorial](https://blog.risingstack.com/node-hero-tutorial-getting-started-with-node-js/)
 - [Node.js multithreading: What are Worker threads, and why do they matter?](https://blog.logrocket.com/node-js-multithreading-what-are-worker-threads-and-why-do-they-matter-48ab102f8b10/)
 - [How to Install Node.js and NPM on Windows](https://phoenixnap.com/kb/install-node-js-npm-on-windows)

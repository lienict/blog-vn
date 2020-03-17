---
layout: post
title: Chuẩn bị những feature Javascript nào để code React?
date: 2020-03-12 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: how-to-start.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ReactJS, Javascript]
---

Không cần phải dài dòng nữa, ReactJS ngày nay gần như đã là thư viện phổ biến và mạnh mẽ nhất dành cho frontend rồi.
Từ ngày [React Hooks](https://reactjs.org/hooks) ra đời, cách code React đã trở nên đơn giản, dễ code hơn bao giờ hết. 
Thành thạo những features của JavaScript để áp dụng vào việc build một ứng dụng bằng React đã trở thành một việc 
vô cùng tất yếu rồi. Bài viết này sẽ liệt kê ra vài features JavaScript mà tôi khuyến khích các bạn dành thời gian
để thành thạo nó, từ đó làm cho việc xây dựng ứng dụng viết bằng JS (không chỉ là ReactJS) của các bạn trở nên 
hiệu quả hơn bao giờ hết.
Let's go! 

## Template Literals

Template literals là tên gọi của tính năng dành cho thao tác với string,được thêm vào trong phiên bản ES6. Với tính năng này, chúng ta có thể khai báo hoặc sử dụng multi-line string dễ dàng, bên cạnh đó có thể sử dụng biến, biểu thức, và thực hiện hàm bên trong 1 string và không cần phải thông qua phép cộng string cổ điển (khá tiện lợi đó nha!).

{% highlight js %}
const greeting = 'Hello'
const subject = 'World'
console.log(`${greeting} ${subject}!`) // Nó sẽ trả ra là Hello World
// Kết quả trả ra giống với cách viết cộng string này
console.log(greeting + ' ' + subject + '!')

// Trong React, ta có thể dùng nó để thêm class mà được định nghĩa từ trước như sau:
function Box({className, ...props}) {
  return <div className={`box ${className}`} {...props} />
}

// sử dụng để khai báo multi-line
const multi = `dong 1
dong 2
dong 3
`;

// thực hiện biểu thức trong string
console.log(`aaa ${true ? "true ne" : "false ne"}`) // nó sẽ in ra là 'aaa true ne'
{% endhighlight %}

[MDN: Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

## Shorthand property names

ES6 đã giới thiệu 2 tính năng mới giúp thao tác với object trở nên ngắn gọn hơn là Shorthand Properties và Shorthand Method Names.
Với Shorthand Properties, khi mà bạn muốn định nghĩa một object mà key của object lại trùng tên với tên biến tham chiếu tới property tương ứng được truyền vào, bạn có thể sử dụng Shorthand Properties để đơn giản hóa việc khai báo.
Với Shorthand Method Names, ta cũng có thể khai báo ngắn gọn 1 hàm khi hàm đó là property của 1 object.

Bạn có thể định nghĩa 1 object trong ES6/ES2015 syntax như sau
{% highlight js %}
const cat = 'Miaow'
const dog = 'Woof'
const bird = 'Peet Peet'
const someObject = {
  cat,
  dog,
  bird,
  save(){ // shorthand method name
  }
}

// kết quả nó sẽ giống với cách viết sau (cách viết theo chuẩn ES5 hoặc cũ hơn)
const someObject = {
  cat: cat, 
  dog: dog, 
  bird: bird,
  save : function(){
  }
}

// Trong React, ta có thể dụng ở nhiều chỗ khác nhau,ví dụ như đoạn custom hook này
function Counter({initialCount, step}) {
  const [count, setCount] = useCounter({initialCount, step})
  return <button onClick={setCount}>{count}</button>
}
{% endhighlight %}

[MDN: Object initializer _New notations in ECMAScript 2015_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)

## Arrow functions

Arrow functions cũng được gọi là "fat arrow" function - là một tính năng giúp chúng ta có thể khai báo function ngắn gọn hơn bằng cách sử dụng mũi tên `=>`. Cú pháp của nó giống với biểu thức Lambdas trong C# hoặc Python. Bằng cách sử dụng arrow functions, chúng ta tránh được việc phải viết `function` keyword và `return` keyword khi khai báo hàm (chúng đã được implicit), và thâm chí không cần dấu ngoặc nhọn.

{% highlight js %}
const getFive = () => 5
const addFive = a => a + 5
const divide = (a, b) => a / b

// tương tự như cách viết này:
function getFive() {
  return 5
}
function addFive(a) {
  return a + 5
}
function divide(a, b) {
  return a / b
}

// TRong React:
function TeddyBearList({teddyBears}) {
  return (
    <ul>
      {teddyBears.map(teddyBear => (
        <li key={teddyBear.id}>
          <span>{teddyBear.name}</span>
        </li>
      ))}
    </ul>
  )
}
{% endhighlight %}

[MDN: Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Destructuring

Destructuring là tính năng mà tôi thích nhất của Javascript. Tôi dùng chúng với object và array mọi lúc mọi nơi.

{% highlight js %}
// const obj = {x: 3.6, y: 7.8}
// makeCalculation(obj)

function makeCalculation({x, y: d, z = 4}) {
  return Math.floor((x + d + z) / 3)
}

// tương tự với cách viết này
function makeCalculation(obj) {
  const {x, y: d, z = 4} = obj
  return Math.floor((x + d + z) / 3)
}

// cũng tương tự với cách viết này
function makeCalculation(obj) {
  const x = obj.x
  const d = obj.y
  const z = obj.z === undefined ? 4 : obj.z
  return Math.floor((x + d + z) / 3)
}

// Trong React:
function UserGitHubImg({username = 'ghost', ...props}) {
  return <img src={`https://github.com/${username}.png`} {...props} />
}
{% endhighlight %}

[MDN: Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## Parameter defaults

Đây cũng là tính năng mà tôi luôn sử dụng. Nó là một cách rất đơn giản nhưng rất hữu dụng khi bạn muốn định nghĩa những giá trị mặc định cho function của bạn

{% highlight js %}
// add(1)
// add(1, 2)
function add(a, b = 0) {
  return a + b
}

// Tương tự với cách viết sử dụng arrow function này
const add = (a, b = 0) => a + b

// Cũng tương tự với cách viết cổ điển này
function add(a, b) {
  b = b === undefined ? 0 : b
  return a + b
}

// Trong React:
function useLocalStorageState({
  key,
  initialValue,
  serialize = v => v,
  deserialize = v => v,
}) {
  const [state, setState] = React.useState(
    () => deserialize(window.localStorage.getItem(key)) || initialValue,
  )

  const serializedState = serialize(state)
  React.useEffect(() => {
    window.localStorage.setItem(key, serializedState)
  }, [key, serializedState])

  return [state, setState]
}
{% endhighlight %}

[MDN: Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Rest/Spread

Toán tử `...` là một tính năng cực kỳ cool xì lầu của ES6. Chúng ta có thể sử dụng nó với 2 cách khác nhau đó là `Spread Operator` hoặc là `Rest parameter`

`Rest parameter` : Tức là nó sẽ trả ra mọi thứ còn lại vào trong một mảng hoặc object (ghi nhớ là còn lại nhé).

`Spread Operator` : Tính năng này cho phép bạn chuyển đổi một chuỗi/array/object thành nhiều argument (trong trường hợp gọi với hàm) hoặc là nhiều phần tử (cho array/object). Nói cách khác, nó cho phép chúng ta mở rộng một đối tượng. Với Rest Parameters chúng ta có thể lấy ra list của các tham số cho vào một mảng. Spread Operator cho phép chúng ta chia nhỏ đối tượng trong một mảng vào một biến nào đó.

{% highlight js %}
const arr = [5, 6, 8, 4, 9]
Math.max(...arr)
//Tương tự với
Math.max.apply(null, arr)

const obj1 = {
  a: 'a from obj1',
  b: 'b from obj1',
  c: 'c from obj1',
  d: {
    e: 'e from obj1',
    f: 'f from obj1',
  },
}
const obj2 = {
  b: 'b from obj2',
  c: 'c from obj2',
  d: {
    g: 'g from obj2',
    h: 'g from obj2',
  },
}
console.log({...obj1, ...obj2})
// Tương tự với
console.log(Object.assign({}, obj1, obj2))

function add(first, ...rest) {
  return rest.reduce((sum, next) => sum + next, first)
}
// cũng tương tự với
function add() {
  const first = arguments[0]
  const rest = Array.from(arguments).slice(1)
  return rest.reduce((sum, next) => sum + next, first)
}

// Trong React:
function Box({className, ...restOfTheProps}) {
  const defaultProps = {
    className: `box ${className}`,
    children: 'Empty box',
  }
  return <div {...defaultProps} {...restOfTheProps} />
}
{% endhighlight %}

[MDN: Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

[MDN: Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

## ESModules

ESModules hay còn gọi là JS modules, nó là một tính năng quan trọng mới của Javascript, trước đây phải chúng sử dụng CommonJS trong NodeJS hay AMD để có thể sử dụng tính năng này. Giờ thì ES6 cho phép chúng ta export và import các object, nhờ thế chúng ta có thể chia nhỏ chương trình ra thành các modules, mỗi modules có thể là một chức năng đặc biệt. 
Trong một module, bạn có thể sử dụng từ khóa `export` để export bất kỳ kiểu dữ liệu nào như biến, class, function. Đồng thời cũng sử dụng từ khóa import để import module từ file khác.

{% highlight js %}
export default function add(a, b) {
  return a + b
}

/*
 * import add from './add'
 * console.assert(add(3, 2) === 5)
 */

export const foo = 'bar'

/*
 * import {foo} from './foo'
 * console.assert(foo === 'bar')
 */

export function subtract(a, b) {
  return a - b
}

export const now = new Date()

/*
 * import {subtract, now} from './stuff'
 * console.assert(subtract(4, 2) === 2)
 * console.assert(now instanceof Date)
 */

// in React:
import React, {Suspense, Fragment} from 'react'
{% endhighlight %}

[MDN: import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

[MDN: export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

## Ternaries

Trong React, để làm với render có điều kiện, bạn có thể sử dụng nhiều cách như dùng if/else, switch hoặc là toán tử &&..

Về phía cá nhân thì tôi yêu thích ternaries nhất. Sử dụng Ternaries làm code JSX trở nên trong sáng hơn.

{% highlight js %}
const message = bottle.fullOfSoda
  ? 'The bottle has soda!'
  : 'The bottle may not have soda :-('

// is the same as
let message
if (bottle.fullOfSoda) {
  message = 'The bottle has soda!'
} else {
  message = 'The bottle may not have soda :-('
}

// in React:
function TeddyBearList({teddyBears}) {
  return (
    <React.Fragment>
      {teddyBears.length ? (
        <ul>
          {teddyBears.map(teddyBear => (
            <li key={teddyBear.id}>
              <span>{teddyBear.name}</span>
            </li>
          ))}
        </ul>
      ) : (
        <div>There are no teddy bears. The sadness.</div>
      )}
    </React.Fragment>
  )
}
{% endhighlight %}

[MDN: Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

## Array Methods

Javascript cung cấp rất nhiều phương thức để làm việc với array, dưới đây là những tính năng mà tôi dùng nhiều nhất

- find
- some
- every
- includes
- map
- filter
- reduce

Dưới đây là vài ví dụ

{% highlight js %}
const dogs = [
  {
    id: 'dog-1',
    name: 'Poodle',
    temperament: [
      'Intelligent',
      'Active',
      'Alert',
      'Faithful',
      'Trainable',
      'Instinctual',
    ],
  },
  {
    id: 'dog-2',
    name: 'Bernese Mountain Dog',
    temperament: ['Affectionate', 'Intelligent', 'Loyal', 'Faithful'],
  },
  {
    id: 'dog-3',
    name: 'Labrador Retriever',
    temperament: [
      'Intelligent',
      'Even Tempered',
      'Kind',
      'Agile',
      'Outgoing',
      'Trusting',
      'Gentle',
    ],
  },
]

dogs.find(dog => dog.name === 'Bernese Mountain Dog')
// {id: 'dog-2', name: 'Bernese Mountain Dog', ...etc}

dogs.some(dog => dog.temperament.includes('Aggressive'))
// false

dogs.some(dog => dog.temperament.includes('Trusting'))
// true

dogs.every(dog => dog.temperament.includes('Trusting'))
// false

dogs.every(dog => dog.temperament.includes('Intelligent'))
// true

dogs.map(dog => dog.name)
// ['Poodle', 'Bernese Mountain Dog', 'Labrador Retriever']

dogs.filter(dog => dog.temperament.includes('Faithful'))
// [{id: 'dog-1', ..etc}, {id: 'dog-2', ...etc}]

dogs.reduce((allTemperaments, dog) => {
  return [...allTemperaments, ...dog.temperaments]
}, [])
// [ 'Intelligent', 'Active', 'Alert', ...etc ]

// in React:
function RepositoryList({repositories, owner}) {
  return (
    <ul>
      {repositories
        .filter(repo => repo.owner === owner)
        .map(repo => (
          <li key={repo.id}>{repo.name}</li>
        ))}
    </ul>
  )
}
{% endhighlight %}

[MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

## Promises và async/await

Ừm, có thể cần phải có một bài viết riêng dành cho Promise và async/await. Đại khái thì thế này, Promise thì là một chủ đề khá lớn và nó làm các lập trình viên tốn chút thời gian để thực hành và làm việc một cách trơn tru với nó. Bây giờ, trong hệ sinh thái của Javascript thì Promises đã có mặt ở khắp các ngõ ngách rồi.
Promise giúp bạn quản lý code bất đồng bộ và được trả về từ nhiều DOM APIs cũng như là phía thư viện thứ ba (third pary library).
Promise xuất hiện góp phần rất lớn làm loại bỏ được callback hell. Nhưng khi dùng Promise không khéo léo, lại dễ dẫn đến Promise hell.
Từ đó Async/await ra đời như một cơ chế giúp bạn thao tác code bất đồng bộ một cách tuần tự và trong sáng hơn. 
Giờ thì mình cũng toàn dùng Async/await, ít khi dùng Promise. Mình hay dùng Promise khi muốn bọc Promise vào một hàm, để có thể sử dụng Async/await với hàm đó.

{% highlight js %}
function promises() {
  const successfulPromise = timeout(100).then(result => `success: ${result}`)

  const failingPromise = timeout(200, true).then(null, error =>
    Promise.reject(`failure: ${error}`),
  )

  const recoveredPromise = timeout(300, true).then(null, error =>
    Promise.resolve(`failed and recovered: ${error}`),
  )

  successfulPromise.then(log, logError)
  failingPromise.then(log, logError)
  recoveredPromise.then(log, logError)
}

function asyncAwaits() {
  async function successfulAsyncAwait() {
    const result = await timeout(100)
    return `success: ${result}`
  }

  async function failedAsyncAwait() {
    const result = await timeout(200, true)
    return `failed: ${result}`
  }

  async function recoveredAsyncAwait() {
    let result
    try {
      result = await timeout(300, true)
      return `failed: ${result}` // this would not be executed
    } catch (error) {
      return `failed and recovered: ${error}`
    }
  }

  successfulAsyncAwait().then(log, logError)
  failedAsyncAwait().then(log, logError)
  recoveredAsyncAwait().then(log, logError)
}

function log(...args) {
  console.log(...args)
}

function logError(...args) {
  console.error(...args)
}

// Dùng promise để biến hàm có thể sử dụng async/await
function timeout(duration = 0, shouldReject = false) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (shouldReject) {
        reject(`rejected after ${duration}ms`)
      } else {
        resolve(`resolved after ${duration}ms`)
      }
    }, duration)
  })
}

// Trong React:
function GetGreetingForSubject({subject}) {
  const [isLoading, setIsLoading] = React.useState(false)
  const [error, setError] = React.useState(null)
  const [greeting, setGreeting] = React.useState(null)

  React.useEffect(() => {
    async function fetchGreeting() {
      try {
        const response = await window.fetch('https://example.com/api/greeting')
        const data = await response.json()
        setGreeting(data.greeting)
      } catch (error) {
        setError(error)
      } finally {
        setIsLoading(false)
      }
    }
    setIsLoading(true)
    fetchGreeting()
  }, [])

  return isLoading ? (
    'loading...'
  ) : error ? (
    'ERROR!'
  ) : greeting ? (
    <div>
      {greeting} {subject}
    </div>
  ) : null
}
{% endhighlight %}

[MDN: Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[MDN: async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

[MDN: await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

Good luck!

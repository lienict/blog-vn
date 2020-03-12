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
Từ ngày React Hooks ra đời, cách code React đã trở nên đơn giản, dễ code hơn bao giờ hết. 
Thành thạo những features của JavaScript để áp dụng vào việc build một ứng dụng bằng React đã trở thành một việc 
vô cùng tất yếu rồi. Bài viết này sẽ liệt kê ra vài features JavaScript mà tôi khuyến khích các bạn dành thời gian
để thành thạo nó, từ đó làm cho việc xây dựng ứng dụng React (chắc chắn là hơn thế nữa) của các bạn trở nên 
hiệu quả hơn bao giờ hết.
Let's go! 

## Template Literals

Template literals are like regular strings with super-powers:

{% highlight js %}
const greeting = 'Hello'
const subject = 'World'
console.log(`${greeting} ${subject}!`) // Hello World!

// this is the same as:
console.log(greeting + ' ' + subject + '!')

// in React:
function Box({className, ...props}) {
  return <div className={`box ${className}`} {...props} />
}
{% endhighlight %}

[MDN: Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

## Shorthand property names

This is so common and useful that I do this without thinking now.

{% highlight js %}
const a = 'hello'
const b = 42
const c = {d: [true, false]}
console.log({a, b, c})

// this is the same as:
console.log({a: a, b: b, c: c})

// in React:
function Counter({initialCount, step}) {
  const [count, setCount] = useCounter({initialCount, step})
  return <button onClick={setCount}>{count}</button>
}
{% endhighlight %}

[MDN: Object initializer _New notations in ECMAScript 2015_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)

## Arrow functions

Arrow functions are another way to write functions in JavaScript, but they do
have a few semantic differences. Luckily for us in React land, we don't have to
worry about `this` as much if we're using hooks in our project (rather than
classes), but the arrow function allows for terser anonymous functions and
implicit returns, so you'll see and want to use arrow functions plenty.

{% highlight js %}
const getFive = () => 5
const addFive = a => a + 5
const divide = (a, b) => a / b

// this is the same as:
function getFive() {
  return 5
}
function addFive(a) {
  return a + 5
}
function divide(a, b) {
  return a / b
}

// in React:
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

> One thing to note about the example above is the opening and closing
> parentheses `(`. This is a common way to leverage the arrow function's
> implicit return capabilities when working with JSX.

[MDN: Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Destructuring

Destructuring is probably my favorite JavaScript feature. I destructure objects
and arrays all the time (and if you're using `useState` you probably are too,
[like so](/blog/react-hooks-array-destructuring-fundamentals)). I love how
declarative it is.

{% highlight js %}
// const obj = {x: 3.6, y: 7.8}
// makeCalculation(obj)

function makeCalculation({x, y: d, z = 4}) {
  return Math.floor((x + d + z) / 3)
}

// this is the same as
function makeCalculation(obj) {
  const {x, y: d, z = 4} = obj
  return Math.floor((x + d + z) / 3)
}

// which is the same as
function makeCalculation(obj) {
  const x = obj.x
  const d = obj.y
  const z = obj.z === undefined ? 4 : obj.z
  return Math.floor((x + d + z) / 3)
}

// in React:
function UserGitHubImg({username = 'ghost', ...props}) {
  return <img src={`https://github.com/${username}.png`} {...props} />
}
{% endhighlight %}

[MDN: Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

> Definitely read that MDN article. You are certain to learn something new. When
> you're done, try to refactor this to use a single line of destructuring:

{% highlight js %}
function nestedArrayAndObject() {
  // refactor this to a single line of destructuring...
  const info = {
    title: 'Once Upon a Time',
    protagonist: {
      name: 'Emma Swan',
      enemies: [
        {name: 'Regina Mills', title: 'Evil Queen'},
        {name: 'Cora Mills', title: 'Queen of Hearts'},
        {name: 'Peter Pan', title: `The boy who wouldn't grow up`},
        {name: 'Zelena', title: 'The Wicked Witch'},
      ],
    },
  }
  // const {} = info // <-- replace the next few `const` lines with this
  const title = info.title
  const protagonistName = info.protagonist.name
  const enemy = info.protagonist.enemies[3]
  const enemyTitle = enemy.title
  const enemyName = enemy.name
  return `${enemyName} (${enemyTitle}) is an enemy to ${protagonistName} in "${title}"`
}
{% endhighlight %}

## Parameter defaults

This is another feature I use all the time. It's a really powerful way to
declaratively express default values for your functions.

{% highlight js %}
// add(1)
// add(1, 2)
function add(a, b = 0) {
  return a + b
}

// is the same as
const add = (a, b = 0) => a + b

// is the same as
function add(a, b) {
  b = b === undefined ? 0 : b
  return a + b
}

// in React:
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

The `...` syntax can be thought of as kind of a "collection" syntax where it
operates on a collection of values. I use it all the time and strongly recommend
you learn how and where it can be used as well. It actually takes different
meanings in different contexts, so learning the nuances there will help you.

{% highlight js %}
const arr = [5, 6, 8, 4, 9]
Math.max(...arr)
// is the same as
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
// is the same as
console.log(Object.assign({}, obj1, obj2))

function add(first, ...rest) {
  return rest.reduce((sum, next) => sum + next, first)
}
// is the same as
function add() {
  const first = arguments[0]
  const rest = Array.from(arguments).slice(1)
  return rest.reduce((sum, next) => sum + next, first)
}

// in React:
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

If you're building an app with modern tools, chances are it supports modules,
it's a good idea to learn how the syntax works because any application of even
trivial size will likely need to make use of modules for code reuse and
organization.

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

> As another resource, I gave a whole talk about this syntax and you can
> [watch that talk here](https://www.youtube.com/watch?v=kTlcu16rSLc&list=PLV5CVI1eNcJgNqzNwcs4UKrlJdhfDjshf)

## Ternaries

I love ternaries. They're beautifully declarative. Especially in JSX.

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

> I realize that ternaries can get a knee-jerk reaction of disgust from some
> people who had to endure trying to make sense of ternaries before
> [prettier](https://prettier.io) came along and cleaned up our code. If you're
> not using prettier already, I strongly advise that you do. Prettier will make
> your ternaries much easier to read.

[MDN: Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

## Array Methods

Arrays are fantastic and I use array methods all the time! I probably use the
following methods the most frequently:

- find
- some
- every
- includes
- map
- filter
- reduce

Here are some examples:

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

## Promises and async/await

This one's a big subject and it can take a bit of practice and time working with
them to get good at them. Promises are everywhere in the JavaScript ecosystem
and thanks to how entrenched React is in that ecosystem, they're everywhere
there as well (in fact, React itself uses promises internally).

Promises help you manage asynchronous code and are returned from many DOM APIs
as well as third party libraries. Async/await syntax is a special syntax for
dealing with promises. The two go hand-in-hand.

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

// This is the mothership of all things asynchronous
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

// in React:
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

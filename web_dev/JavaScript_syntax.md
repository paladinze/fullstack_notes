
```js
/* ES6（ES2015） */

// arrow function
const multiply = (x, y) => x * y;

// default value in function
function multiply(x = 1, y = 1) {
	return x * y;
}

// templated string
const greeting = `Hello ${first} ${last}! Welcome back!`;

// multi-line string
const multiline = `This on the other hand,
actually is a multi-line string,
thanks to JavaScript ES6`

// Let and Const has block scope
function scopeTest() {
	let x = 10;
	{
		let x = 100;
	}
	return x;
}
console.log(scopeTest()); // 10

// destructure: simple
const randomData = { a: 12, b: false, c: 'blue' };
const { a, c } = randomData;

// destructure: array
const arr = [1, 2, 3];
const [a, b, c] = arr;
console.log(a, b, c); // 1, 2, 3

// destructure: nested object
const user = {
	id: 339,
	name: 'Fred',
	age: 42,
	education: {
		degree: 'primary'
	}
};
const { education: { degree } = {} } = user;
console.log(degree); //prints: primary

// val can be ommited, if val and prop have the same name
function showBookInfo(title, author) {
	return {
		title,
		author
	}
}
console.log(showBookInfo("The Hobbit", "J.R.R. Tolkien"));


// forEach
const numbers = [1, 2, 3, 4, 5];
function timesTwo(number) {
	console.log(number * 2);
}
numbers.forEach(timesTwo);

// map
const numbers = [1, 2, 3, 4, 5];
function timesTwo(number) {
	return number * 2;
}
const doubleNumbers = numbers.map(timesTwo);
console.log(doubleNumbers);

// filter
const numbers = [1, 2, 3, 4, 5];
function isOdd(number) {
	return number % 2 === 1
}
const oddNumbers = numbers.filter(isOdd);
console.log(oddNumbers);

// class
class Book {
	constructor(title, author, pages) {
		this.title = title;
		this.author = author;
		this.pages = pages;
	}

	get title() {
		return this.title;
	}

	getPageCount() {
		return this.pages;
	}
}

// class inheritance
class Novel extends Book {
	constructor(title, author, pages, genre) {
		super(title, author, pages);
		this.genre = genre;
	}

	getGenre() {
		return this.genre;
	}
}
let book = new Novel('The Hobbit', 'J.R.R. Tolkien', 310, 'Fantasy');
console.log(book.getAuthor());

// module: named exports/imports
// lib.js
export const sqrt = Math.sqrt;
export function square(x) {
	return x * x;
}

// main.js
import { square, diag } from 'lib';
console.log(square(11)); // 121

// module: default exports
export default function () {};
import myFunc from 'myFunc';
myFunc();


// spread operator
function sum(x, y, z) {
	return x + y + z;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers));


// for of: iterate the values
let a = [1, 2, 3]
for (let i of a) console.log(i);

// for in: iterate the keys
let a = { a: 1, b: 2, c: 3 }
for (let i in a) console.log(a);


// ES7 (2016)
let numbers = [1, 2, 3, 4];
if(numbers.includes(2)) {
  console.log('Array contains value');
}

// Exponentiation Operator
console.log(2 ** 4); // 16


// define promise
const myPromise = () => {
	return new Promise((resolve, reject) => {
		resolve("promise success")
		reject("failure reason")
	})
}

// promise chain simple
const asyncPromise = new Promise((resolve, reject) => {
	console.log('Doing the first thing async...');
	resolve();
}).then(() => {
	console.log('Doing something else...');
})

// promise chain medium
const url = 'https://jsonplaceholder.typicode.com/posts';
const getData = (url) => fetch(url);
getData(url).
	then(data => data.json()).
	then(result => console.log(result));

// ES8 (2017)
// asyc await syntax: a wrapper for promise
// async function always return a promise.

async function loadJson(url) {
  let resp = await fetch(url)
  if (resp.status == 200) {
    return resp.json()
  } else {
    throw new Error(resp.status)
  }
}

loadJson('no-such-user.json')
  .catch(alert); // Error: 404


// aync await: call async from a regular function
async function wait() {
  await new Promise(resolve => setTimeout(resolve, 1000));
  return 10;
}

function f() {
  wait().then((res) => console.log(res))
}
f()

// async: arrow function
const msg = async () => {
  const msg = await scaryClown();
  console.log('Message:', msg);
}


// async: api call
async function fetchUsers(endpoint) {
  const res = await fetch(endpoint);
  const data = await res.json();

  data = data.map(user => user.username);

  console.log(data);
}

fetchUsers('https://jsonplaceholder.typicode.com/users');


// ES9 (2018)

// Object Rest / Spread: destructure
const {a, b, c, ...x} = {a: 1, b: 2, c: 3, x: 4, y: 5, z: 6};

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3

console.log(x); // { x: 4, y: 5, z: 6 }



// Object Rest / Spread: merge
const a = 1, b = 2, c = 3;
const x = {x: 4, y: 5, z: 6};

const obj = {a, b, c, ...x};

console.log(obj); //{a: 1, b: 2, c: 3, x: 4, y: 5, z: 6};
```
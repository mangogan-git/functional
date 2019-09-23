# Naming Convention
<!-- .slide: id="naming" -->

Variable
```js
/** @type {string} */
const _private = '_private';

/**
 * Gender
 * 
 * @enum {string}
 **/
const Enum = {
    FEMALE: 0,
    MALE: 1,
};

const PI = 3.14;
```

Note: 
1. 私有成員用 **_** 開頭
2. 列舉值首字大寫
3. 常數全大寫
4. 變數與函數命名用駝峰方式，首字小寫

--

Function
```js
function nameCamelCase(){
    // ...
}

const obj = {
    _privateMethod(){

    },

    publicMethod(){

    }
}
```

> 有時候會用 **$** 做變數開頭 (Jquery)，通常代表該變數是 [DOM](https://developer.mozilla.org/zh-TW/docs/Web/API/Document_Object_Model) 物件
<!-- .element: class="fragment" data-fragment-index="1" -->

Note:
習慣上也是使用底線 **_** 來區分私有函式與公用函釋
不過在 JS 中並沒有真正的 private

--

# 語句結構 (statements)

## if...else
```js
if(true) {
    // ...
}
// comment here
else {
    // ...
}
```
> 這邊是我們的習慣，看團隊中的規範  
> 這裡有一篇[討論](https://github.com/airbnb/javascript/issues/325)可以參考
<!-- .element: class="fragment" data-fragment-index="1" -->

--

## enum
當你有兩個列舉是互相有直接關係的
```js
const Animal = {
    DOG: 0,
    CAT: 1,
};

const Sound = {
    '0': 'Bark!',
    '1': 'meow~',
};
// 或是寫成 array ['Bark!', 'meow~']

console.log(`dog say: ${Sound[Animal.DOG]}`);
// "dog say: Bark!"
```

--

建議寫成這種結構
```js
const Animal = {
    DOG: 0,
    CAT: 1,
};

const Sound = {
    [Animal.DOG]: 'Bark!',
    [Animal.CAT]: 'meow~',
};

```

---

# 註解風格
習慣上採用 [JSDoc](https://jsdoc.app/) 的註解風格, 有時候會混用一些 TypeScript 的註解方式

Number
```js
/**
 * Sum two number
 * 
 * @param {number} a
 * @param {number} b
 * @returns number
 * @example
 * sum(1 + 2); // 3
 **/
function sum(a, b) {
    return a + b;
}
```

--

Object - style1
```js
/**
 * @param {Object} param
 * @param {number} param.a - describe...
 * @param {number} param.b - describe...
 * @returns {number}
 **/
function sum(param) {
    return param.a + param.b;
}
```

--

Object - style2
```js
/**
 * @param {{a:number, b:number}} param
 * @returns {number}
 **/
function sum(param) {
    return param.a + param.b;
}
```

--

解構賦值 ([Destructuring parameter](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment))
```js
/**
 * @param {Object} param
 * @param {number} param.a
 * @param {number} param.b
 * @returns {number}
 **/
function sum({a, b}) {
    return a + b;
}
```

--

Callback - style1
```js
/**
 * @param {Object} param
 * @param {number} param.a
 * @param {number} param.b
 * @param {(result: number)=>void} param.cb - result callback
 * @returns {number}
 **/
function sum({a, b, cb}) {
    cb(a + b);
}
```

--

Callback - style2
```js
/**
 * @param {Object} param
 * @param {number} param.a
 * @param {number} param.b
 * @param {function(number)} param.cb - result callback
 * @returns {number}
 **/
function sum({a, b, cb}) {
    cb(a + b);
}
```

--

String
```js
/**
 * @param {string} str
 * @returns {string}
 * 
 * @example
 * upperCase('aaa'); // AAA
 **/
function upperCase(str) {
    return String.prototype.toUpperCase.call(str);
}
```

--

see more at:
- [JSDoc](https://jsdoc.app/)
- [aribnb javascript style guide](https://github.com/airbnb/javascript)
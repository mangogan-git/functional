<style type="text/css">
  /********************************************* 
  * HEADERS
  *********************************************/
  .reveal h1 { 1.6em; }
  .reveal h2 { 1.4em; }
  .reveal h3 { 1.2em; }
  .reveal h4 { 1em; }

  /********************************************* 
  * FONT
  *********************************************/
  .reveal p.left {
      
  }

  /********************************************* 
  * CODE
  *********************************************/
  .reveal pre {
      /* font-size: 1em; */
  }
  .reveal pre code {
      max-height: 80%;
  }
</style>

# TITLE
Javascript...

---
我們假設你已經知道了:

- var, let ,const 的差異
- 變數提升 (Hosting)
- 閉包 (closure)
- this (context 上下文)
- prototype

這些 JS 的特性

--

在這裡會提到

- 命名慣例、規範
- 常用的 API
- Functional Programming

---

# ...
[LINK](#/appendix)
[LINK](#/naming)

Note:
# 大綱
常用 API
組合與繼承
常見的錯誤

---
# 命名慣例
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
<!-- .element: style="font-size: 100%;" -->

--

Function
```js
function nameCamelCase(){
    // ...
}
```

---

# 註解風格

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

Destructuring parameter 

[reference](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

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
- [devdocs.io](https://devdocs.io/jsdoc/)


---

# iframe

<iframe width="100%" height="600px" src="//jsfiddle.net/duskyhell/wbnLah2j/embedded/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
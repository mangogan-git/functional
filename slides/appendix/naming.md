# Naming Convention
<!-- .slide: id="naming" -->

--
一些名詞對照

- **Object**: 物件，大陸翻譯 "对象"
- **Function**: 函式，物件中的屬性稱 "方法"

--
## Variable
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
## Function
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
## Class

類別名稱首字大寫
```js
class User {
    constructor(name){
        this.name = name;
        // ...
    }

    greeting(){
        return `Hello, ${this.name}`;
    }
}

// or

const Animal = function(name){ this.name = name;};
Animal.prototype.greeting = 
    function(){return `Hello, ${this.name}`}

```

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
## String

```js
const someText = 'aegis';

const otherText = 'pwd "how do you turn this on"';
```
表示一個字串可以用 雙引號 **"..."*** 或單引號 ***'...'***  
我們習慣上統一使用單引號 **'...'***

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
<pre><code class="hljs javascript" data-line-numbers="7,8" data-trim>
const Animal = {
    DOG: 0,
    CAT: 1,
};

const Sound = {
    [Animal.DOG]: 'Bark!',
    [Animal.CAT]: 'meow~',
};
</code></pre>

--
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

Note: 
1. 習慣上註解都使用 JSDoc 的格式
2. 命名規範可以透過 Eslint 套件來協助檢查, 可以參考 aribnb
# Guide

網路上的教學文章有一些比較舊，使用的是 ES5 的語法

這裡列出建議的使用方式

---

## 1. 使用[箭頭函式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions)取代一般函式
因為它看起來比較簡潔，而且綁定了上下文 (context)，避免在傳遞 callback 時出了問題

// ES5
```js
var stringSplit = function(text, separator) {
    return text.split(separator)
};

stringSplit('a_b_c', '_'); // ['a', 'b', 'c']
```
// ES6
```js
const stringSplit = (text, separator) => text.split(separator);
```

--

只有一個參數可以省略括號 **"()"**

// ES5
```js
var add1 = function (a) {
    return a + 1;
};
```

// ES6
```js
const add1 = a => a + 1
```

--

綁定上下文 (context)
<pre><code class="hljs javascript" data-line-numbers="3-5" data-trim>
const user = {
    id: 'c8763',
    login(){
        httpPost(this.id, this._onLogin.bind(this));
    },
    _onLogin(){
        console.log(`user ${this.id} login success`);
    }
};
</code></pre>

等同
<pre><code class="hljs javascript" data-line-numbers="3-5" data-trim>
const user = {
    id: 'c8763',
    login(){
        httpPost(this.id, () => this._onLogin());
    },
    _onLogin(){
        console.log(`user ${this.id} login success`);
    }
};
</code></pre>

> 比較常遇到忘記寫 `bind(this)` 的情況

---

## 2. 使用 Default Value 取代條件判斷

// ES5
```js
var stringSplit = function(text, separator) {
    if (separator === undefined) {
        separator = " ";
    }

    return text.split(separator)
};
```

// ES6
```js
const stringSplit = (text, separator = " ") => text.split(separator);
```

---

## 3. 使用[解構賦值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)取代可選參數(optional parameter)

// ES5
```js
/**
 * @param {string} path - 檔案路徑
 * @param {(current: number, total: number)=>void} [progress] - 下載進度
 * @param {function} finish - callback
 **/
var download = (path, progress, finish)=> {
    if(arguments.length === 2) {
        finish = progress;
        progress = undefined;
    }
    // stuff...
};

download('https://github.com/404.png', function(){ console.log('finish')});
```

Note:
在 JS 註解中參數用引號 "[]" 包起來代表該參數為 optional

--

// ES6
```js
/**
 * @param {string} path - 檔案路徑
 * @param {(current: number, total: number)=>void} [progress] - 下載進度
 * @param {function} finish - callback
 **/
const download({path, progress, finish}) {
    // stuff...
};

download({
    path: 'https://github.com/404.png',
    finish(){
        console.log('finish');
    },
});
```

Note: 
我的建議是當你的參數超過兩個就使用解構賦值，一個是沒有參數傳遞順序的問題，另外就是調用者的參數語意也清楚
(前提是要有好的變數命名)


---

## 4. 使用[字串模板](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)取代字串串接

// don't use
```js
getUserData(data => {
    console.log('name: ' + data.name + ', age:' + data.age);
});
```

// use
```js
getUserData(data => {
    console.log(`name: ${data.name}, age: ${data.age}`);
});
```

---

## 5. 使用展開運算符([Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax))取代 arguments

// don't use
```js
function sum(){
    const numberList = Array.prototype.slice.call(arguments);
    return numberList.reduce((v, r) => v + r);
}
sum(1, 2, 3, 4, 5, 6); // 21
```

// use
```js
function sum(...numerics) {
    return numerics.reduce((v, r) => v + r);
}
```

--

還可以用來合併陣列、呼叫函式

```js
const aryA = [1,2,3];
const aryB = [4,5,6];
const aryC = [...aryA, ...aryB];
```

call function
```js
const add = (a, b) => a + b;
add(...[1, 2]); //3
```

---

## 6. 使用[解構賦值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)取出成員變數

// math_util.js
```js
const add = (a, b) => a + b;
const pow = (base, exponent) => base ** exponent;
// equality Math.pow()

module.export = {
    add,
    pow,
}
```

// don't use
```js
const math = require('math_util');
const add = math.add;
const pow = math.pow;
// ...
```

// use
```js
const {add, pow} = require('math_util');
```

---

## 7. 使用 forEach, reduce 取代 for loop

// don't use
```js
const ary = [1,2,3,4,5];
let result = 0;
for(let idx =0; idx < ary.length; idx ++) {
    result += ary[idx];
}
```

// use
```js
let result = 0;
ary.forEach(v => result+=v);

// or
const result = ary.reduce((v,r) => v + r);
```

--

還有一個 map

// don't use
```js
const ary = [1, 2, 3];
let doubleAry;
for(let idx =0; idx < ary.length; idx ++) {
    doubleAry[idx] = ary[idx] * 2;
}
```

// use
```js
const ary = [1, 2, 3];
const doubleAry = ary.map(num => num * 2);
```

--

為什麼要用 forEach?
# TODO
google: for vs foreach site:jsperf.com  
https://jsperf.com/for-vs-foreach-vs-for-of/602

https://github.com/dg92/Performance-Analysis-JS
https://codeburst.io/javascript-performance-test-for-vs-for-each-vs-map-reduce-filter-find-32c1113f19d7

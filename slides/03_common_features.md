# Essential features
這部份會介紹一些常用的特性與常見的錯誤

--

## this
**this** 永遠指向調用該函式的物件 (也就是指向 caller)
```js
class User {
    constructor(name){
        this.name = name;
    }

    greeting(){
        return `Hello, ${this.name}`;
    }
}

const jeff = new User('Jeff');
jeff.greeting(); // "Hello, Jeff"
```
就這樣，沒什麼複雜的地方

--

再來是 Object's method
```js
const obj = {
    _name: 'obj name',
    printName(){
        console.log(this._name);
    },
};

obj.printName(); // "obj name"
```

caller 為 **`obj`** ，所以輸出 '`obj name`'
<!-- .element: class="fragment" data-fragment-index="1" -->
<br/>
<br/>

接著下面這個例子就比較多人會遇到問題
<!-- .element: class="fragment" data-fragment-index="2" -->

--

log 會輸出什麼？
```js
var name = 'outside';
function printName(){
    console.log(this.name);
}
printName(); // ?
```

在 NodeJs 中會輸出 `"outside"`
<!-- .element: class="fragment" data-fragment-index="1" -->
在 瀏覽器中會輸出 `"outside"`
<!-- .element: class="fragment" data-fragment-index="2" -->
在[嚴格模式](#/appendix_strict)下會拋出例外  
<!-- .element: class="fragment" data-fragment-index="3" -->
`TypeError: Cannot read property 'name' of undefined`
<!-- .element: class="fragment error" data-fragment-index="3" -->

--

### var, let, const

我們先講 `var` 跟 `let`, `const` 的[差別](#/appendix_declare)
<pre><code class="hljs javascript" data-line-numbers="1,5" data-trim>
var name = 'outside';
function printName(){
    console.log(this.name);
}
printName(); // "outside"
</code></pre>

<pre><code class="hljs javascript" data-line-numbers="1,5" data-trim>
const name = 'outside';
function printName(){
    console.log(this.name);
}
printName(); // undefined
</code></pre>

`var` 會把你的變數暴露到全域物件

--

run in [repel](https://repl.it/repls/WatchfulPeskyTree)
<iframe height="600px" width="100%" src="https://repl.it/repls/WatchfulPeskyTree?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals">

```js
var name = 'outside';
console.log(global.name);

const name2 = 'outside2';
console.log(global.name2);
```

</iframe>

--

首先要避免在一般的函式內使用到 `this`
```js
function printName(){
    console.log(this.name);
}
```

也避免使用 `var`，用 `var` 會有變數提升([hoisting](https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting)) 與暴露到全域的問題

--

有時候當變數名稱很長，你可能想要用另外一個比較短的變數去接它
```js
const userModelOfTheFacebook = {
    _name: 'fb name',
    getName(){
        return this._name;
    },
};
userModelOfTheFacebook.getName();
// 替換成
const getFbName = userModelOfTheFacebook.getName;
getFbName(); // 問題就出在這
```

這邊的 `getFbName()` **Caller** 被改變了

--

> **this** 永遠指向調用該函式的物件 (也就是指向 Caller)

1. `getFbName()`: 預設情況下 **this** 會指向全域物件
2. 全域物件在 NodeJs 裡面是 **"global"**, 瀏覽器下是 **"window"**
3. [嚴格模式](#/appendix_strict)下拋出例外

<pre><code class="hljs javascript" data-line-numbers="2" data-trim>
const getFbName = userModelOfTheFacebook.getName;
getFbName();
</code></pre>

Note:
這邊的 getFbName(); 因為是直接呼叫，所以它會回傳 `undefined` 或是拋出例外

--

run in [repel](https://repl.it/repls/HeartfeltHospitableHypercard)
<iframe height="600px" width="100%" src="https://repl.it/repls/HeartfeltHospitableHypercard?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals">

```js
console.log(`global === this? ${global === this}`); // true

var name = 'outside';
function printNameStrictMode(){
  'use strict'
  console.log(this.name);
}
printNameStrictMode();
```
</iframe>

--

## 改變 "this"

<pre><code class="hljs javascript" data-line-numbers="2" data-trim>
const getFbName = userModelOfTheFacebook.getName;
getFbName();
</code></pre>
這裡簡單描述，詳細請見此篇 [slides](https://slides.com/mangogan/js_this)
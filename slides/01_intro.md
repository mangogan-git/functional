<style type="text/css">
  /********************************************* 
  * FONT
  *********************************************/
  .reveal .left {
      text-align: left;
  }  
  .reveal p.error {
      color: #ff0066;
  }
  /********************************************* 
  * CODE
  *********************************************/
  .reveal blockquote p{
	font-size: 1em;
  }
  .reveal pre {
      font-size: 1em;
  }
  .reveal pre code {
      max-height: 80%;
      padding: 10px;
  }
</style>

# TITLE
TODO...

---
假設你已經知道了:

- JS 基本的語法結構
- ES5、ES6 的差異
- 變數提升 ([Hoisting](#/appendix_hoisting))
- 閉包 ([Closure](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Closures))
- [prototype](https://slides.com/mangogan/jsprototype#/)

這些 JS 的特性

Note: 我會介紹一些我覺得比較重要的特性，其他的補充資料可以參考附錄

--

在這份 Slides 中會提到:

- 命名慣例
- 幾個比較重要的特性
- 常見的錯誤
- 常用的工具網站

> 後面提到的 JS 皆是在 NodeJS 下執行的結果，我們不會特別討論與瀏覽器之間的差異，撰寫此文時我用的版本是 **10.15.3**  
> 
> 如果你還沒有安裝 NodeJs，可以在[這裡](https://repl.it/languages/nodejs)做一些測試

--

一些名詞對照

- **Object**: 物件，大陸翻譯 "对象"
- **Function**: 函式，物件中的屬性稱 "方法"

--

其他參考資料

- [ECMAScript 6 入门](http://es6.ruanyifeng.com/)
- [devdocs.io](https://devdocs.io/javascript/)
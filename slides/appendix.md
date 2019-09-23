# 附錄 A
<!-- .slide: id="appendix" -->
TODO...
--

# var, let, const
<!-- .slide: id="appendix_declare" -->

- `var`: 不使用，var 會有變數提昇的問題 (Hoisting)
- `let`: 變數
- `const` 常數，不過屬性還是會被改變
    ```js
    const obj = {a: 1};
    obj.a = 2;
    console.log(obj.a); // 2
    ```
---

# "use strict"
<!-- .slide: id="appendix_strict" -->
see [https://slides.com/mangogan/jsintro#/8/1](https://slides.com/mangogan/jsintro#/8/1)
# Hoisting

---

# 常用 API

- [Object](#/Object)
- Array
- String

--

# Object
<!-- .slide: id="Object" data-transition="concave" data-background="#A7C66B" -->
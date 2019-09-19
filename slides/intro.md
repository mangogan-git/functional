# TITLE
Functional programing in Javascript

<sub>[github](//www.google.com)</sub>

---

# ...
<a href="#/appendix">Link</a>

---

# 為什麼要用 functional programing?

1. 易於測試
2. 易於重用、組合
3. 

---

# Pure Function, Impure Function, SideEffect

- Pure Function: 純函數，沒有副作用
- Impure Function: 有副作用的函數
- Side Effect: 副作用

什麼是副作用?

--

# SideEffect

1. 輸出結果受到除了輸入以外的外部狀態影響
    ```js
    let count = 1;
    function counting(n) {
        count = count+1;
    }
    ```
2. 函數改變輸入的參數
    ```js
    const array = [1, 2, 3];
    array.shift();
    console.log(array); // [2, 3]
    ```

其它還有受到時間性質、I/O、外部資料庫等等影響

---

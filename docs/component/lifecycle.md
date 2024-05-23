# 元件的生命週期

## 執行順序

!["元件的生命週期"](https://codecraft.tv/courses/angular/components/lifecycle-hooks/images/lifecycle-hooks.png)

### 1. constructor
當 constructor 執行時，元件尚未被初始化，因此幾乎不會在這個階段寫程式碼，主要用於相依注入 (dependency injection)，例如服務、函式或值。


### 2. ngOnChanges
第一次 binding 就會觸發，當綁定的值變動的時候觸發，前提是要有綁定的值。可觸發多次，子元件的值會參考父元件最後一次改變的值，子元件更改父元件傳入的值，但父元件不受影響。

### 3. ngOnInit
用來初始化頁面內容，顯示數據綁定、設置 directive 和輸入屬性，在第一次 ngOnChanges 完成後呼叫，只執行一次。

### 4. ngDoCheck
在 ngOnChanges 和 ngOnInit 之後，於每次檢測變化時執行，使用時需注意 ngOnChanges 被觸發的頻率非常高，程式碼應盡量精簡，避免導致頁面性能問題，不論是父組件或子組件的值發生改變，都會觸發到整顆樹的 doCheck。子元件的值發生改變，會觸發父元件與子元件的 doCheck；父元件的值發生改變，也會觸發父元件與子元件的 doCheck。

### 5. ngOnDestory
在元件被摧毀之前執行。

---

> 參考資料  
> [Angular 生命週期介紹](https://lt1stsolomid.medium.com/希望是最詳細的-angular-生命週期文章-27da6e8b33a9)  
> [Angular Component Lifecycle](https://angular.io/guide/lifecycle-hooks)
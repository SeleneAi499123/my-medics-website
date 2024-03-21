# ng-content

ng-content 允許使用者在一個組件的模板中定義一個插槽，然後在該組件的外部使用時，可以將顯示內容投影到這個插槽中。

---

## ng-content

以下為父層的html：

```html
<check-stock [qty]="qty_parent" [stock]="stock_parent">
  <span id="lower">庫存不足{{stock_parent}}</span>
  <span id="enough">庫存足夠{{stock_parent}}</span>
</check-stock>
```

子層的html：
```html
<ng-content *ngIf="isLower; else enough" select="#lower"></ng-content>
<ng-template #enough>
    <ng-content select="#enough"></ng-content>
</ng-template>   
```

---

## @ContentChild

- 取得符合的元素或是名字(#name)
- 在ngAfterContentInit() 裡面取得內容查詢

父層的html：
```html
<check-stock [qty]="qty_parent" [stock]="stock_parent">
  <!-- @ContentChildren -->
  <span #span id="lower">庫存不足{{stock_parent}}</span>
  <span #span id="enough">庫存足夠{{stock_parent}}</span>
</check-stock>
```

子層的.ts：
```ts
@ContentChildren('span') mySpans:any;

ngAfterContentInit() {
    this.mySpans.forEach((element:any) => {
        console.log(element);
    });
}
```
---


## @ViewChild

- 會在檢視DOM的當中取得符合的元素類型或是名字(#name)
- 在ngAfterContentInit()裡面處理
- @ViewChild 取得第一個符合的元素
- @ViewChildren 取得一組符合的元素(List)

父層的html：
```html
<h1 #title1>標題</h1>
```

子層的.ts：
```ts
@ViewChild ('title1') h1:ElementRef |any;

ngAfterViewInit() {
    let title1=this.h1.nativeElement;
    title1.addEventListener("click", ()=>title1.innerHTML ="title1 + click event");
}

ngAfterViewChecked() {
    // h1被Click到就會觸發ngAfterViewChecked
    console.log(h1.nativeElement);
}
```
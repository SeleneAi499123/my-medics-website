# 什麼是元件

元件（Component）是一種應用程式的檢視元素，由HTML、TypeScript、CSS組合而成。每個應用程式預設都會有一個AppComponent元件，這是應用程式的根元件，以`<app-root></app-root>`載入到`index.html`中。

---

## 建立一個元件

使用終端機指令在專案的app目錄底下新增一個MyComponent元件，會產生`my-component.component.ts`以及`my-component.component.html`兩個檔案，並且會自動在`app.module.ts`內引用元件：

```bash
ng g c my-component
```

若不需要.html檔，可在後面加上`-t`參數。  

想要顯示該元件的內容，需要在父元件`app.component.html`內嵌入`<app-my-component></app-my-component>`來顯示View，元件的selector名稱可以在`my-component.component.ts`裡面修改。

```html title="app.component.html"
<app-my-component></app-my-component>
```

```ts
@Component({
  // 在這裡修改selector
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styles: [
  ]
})
```

---


## 結構型指令

- **ngFor**

```html
<ul>
    <li *ngFor="let m of members; let i =index; let flag=last">
        {{i+1}}:{{m}}
        <ng-container *ngIf="flag">
            <hr>
             共{{i+1}}筆
        </ng-container>
        
    </li>
</ul>
```
index 會取索引值，其他屬性的使用請參考以下表格：


|  屬性名    | 回傳 Boolean |
| --------- | ----------- |
| first    | 是否為第一筆  |
| last    | 是否為最後一筆  |
| even    | 是否為偶數  |
| odd | 是否為奇數  |

- **ngIf**

```html
<div *ngIf="noMember.length>0;else showThisDiv">
    <!-- 不會進這裡 -->
</div>
<ng-template #showThisDiv>
    空陣列
</ng-template>
```
使用`#`可以為元素宣告自定義的變數名稱。


- **ngSwitch**

```html
<td>
    <ng-container [ngSwitch]="s.Birthday.getMonth()">
    <span *ngSwitchCase="thisMonth">本月壽星</span>
    <span *ngSwitchCase="thisMonth+1">下個月生日</span>
    <span *ngSwitchDefault>Default都不是</span>
    </ng-container>  
</td>
```

---

## 容器


### ng-container
ng-container 不會被渲染出來，通常都會被拿來處理一些邏輯的事情，如 ngIf、ngSwitch 或 ngFor。
雖然這些也能寫在 div 上，不過 div 它會被呈現出來，有時後會影響排版。



### ng-template
如果有使用到 if/else，這時後就需要一個 ng-template 來做搭配，通常它不會直接顯示出來，當條件成立後，ng-template 裡的內容才會被呈現。
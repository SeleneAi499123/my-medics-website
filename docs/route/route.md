# 什麼是Route

Angular 的路由功能是 Angular 框架中的一個重要部分，它允許開發者在不同的 URL 路徑之間導航，並在每個路由路徑下加載相應的組件，並記錄瀏覽歷史。

---

## 啟用Routing功能

在新建一個 Angular 專案時，我們可以加入 `--routing` 參數，使專案的app夾底下產生`app-routing.module.ts`，並且會自動在`app.module.ts`內自動匯入AppRoutingModule模組。

```bash
ng new proj01 --routing
```

或是在既有專案中加入routing模組。

```bash
ng g module app-routing --module app --flat
```

---

## 定義路由清單

由CLI建立的`app-routing.module.ts`預設內容如下：

```typescript
import { RouterModule, Routes } from '@angular/router';
// 其他省略

const routes: Routes = [ ];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})

export class AppRoutingModule { }
```

我們可以藉由修改`routes`陣列內容來實現路由的配置，前面記得加上`export`才能給其他組件使用。

```typescript
export const routes: Routes = [
  { path:'page1', component:Page1Component, data:[], title:'page1' },
  { path:'page2', component:Page2Component, data:[], title:'page2' }
];
```

|  屬性    | 說明 |
| --------- | ----------- |
| path    | 路徑  |
|  component   | 符合路徑時的啟用元件  |
| redirectTo    | 重新導向的url  |
| children    | 設定子路由的Routes物件，指定巢狀路由  |
| data    | 開發人員自訂資料，為一組陣列  |
| title    | 超連結的文字顯示  |


---

## 產生導覽列

透過在網站的首頁新增導覽列，讓使用者可以更方便的瀏覽其他頁面，我們可以用`*ngFor`產生路由清單，最後不要忘記加上`<router-outlet></router-outlet>`啟用Angular的Route功能。

```html title="app.component.html"
<ul>
    <li *ngFor="let r of myRoutes">
        <a [routerLink]="r.path">{{r.title}}</a>        
    </li>
</ul>

<router-outlet></router-outlet>
```

宣告myRoutes變數，透過匯入`app-routing.module`來使用：

```typescript title="app.component.ts"
import { routes } from './app-routing.module'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styles: []
})

export class AppComponent {
  title = 'mod02';
  myRoutes = routes;
}
```

---

## 重新導向

透過將`path`設為空字串，當使用者沒有輸入完整路徑時，將頁面導向首頁，`pathMatch`的預設值是`prefix`，路徑由左開始檢查只要部分符合就會套用，此處設定為`full`以確保路徑完全符合。

```typescript
export const routes: Routes = [
  { path:'', redirectTo:'Home', pathMatch:'full' },
  { path:'Home', component:Page1Component, data:[], title:'page1' },
  // ...
];
```

---

## 使用萬用符號 **

路徑的比對是有順序性的，若有相同的兩個path，則會先套用上面的選項。使用萬用符號`**`可以在當以上路徑都不符合時，將頁面導向自訂義的PageNotFound元件，此路徑會放在整個路由清單的最後一項。

```typescript
export const routes: Routes = [
  { path:'', redirectTo:'Home', pathMatch:'full' },
  { path:'Home', component:Page1Component, data:[], title:'page1' },
  // ...
  { path:'**', component:PageNotFoundComponent }
];
```

---

## routerLinkActive 醒目提示

在超連結內加入`routerLinkActive="active"`會使該連結被點選時，為其套用`.active`樣式。
```html
<a routerLink="home" routerLinkActive="active">
```
```html
<style>
    .active{
        font-weight: bold;
        background-color: darkgray;
    }
</style>
```



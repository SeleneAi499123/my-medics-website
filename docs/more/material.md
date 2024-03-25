

# MkDocs Material

MkDocs Material 有許多好用的小東西，可以幫助我們豐富網站內容，詳細的使用方法可以參考[官方操作手冊](https://squidfunk.github.io/mkdocs-material/)。

 ---

## Extra features

:bulb:{.bulb} 以下是我在這個網站有用到的功能：

- ### Admonitions

 使用一些好用的警示框，像是 warning 框跟可展開的 info 框：

!!! warning 
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

??? info
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

---

- ### Buttons

在我的首頁有用到兩個按鈕，分別會導向 Getting started 或 Learn more 頁面。

[Quick start](../getting-started.md){ .md-button .md-button--primary } [Learn more](#){ .md-button }

---

- ### Code blocks 

在寫Markdown 筆記時，通常會用到大量的程式碼區塊，加上標題以及使用跟螢光筆功能，可以使我們在閱讀時更加的方便。

```ts title="check-ext-no.directive.ts" hl_lines="2 6-10"
export class CheckExtNoDirective {
    validate(control:AbstractControl):ValidationErrors | null{
        let extNo:number=parseInt(control.value);
        let result=null;
        if(extNo<1000||extNo>1999){
            result={
                "CheckExtNo":{
                    actualValue:extNo,
                    requiredValue:'分機介於1000~1999'
                }
            }
        }
        return result;
    }
}
```

---

- ### Content tabs

若是有兩個資訊需要比對時，使用 Content tabs 可以快速切換瀏覽內容。

=== "Latest"
    ``` sh
    npm install -g @angular/cli
    ```

=== "15.x"
    ``` sh
    npm install -g @angular/cli@15
    ```

---

- ### Data tables

可以在.md檔內用非常直觀的方式畫出一個表格，還可以設定對齊方式。

| Method      | Description      |
| ----------- | ---------------- |
| `GET`       |  Fetch resource  |
| `PUT`       |  Update resource |
| `DELETE`    |  Delete resource |

---

- ### Diagrams

在理解 Angular 的 Binding 功能時，繪畫 sequence diagrams 可以幫助我更好地理解。

``` mermaid
sequenceDiagram
    Component->>DOM: {{value}}
    Component->>DOM: [property] = "value"
    DOM->>Component: (Event) = "handler"
    
    Component->>DOM: 雙向綁定
    DOM->>Component: [(ngModel)] = "Property"
```


---

- ### Grids

Angular 有許多元件，這時使用grid cards 就可以直接導向目標頁面。


<div class="grid cards" markdown>

-   :simple-webcomponentsdotorg: __Component__

    ---

    了解什麼是 Angular 元件。

    [:octicons-arrow-right-24: Go to Page](../component/component.md)

-   :material-connection: __Service__

    ---

    了解服務的用法以及靜態注射的原理。

    [:octicons-arrow-right-24: Go to Page](../service/di.md)

-   :octicons-quote-16: __Directive__

    ---

    建立你自己的指令用於html元素上。

    [:octicons-arrow-right-24: Go to Page](../directive/directive.md)

-   :octicons-blocked-16: __Guard__

    ---

    建立網頁的守門員，驗證使用者身份。

    [:octicons-arrow-right-24: Go to Page](#)

</div>

---

## Special thanks

:rose: 將 MK Docs 網站部署到 GitLab Page 的方法，感謝日宏提供的 [教學](https://test-zoxul-25825563df0f22bc52a20ee5150919645dc3ef0f19709d858ccf.gitlab.io/git/) 。  
:sunflower: 感謝 Kim 學長提供 [範例](https://week-1-markdown-vian1113-988613423c571b6e909372a4c42f9b2b41b308.gitlab.io/) 給我參考～


# MkDocs Material

MkDocs Material 有許多好用的小東西，可以幫助我們豐富網站內容，詳細的使用方法可以參考[官方操作手冊](https://squidfunk.github.io/mkdocs-material/)。

 ---

## Addtionals

:bulb:{.bulb} 以下是我在這個網站有用到的功能：


- ### Reference

將首頁index.md更改為自訂內容，檔案會放在`material/overrides/`目錄下面，詳細的操作方法可以參考[官網的手冊](https://squidfunk.github.io/mkdocs-material/reference/)：

```yaml
---
template: home.html
---
```

---

- ### Admonitions

 使用一些好用的警示框，像是warning框跟可展開的info框：

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

在寫Markdown 筆記時，通常會用到大量的程式碼區塊，加上標頭以及使用跟螢光筆功能，可以使我們在閱讀時更加的方便。

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
    Component->>DOM: [(ngModel)] = "Property"
```

---

- ### Grids

Angular 有許多元件，這時使用grid cards 就可以直接導向目標頁面。

<div class="grid cards" markdown>

- :fontawesome-brands-html5: __HTML__ for content and structure
- :fontawesome-brands-js: __JavaScript__ for interactivity
- :fontawesome-brands-css3: __CSS__ for text running out of boxes
- :fontawesome-brands-internet-explorer: __Internet Explorer__ ... huh?

</div>
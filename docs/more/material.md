

# MkDocs Material

MkDocs Material 有許多好用的小東西，可以幫助我們豐富網站內容，詳細的使用方法可以參考[官方操作手冊](https://squidfunk.github.io/mkdocs-material/)。

:bulb:{.bulb} 以下是我在這個網站有用到的功能：

 ---

- ### Reference

將首頁index.md更改為自訂內容，檔案會放在`material/overrides/`目錄下面，[參考資料](https://squidfunk.github.io/mkdocs-material/reference/)：

```css
---
template: home.html
---
```

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

- ### Buttons

在我的首頁有用到兩個按鈕，分別會導向 Getting started 或 Learn more 頁面。

[Quick start](../getting-started.md){ .md-button .md-button--primary } [Learn more](#){ .md-button }
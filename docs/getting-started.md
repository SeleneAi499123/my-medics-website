# Getting started

[Angular] 是一個基於 [TypeScript] 的前端開發平台，採用[單頁式應用程式]、以及 [MVC] 架構，由 Google 團隊開發和維護，幫助開發者構建高效、模塊化和易於維護的現代 Web 應用程序。

  [Angular]: https://zh.wikipedia.org/zh-tw/Angular
  [TypeScript]: https://www.typescriptlang.org
  [單頁式應用程式]: https://zh.wikipedia.org/zh-tw/单页应用
  [MVC]: https://zh.wikipedia.org/zh-tw/MVC

---

:material-information-outline:{ title="Important information" } 想要開始使用 Angular，需要先安裝會使用到的套件及工具。

## 1. 安裝 Node.js

在 [Node.js 官方網站](https://nodejs.org/) 下載適合作業系統的版本，安裝完成後，可以在終端中運行以下命令來檢查 Node.js的安裝版本：

```bash
node -v
```

___

## 2. 安裝 TypeScript

使用 [npm](https://www.npmjs.com) 管理器來安裝 TypeScript，在終端中執行npm安裝指令：

```bash
npm install -g typescript
```

___

## 3. 安裝 Angular CLI

[Angular CLI](https://angular.io/cli)（Command Line Interface）是由 Angular 團隊提供的強大工具，用於簡化 Angular 應用程式的開發流程。它提供了各種命令，可快速搭建、構建、測試和部署 Angular 應用程式。

=== "Latest"

    ``` sh
    npm install -g @angular/cli
    ```

=== "15.x"

    ``` sh
    npm install -g @angular/cli@15
    ```


|  參數    | 說明 |
| --------- | ----------- |
| -g    | 安裝在全域       |
| --save-dev | 只安裝在目前專案  |

___

## 4. 安裝 Visual Studio Code

從 [Visual Studio Code 官方網站](https://code.visualstudio.com/) 下載適用於作業系統的安裝程式。  


!!! warning "若在 VS Code 環境中遇到無法執行 PowerShell 腳本的問題時，請輸入以下指令："
    `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`
## 建立多專案工作區

建立 Workspace 可以同時開發多個 Angular 專案，共用 node_Module 資料夾，在工作區下新增的專案會放在 `project` 資料夾底下。

```bash
ng new my-workspace --create-application false
```

___

## 創建專案

輸入以下指令創建一個新的 Angular 專案：

```bash
ng new my-angular-app -s -S
```

|  參數    | 說明 |
| --------- | ----------- |
| `--help`    | 列出參數說明  |
| `--routing`    | 產生routing module  |
| `--style`    | 指定樣式表類型，如CSS  |
| `-S`    | 不會建立spec.ts測試檔  |
| `-s` | 可使用inline style  |

___

## 運行應用程式

輸入以下指令會默認在 `http://localhost:4200/` 上運行應用程式。

```bash
ng serve -o
```

|  參數    | 說明 |
| --------- | ----------- |
| `--help`    | 列出參數說明  |
| `-o`    | 在預設瀏覽器開啟  |
| `--port`    | 指定port位置  |
| `--ssl` | 使用https  |

___

## 生成元件指令

[Angular CLI](https://angular.io/cli/generate) 可以透過在`app`資料夾底下輸入`ng g`指令來生成各種類型的檔案：

```bash
ng generate <schematic> [name]

# 簡寫
ng g <schematic> [name]
```

常用的 schematics：

- component 元件
- directive 指令
- pipe 管道
- service 服務
- class 類別
- guard 守門員
- interface 介面
- enum 枚舉
- module 模組
- application 專案

---

> 參考資料  
> [Angular CLI 官方文檔](https://angular.io/cli)
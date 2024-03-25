#  將本地存儲庫關聯至多個遠端存儲庫

## 建立關聯

使用`git remote add`指令，將本地存儲庫與多個遠端存儲庫做關聯。

```bash
git remote add origin <remote1_url>
git remote add origin2 <remote2_url>
```

!!!Note "Note"
    要透過 SSH URL 來存取遠端儲存庫，需要先建立用於通信的SSH金鑰對，詳細步驟可參考[這篇文章](./ssh-key.md)。

確認遠端儲存庫是否已經成功添加。

```bash
git remote -v
```

![](../assets/images/screenshot/gitremoteadd.png)

## 建立 commit

 ```bash
 git add .
 ```

 ```bash
 git commit -m "description"
 ```

## push 到遠端儲存庫

```bash
git push origin main
git push origin2 main
```

!!!warning "Warning"
    如果想要存取的伺服器沒有在 SSH 代理的 known_hosts 名單內，會跳出提示訊息 Are you sure you want to continue connecting，這時輸入 `yes` 來確定使用此金鑰進行連線。

![](../assets/images/screenshot/gitpushtoremote2.png)

## 執行結果

Push 到 GitLab 的結果

![](../assets/images/screenshot/remote1.png)

Push 到 GitHub 的結果

![](../assets/images/screenshot/remote2.png)


    
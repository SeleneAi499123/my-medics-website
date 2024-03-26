# 將本地目錄關聯至多個遠端存儲庫

本文章將說明，在已經連接一個遠端存儲庫的情況下，要怎麼透過`git push`指令，將本地的變更推送至多個遠端存儲庫。

---

## 建立關聯

1. 使用`git remote add`指令，連結至主要的遠端儲存庫：

    ```bash
    git remote add  origin <remote_repository_URL_1>
    ```

2. 新增其他想要同步更新的遠端儲存庫，可以輸入以下指令：

    ```bash
    git remote set-url --add --push origin <remote_repository_URL_2>
    ```

3. 確認遠端儲存庫是否已經成功添加：

    ```bash
    git remote -v
    ```

    ![](../assets/images/screenshot/gitremote-v.png)

---

## 提交變更(commit) 並 push

```bash
# 提交變更(commit)
git add .
git commit -m "description"
 
# push 到遠端儲存庫
git push origin main
```

!!!warning "Warning"
    如果想要存取的伺服器沒有在 SSH 代理的 known_hosts 名單內，會跳出提示訊息 Are you sure you want to continue connecting，這時輸入 `yes` 來確定使用此金鑰進行連線。

![](../assets/images/screenshot/gitpushtoremote2.png)

---

## 執行結果

- push 到 GitLab 的結果

![](../assets/images/screenshot/remote1.png)

- push 到 GitHub 的結果

![](../assets/images/screenshot/remote2.png)


    
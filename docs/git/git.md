# 學習 Git 版本控制

## 基本指令

- ### **git init**

在本地目錄(local repo)創建一個新的 Git 儲存庫。

```bash
git init <file directory>
```

![](../assets/images/screenshot/git-init.png)

---

- ### **git clone**

或是將遠端倉庫(remote repo)複製到本機的工作目錄(working dir)下。

=== "HTTPS"
    ```bash
    git clone <https url>
    ```

=== "SSH"
    ```bash
    git clone <ssh url>
    ```

---

- ### **git remote**

將本地儲存庫(local repo)與遠端儲存庫(remote repo)做關聯，`origin`是遠端儲存庫的別名。

```bash
git remote add origin <remote repository url>
```

> 延伸閱讀：[將本地存儲庫關聯至多個遠端存儲庫](../git/git-remote-multi-repo.md)

---

- ### **git add**

提交檔案變更到暫存區。

```bash
git add <file name>     // 指定檔案
git add .               // 當前目錄下所有已變更的檔案
```

![](../assets/images/screenshot/git%20add.png)

---

- ### **git commit -m**

將暫存的更改提交到儲存庫。

```bash
git commit -m "提交訊息"

```

![](../assets/images/screenshot/git%20commit.png)

---

- ### **git push**

將本地變更推送到遠端儲存庫，本地分支名稱預設是`main`。

```bash
git push origin <分支名>
```

![](../assets/images/screenshot/git%20push.png)

!!! warning "Git 在推送時要求輸入使用者名稱和密碼"
    通常是因為遠端倉庫使用了 HTTPS URL，而不是 SSH URL，這意味著 Git 嘗試透過 HTTPS 協定進行認證。

!!! tip "解決辦法"
    將遠端倉庫的 URL 更改為 SSH URL，Git 將使用 SSH URL 進行遠端操作，而不再需要輸入使用者名稱和密碼。
    ```bash
    git remote set-url origin <SSH URL>
    ```


遠端儲存庫：

![](../assets/images/screenshot/git%20push%20remote.png)





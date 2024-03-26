# 建立 GitHub SSH Key

SSH（Secure Shell）金鑰是一種用於加密通信和身份驗證的密鑰對，由一個公鑰和一個私鑰組成。在SSH通訊中，公鑰被用來加密信息，而相應的私鑰則用於解密信息。同時，私鑰也用來證明使用者的身份。當與一個服務器（比如GitHub）通信時，可以使用SSH金鑰對來證明是授權訪問該服務器的使用者。

---

## 1. 生成 SSH 金鑰對：

在終端機（或命令提示字元）中執行以下命令來生成：

```bash
ssh-keygen -t rsa -b 4096 -C "example@example.com"
```

!!!info "Info"
    這將會在預設目錄（通常是 ~/.ssh/）下生成一對 SSH 金鑰（公鑰和私鑰）。在生成金鑰的過程中，可以選擇為其提供密碼以提高安全性。

---

## 2.  新增到 SSH 代理：

將 SSH 金鑰新增到代理中，以免在每次使用時輸入密碼：

```bash
ssh-add ~/.ssh/id_rsa
```

---

## 3. 複製 SSH 公鑰

使用以下命令將其列印到終端機並複製：

```bash
pbcopy ~/.ssh/id_rsa.pub
```

---

## 4. 新增 SSH 公鑰到 GitHub

登錄到 GitHub 帳戶，然後轉到個人設置中的 SSH and GPG keys，點擊 New SSH key，將複製的 SSH 公鑰貼上。
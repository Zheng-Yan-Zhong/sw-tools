# SW Tools

使用工具之筆記.

## Table of Contents

- [SW Tools](#sw-tools)
  - [Table of Contents](#table-of-contents)
  - [Markdown](#markdown)
  - [VS Code](#vs-code)
    - [Hot key](#hot-key)
    - [Extentions](#extentions)
  - [Git](#git)
    - [pretty log](#pretty-log)
    - [merge abort](#merge-abort)
  - [Github](#github)
  - [Github pages](#github-pages)
  - [Heroku](#heroku)
    - [TroubleShooting](#troubleshooting)

---

## Markdown

---

## VS Code

- IDE
- lighter than other popular IDE

### Hot key

| 快捷鍵                     | 指令             |
| -------------------------- | ---------------- |
| cmd + F                    | 搜尋             |
| ctrl + shift + K           | 刪除整行         |
| shift + option + up / down | 複製整行至上或下 |
| option + left / right      | 快速移動         |
| cmd + b                    | 開關側邊欄       |
| ctrl + ~                   | 開關 terminal    |
| alt + up / down            | 移動整行         |
| cmd + p                    | 切換到..文件     |
| cmd + shift + o            | 切換到..變數     |
| cmd + w                    | 關閉文件         |
| cmd + k + f                | 關閉文件夾       |

### Extentions

- prettier-eslint

```json
//settings.json

  "files.autoSave": "onWindowChange",
  "editor.formatOnSave": true,
  "prettier.singleQuote": true
```

---

## Git

Git 是進行代碼追蹤及版本控制的軟體,與 Github 搭配成為開發的利器.

![](https://i.imgur.com/z5EWDc3.png)

> source: https://www.bitbull.it/en/blog/how-git-flow-works/

- [pretty log](#pretty-log)
- [merge abort](#merge-abort)

| 指令                          | 描述                                 |
| ----------------------------- | ------------------------------------ |
| git init                      | 初始化當前資料夾                     |
| git status                    | 列出尚未被追蹤的文件                 |
| git add . \| git add -all     | 追蹤所有文件                         |
| git commit -m "text"          | 推送至等待區                         |
| git log                       | 檢查目前等待的 log                   |
| git push                      | 推送至 github 儲存庫                 |
| git branch \<branchName>      | 建立分支                             |
| git branch                    | 查看所有分支                         |
| git brach -b \<branchName>    | 建立分支並且切換該分支               |
| git checkout \<branchName>    | 切換分支                             |
| git pull \<git repo address>  | 拉取儲存庫最新狀態並且更新本地儲存庫 |
| git clone \<git repo address> | 拉取當前儲存庫至本地                 |
| git merge                     | 把分支合併至主線                     |
|                               |                                      |

### pretty log

```git
$ git config --global alias.logline "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

當然你要 alias 什麼都可以,這邊使用 logline 對我來說比較好記憶

```git
git logline
```

---

### merge abort

會產生合併失敗主要是,當前的 master 已經不匹配於遠端儲存庫的進度了,所以我們需要把 master 更新至最新進度,並且把分支接回 master.

```git
git rebase master
```

然後就可以把分支 merge 到 master

```git
git merge
```

---

## Github

Github 是基於 Git 進行代碼託管的線上網站.

---

## Github pages

- host static page
- pushed and npm run deploy

```javascript=
npm install gh-pages --save-dev
```

然後進入 package.json

```javascript
"homepage": "http://<accountName>.github.io/<repoName>",
```

```javascript
"scripts": {
    "deploy": "gh-pages -d build"
}
```

先推送到 git repo 上後

再運行推送到 github page

```javascript
npm run deploy
```

![](https://i.imgur.com/wBBHVuc.png)

之後進入 repo 中的 pages 頁面

就可以看到成功掛載在 github pages 中了

![](https://i.imgur.com/NGv5a2N.png)

---

## Heroku

- host cloud server

我們先把專案推送到 git repo 上

> 注意！ 一定要記得把 node_modules 加進 .gitignore

![](https://i.imgur.com/0qx2IYj.png)

![](https://i.imgur.com/aiRzANY.png)

當我們要把專案部署的時候切記不要把資料庫連結密碼明文顯示在 code 中

```javascript
//.env
DB_URL =
  'mongodb+srv://root:<password>@project.bfzl8.mongodb.net/social-app?retryWrites=true&w=majority';
```

```javascript
//index.js
require('dotenv').config();
mongoose.connect(process.env.DB_URL);
```

伺服器 port

會使用 process.env.PORT 為了要對應到當我們部署在 Heroku,會自動由 Heroku 也就是伺服器管理方發配一個 port

```javascript
//index.js
app.listen(process.env.PORT || 3001, () => {
  console.log(`terminal running `);
});
```

### TroubleShooting

當在推送至 Heroku 時跑出以下其中一個

```javascript
node:internal/modules/cjs/loader:1187

return process.dlopen(module, path.toNamespacedPath(filename));

Error: /app/node_modules/bcrypt/lib/binding/napi-v3/bcrypt_lib.node: invalid ELF header
```

代表你把 node_modules 給推送上去了阿啊啊啊啊！！！

總算成功推上伺服器了

![](https://i.imgur.com/CwRyALp.png)

---

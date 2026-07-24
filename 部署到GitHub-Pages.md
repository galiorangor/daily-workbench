# 部署到 GitHub Pages（自动同步版）

目标：拿到一个**固定不变**的网址，iPhone Safari 打开 → 添加到主屏幕，就是一个随时能用的 App；以后我帮你改的内容，push 一次就自动同步上去。

沙箱里这套部署包已经准备好了（含 `index.html`、`manifest.json`、三张图标、`.github/workflows/deploy.yml` 自动部署工作流）。

---

## 你只需做 4 步

### ① 建仓库
1. 登录 GitHub → 右上角 `+` → **New repository**
2. 名字随便，例如 `my-workbench`
3. 选 **Public**（免费 Pages 需要 public；有 Pro 也可 private）
4. **不要**勾选 Initialize with README
5. 点 **Create repository**

### ② 生成访问令牌（让我能帮你推送）
1. 右上角头像 → **Settings** → 左侧 **Developer settings**
2. **Personal access tokens** → **Fine-grained tokens** → **Generate new token**
3. Token name：`workbench-deploy`
4. Expiration：选 90 天或自定义
5. Repository access：选 **Only select repositories** → 只勾你刚建的 `my-workbench`
6. Permissions → Repository permissions → **Contents：Read and write**
7. **Generate token** → **复制那串 token**（只显示这一次）

> 把这个 token 在对话里发我一句即可。它是 fine-grained、只限这一个仓库，你随时可在 GitHub 一键吊销，安全可控。

### ③ 我来连上去部署
你把下面两样发我：
- 仓库地址（如 `https://github.com/你的名/my-workbench`）
- 刚才复制的 token

我会在沙箱里执行：
```bash
git remote add origin https://<token>@github.com/你的名/my-workbench.git
git push -u origin main
```
→ GitHub Actions **自动部署**到 Pages。

### ④ 开启 Pages
进你仓库 → **Settings** → **Pages** → Source 选 **GitHub Actions** → Save。
等 1–2 分钟，拿到固定网址，例如：
```
https://你的名.github.io/my-workbench/
```

### ⑤ iPhone 添加到主屏幕
用 **Safari** 打开那个网址 → 底部分享 → **添加到主屏幕** → 命名「我的工作台」→ 添加。
就是一个全屏、带图标、无地址栏的 App 了。

---

## 之后「自动同步」怎么用

| 你想做的事 | 怎么触发 |
|--------------|--------------|
| 让我加/改养生内容 | 在对话里说一声，我改沙箱里的 `index.html` |
| 同步到 iPhone | 因为我已有你的 token，直接 `git push` → Actions 重部署 |
| iPhone 上看最新 | **关闭重开 / 下拉刷新**那个 App 即可 |

> 没给 token 也行，但每次更新得你在自己电脑上 pull 我推的版本再 push——麻烦，所以**推荐给 token**，真正一键自动同步。

---

## 说明
- 对话环境不是持久后端，固定地址只能靠部署到公网（GitHub Pages 免费）。
- 打卡、养生记录存在你**手机浏览器本地**，重开不丢；换设备不共享。
- 养生内容为个人调理记录参考，不替代专业诊疗。

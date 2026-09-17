# 「今日热搜」上传 GitHub 逐步清单

> 面向 Git 初学者。每一步都标明：**在哪个文件夹执行 → 命令做什么 → 成功时看到什么**。
> 按顺序做，一步成功再做下一步。所有命令都在 **Git Bash**（开始菜单搜 "Git Bash"）里输入。

---

## 一、环境检查结果（2026-09-17 已检查）

| 项目 | 状态 | 说明 |
|------|------|------|
| 操作系统 | ✅ Windows 11（内部版本 26200） | 64 位 |
| Git | ✅ 已安装，版本 2.54.0.windows.1 | 够用，无需升级 |
| Git Bash | ✅ 随 Git 一起安装 | 下面所有命令都在这里执行 |
| Node.js | ✅ v22.22.2 | 如果网站是 Node 项目可直接运行 |
| Python | ✅ 3.13 | 如果网站是 Python 项目可直接运行 |
| Git 用户名/邮箱 | ❌ **未配置** | 必须先配置，否则无法提交（见步骤 1） |
| GitHub CLI（gh） | ❌ **未安装** | 不装也行：本清单采用"网页建仓库"方案，不需要它 |
| SSH 密钥 | ❌ 无 | 不需要：本清单采用 HTTPS 方式，首次推送会弹出浏览器登录窗口 |
| 凭据管理器 | ✅ Git 自带 Git Credential Manager | 第一次 push 时会自动弹出 GitHub 登录页，不用手动生成令牌 |

### ⚠️ 特别提醒：项目文件尚未找到
检查了这些位置，**都没有找到「今日热搜」的文件**：
- 当前会话文件夹（`C:\Users\lenovo\WorkBuddy\2026-09-17-21-14-59`）→ 空的
- 项目工作区（`C:\Users\lenovo\WorkBuddy\28-day-project`）→ 空的（刚放入了本清单和 .gitignore）
- 桌面、文档（按名字搜"热搜"）→ 没有匹配

**开始前请先确认项目文件在哪里。** 如果项目还没创建，下面的清单同样适用——先做完步骤 1-2，等项目文件放进 `28-day-project` 后再从步骤 3 继续。

### 缺失工具清单（按你的要求，只列出、不安装）
1. **GitHub CLI（gh 命令）** —— 作用：用命令行创建 GitHub 仓库。本清单用"浏览器网页建仓库"替代，**可以不装**。如果你想装，去 https://cli.github.com 下载安装包，装完后告诉我，我再给你对应的命令版本。
2. 其余必需工具全部齐备，无需任何高风险安装。

---

## 二、上传清单

### 步骤 1：告诉 Git 你是谁（只需做一次）

- **在哪执行**：任意文件夹（Git Bash 打开即可）
- **命令做什么**：给 Git 设置全局用户名和邮箱。每次提交记录都会署上这个名字和邮箱，GitHub 靠邮箱把提交关联到你的账号
- **命令**（把引号里换成你自己的信息，邮箱建议用 GitHub 注册邮箱）：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的GitHub注册邮箱"
```

- **✅ 成功时看到**：没有任何输出（Git 的习惯：没消息就是好消息）。可以输入下面命令验证，能打印出你刚填的名字和邮箱即为成功：

```bash
git config --global user.name
git config --global user.email
```

---

### 步骤 2：确认忽略文件已就位（已帮你创建 ✅）

- **在哪执行**：项目文件夹 `C:\Users\lenovo\WorkBuddy\28-day-project`
- **已做的事**：我已在项目根目录创建了 `.gitignore`（隐藏文件），里面写明了禁止上传的内容：
  - `.env` 及一切密钥/证书/凭据文件（`.env.*`、`*.pem`、`id_rsa*`、`credentials.json` 等）
  - 依赖目录（`node_modules/`、`__pycache__/`、`venv/` 等）
  - 本地数据库（`*.db`、`*.sqlite`、`db.sqlite3` 等）
  - 日志、构建产物、系统/编辑器垃圾文件（`Thumbs.db`、`.DS_Store`、`.idea/` 等）
- **怎么验证**：

```bash
cat .gitignore
```

- **✅ 成功时看到**：屏幕打印出忽略规则的内容
- 💡 如果项目实际不在 `28-day-project`，把这个 `.gitignore` 复制到项目根目录（和 `index.html` / `package.json` 同级的那一层）即可

---

### 步骤 3：进入项目文件夹并初始化仓库

- **在哪执行**：项目文件夹 `C:\Users\lenovo\WorkBuddy\28-day-project`
- **命令做什么**：

```bash
cd /c/Users/lenovo/WorkBuddy/28-day-project
git init
git branch -M main
```

  - `git init`：把当前文件夹变成一个 Git 仓库（会生成一个隐藏的 `.git` 文件夹，所有版本历史都存在里面）
  - `git branch -M main`：把默认分支改名为 `main`（GitHub 的默认叫法，避免叫 `master` 对不上）
- **✅ 成功时看到**：

  - `git init` 输出：`Initialized empty Git repository in C:/Users/lenovo/WorkBuddy/28-day-project/.git/`
  - `git branch -M main`：无输出，不报错即为成功

---

### 步骤 4：把文件加入暂存区

- **在哪执行**：项目文件夹
- **命令做什么**：`git add .` 中的 `.` 代表"当前文件夹下所有文件"，把要保存的文件先登记到"暂存区"（相当于把要寄的东西先装进箱子）。`.gitignore` 里列的文件会被自动跳过

```bash
git add .
```

- **✅ 成功时看到**：没有输出、没有报错
- ⚠️ 如果有 warning 提示 LF/CRLF 换行符转换，属正常现象，可忽略

---

### 步骤 5：上传前的安全检查（强烈建议做）

- **在哪执行**：项目文件夹
- **命令做什么**：`git status` 列出即将被提交的所有文件；第二条命令专门检查有没有敏感文件混进来

```bash
git status
git ls-files | grep -iE "\.env|secret|password|credential|\.pem|id_rsa" || echo "安全：没有敏感文件被登记"
```

- **✅ 成功时看到**：
  - `git status`：所有文件显示为绿色 `new file:`，且**看不到** `node_modules/`、`.env`、`*.db` 之类的内容
  - 第二条命令打印：`安全：没有敏感文件被登记`
- ❌ 如果看到敏感文件：说明 `.gitignore` 没放对位置或规则没覆盖，**先停下来解决**（可以问我），不要继续提交

---

### 步骤 6：做第一次提交

- **在哪执行**：项目文件夹
- **命令做什么**：`git commit` 把暂存区的文件打包成一个"存档点"（版本），`-m` 后面是这次存档的说明

```bash
git commit -m "Day 1｜初始化今日热搜网站项目"
```

- **✅ 成功时看到**：类似
  `[main (root-commit) a1b2c3d] Day 1｜初始化今日热搜网站项目`
  ` 25 files changed, 1200 insertions(+)`
  数字不重要，出现 `root-commit` 和 `files changed` 即为成功
- 💡 按你项目的惯例，提交说明用 `Day X｜一句话说明` 的格式

---

### 步骤 7：在 GitHub 网页上创建远程仓库

- **在哪执行**：浏览器（不需要命令行）
- **做什么**：
  1. 打开 https://github.com 并登录（没有账号就先注册一个）
  2. 点右上角 **+** → **New repository**
  3. Repository name 填：`today-hot-search`（仓库名建议用英文，中文名可能在某些工具里出问题）
  4. Public（公开）或 Private（私有）任选
  5. **三个勾全部不勾**：不要加 README、不要加 .gitignore、不要选 License（本地已有，勾了会冲突）
  6. 点 **Create repository**
- **✅ 成功时看到**：页面跳转到一个空仓库，显示 "Quick setup" 和一串以 `https://github.com/你的用户名/today-hot-search.git` 结尾的地址——**把这串地址复制下来**，下一步要用

---

### 步骤 8：把本地仓库和 GitHub 关联起来

- **在哪执行**：项目文件夹（Git Bash）
- **命令做什么**：`git remote add origin <地址>` 给 GitHub 上的仓库起个别名叫 `origin`，并记住它的地址（只需做一次）

```bash
git remote add origin https://github.com/你的用户名/today-hot-search.git
```

- **✅ 成功时看到**：没有输出。可输入 `git remote -v` 验证，能看到 `origin` 和你刚才的地址
- ❌ 如果报 `remote origin already exists`：说明之前关联过，用下面的命令改成新地址即可：
  `git remote set-url origin https://github.com/你的用户名/today-hot-search.git`

---

### 步骤 9：推送到 GitHub

- **在哪执行**：项目文件夹（Git Bash）
- **命令做什么**：`git push` 把本地的提交上传到 GitHub；`-u origin main` 表示推给 `origin` 的 `main` 分支，并记住这个对应关系（`-u` 只需第一次用）

```bash
git push -u origin main
```

- **✅ 成功时看到**：
  1. **第一次推送**会弹出浏览器窗口让你登录 GitHub（这是 Git 自带的凭据管理器在工作）→ 点授权 → 窗口自动关闭
  2. 命令行最后显示：`Branch 'main' set up to track remote branch 'main' from 'origin'` 和 `main -> main`
  3. 刷新 GitHub 网页，能看到项目的所有文件
- ❌ 如果报 `Authentication failed`：重新推送一次，在弹出的浏览器窗口里完成登录即可
- ❌ 如果报 `rejected`（本地和远程历史不一致，常见于不小心勾了 README）：先运行 `git pull origin main --rebase` 再推送

---

## 三、以后每天的常规操作（记住这四条就够了）

```bash
git add .                        # 1. 装箱
git status                       # 2. 检查（可选但推荐）
git commit -m "Day X｜一句话说明"  # 3. 盖章存档
git push                         # 4. 寄出（以后不用再加 -u origin main）
```

## 四、安全红线（务必记住）

1. `.env`、密码、API 密钥**永远不上传**——一旦推到公开仓库，即使删除也可能被爬虫抓走，等于密钥泄露，必须立刻换新
2. 万一误传了敏感文件：不要只删除文件再提交，**马上告诉我**，我带你处理（可能需要清除历史记录 + 更换密钥）
3. 依赖目录（`node_modules/`）和本地数据库文件不上传，任何人在 GitHub 上看到项目后，靠 `package.json` 等清单文件即可自己安装依赖

# NoteFlow 构建指南

## 文件说明

```
NoteFlow/
├── NoteFlow.html          ← 主应用（直接双击浏览器打开即可使用）
├── electron-src/
│   ├── package.json       ← Electron 项目配置
│   └── main.js            ← Electron 主进程
├── python-src/
│   └── launcher.py        ← Python pywebview 启动器
└── README.md
```

---

## 方式一：直接使用（无需打包）

直接双击 `NoteFlow.html`，用 Chrome / Edge / Firefox 打开即可。
数据自动保存在浏览器 localStorage，完全本地，无需网络。

---

## 方式二：Electron 打包为 .exe（推荐）

### 前提：安装 Node.js (https://nodejs.org)

```bash
# 1. 进入 electron-src 目录
cd electron-src

# 2. 复制主应用到该目录
cp ../NoteFlow.html ./NoteFlow.html

# 3. 安装依赖
npm install

# 4. 运行开发模式预览
npm start

# 5. 打包 Windows exe
npm run build:win
# 输出在 dist/ 目录，包含安装包 (.exe)

# 打包 macOS
npm run build:mac

# 打包 Linux
npm run build:linux
```

打包完成后，`dist/` 目录会生成 `NoteFlow Setup x.x.x.exe` 安装包。

---

## 方式三：Python + pywebview 打包为 .exe

### 前提：安装 Python 3.8+

```bash
# 1. 安装依赖
pip install pywebview pyinstaller

# 2. 进入 python-src 目录
cd python-src

# 3. 复制主应用到该目录
cp ../NoteFlow.html ./NoteFlow.html

# 4. 运行开发模式预览
python launcher.py

# 5. 打包 Windows（单文件 exe）
pyinstaller --onefile --windowed --name NoteFlow ^
  --add-data "NoteFlow.html;." ^
  launcher.py

# macOS / Linux：
pyinstaller --onefile --windowed --name NoteFlow \
  --add-data "NoteFlow.html:." \
  launcher.py
```

打包完成后，`dist/NoteFlow.exe` 即为可直接运行的单文件程序。

---

## 数据存储说明

- 所有数据存储在**浏览器 / 应用的 localStorage** 中
- Electron 版数据路径：`%APPDATA%\noteflow\Local Storage`
- 导出功能：点击侧边栏「导出」可将当前备忘导出为独立 HTML 文件

---

## 多语言支持

点击侧边栏底部「🌐 语言」按钮，支持：
- 🇨🇳 简体中文
- 🇺🇸 English
- 🇯🇵 日本語
- 🇰🇷 한국어
- 🇫🇷 Français

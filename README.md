# NoteFlow

> 本地备忘录桌面应用 · 无需账号 · 无需网络 · 数据永远属于你

---

## 目录

- [功能概览](#功能概览)
- [文件结构](#文件结构)
- [快速开始](#快速开始)
- [方式一：浏览器直接使用](#方式一浏览器直接使用)
- [方式二：Electron 打包 .exe（推荐）](#方式二electron-打包-exe推荐)
- [方式三：Python pywebview 打包 .exe](#方式三python-pywebview-打包-exe)
- [导出格式说明](#导出格式说明)
- [多语言支持](#多语言支持)
- [数据存储](#数据存储)
- [已修复的问题](#已修复的问题)

---

## 功能概览

| 功能 | 说明 |
|------|------|
| 📝 富文本编辑 | 加粗、斜体、下划线、删除线、标题、列表、引用、代码块、表格、链接 |
| ☑️ 待办清单 | 可勾选 checkbox，直接嵌入笔记内容 |
| 📎 多类型文件 | 图片嵌入显示，PDF / Word / Excel / 音视频等以附件卡片内联 |
| 📊 写作统计 | 实时显示字符数、词数、段落数、行数、预计阅读时长 |
| 🔍 全文搜索 | 侧边栏实时过滤，同时检索标题与正文 |
| 💾 自动保存 | 输入 0.8 秒后自动保存至 localStorage |
| ↓ 多格式导出 | HTML · PDF · PNG 截图 · 长图 |
| 🌐 多语言 | 中文 / English / 日本語 / 한국어 / Français |
| ⇔ 可调侧边栏 | 拖拽边界自由调整宽度 |
| 🎨 文字颜色 | 文字色与高亮色取色器 |

---

## 文件结构

```
NoteFlow/
├── NoteFlow.html          ← 主应用（单文件，双击即用）
├── electron-src/
│   ├── NoteFlow.html      ← 同上，已复制
│   ├── main.js            ← Electron 主进程
│   └── package.json       ← 依赖与打包配置
├── python-src/
│   ├── NoteFlow.html      ← 同上，已复制
│   └── launcher.py        ← Python pywebview 启动器
└── README.md
```

---

## 快速开始

**最简单的方式**：直接双击 `NoteFlow.html`，用 Chrome / Edge / Firefox 打开即可使用。无需安装任何软件。

如需打包为独立 `.exe` 桌面程序，选择下方任一方式。

---

## 方式一：浏览器直接使用

```
双击 NoteFlow.html → 用浏览器打开
```

- ✅ 零安装，打开即用
- ✅ 数据保存在浏览器 localStorage，刷新不丢失
- ✅ 完全离线，无需网络
- ⚠️ 数据绑定在当前浏览器，换浏览器不共享

---

## 方式二：Electron 打包 .exe（推荐）

生成专业的 Windows 安装包，体验与原生桌面应用完全一致。

### 前提条件

安装 [Node.js](https://nodejs.org)（LTS 版本即可）

### 步骤

```bash
# 1. 进入 electron-src 目录
cd electron-src

# 2. 安装依赖（首次需要联网）
npm install

# 3. 预览（可选）
npm start

# 4. 打包
npm run build:win     # Windows → dist/NoteFlow Setup x.x.x.exe
npm run build:mac     # macOS   → dist/NoteFlow-x.x.x.dmg
npm run build:linux   # Linux   → dist/NoteFlow-x.x.x.AppImage
```

打包完成后，`dist/` 目录中的安装包即为最终产物。

### Electron 版数据路径

| 系统 | 路径 |
|------|------|
| Windows | `%APPDATA%\noteflow\Local Storage\` |
| macOS | `~/Library/Application Support/noteflow/` |
| Linux | `~/.config/noteflow/` |

---

## 方式三：Python pywebview 打包 .exe

生成无需依赖的单文件可执行程序。

### 前提条件

安装 Python 3.8 或以上版本

### 步骤

```bash
# 1. 安装依赖
pip install pywebview pyinstaller

# 2. 进入 python-src 目录
cd python-src

# 3. 预览（可选）
python launcher.py

# 4. 打包

# Windows（单文件 exe）
pyinstaller --onefile --windowed --name NoteFlow ^
  --add-data "NoteFlow.html;." ^
  launcher.py

# macOS / Linux
pyinstaller --onefile --windowed --name NoteFlow \
  --add-data "NoteFlow.html:." \
  launcher.py
```

打包完成后，`dist/NoteFlow.exe`（Windows）即为可直接分发的单文件程序。

---

## 导出格式说明

点击侧边栏「导出」按钮，弹出下拉菜单，提供四种格式：

| 格式 | 文件 | 说明 |
|------|------|------|
| 📄 HTML 文件 | `.html` | 保留所有格式与内嵌图片，可直接在浏览器打开 |
| 🖨 导出 PDF | — | 调用系统打印对话框，选「另存为 PDF」 |
| 🖼 导出图片 | `.png` | 当前可视区域截图，2× 分辨率 |
| 📜 导出长图 | `.png` | 完整内容全高截图，适合分享 |

> **注**：图片导出采用纯 JS 实现（SVG foreignObject + Canvas），完全离线，无需外部库。
> 若笔记内嵌了外链图片（http:// 开头），截图时该图片可能无法渲染，自动 fallback 到新窗口供截图。
> 通过应用插入的图片（base64）可正常渲染。

---

## 多语言支持

点击侧边栏底部 **🌐 语言** 按钮切换，语言偏好自动保存：

| 语言 | |
|------|-|
| 🇨🇳 简体中文 | 默认 |
| 🇺🇸 English | |
| 🇯🇵 日本語 | |
| 🇰🇷 한국어 | |
| 🇫🇷 Français | |

所有界面文字（按钮、提示、统计标签、导出菜单）均随语言切换。

---

## 数据存储

- 所有笔记数据存储在 **localStorage**，完全本地，不上传任何服务器
- 浏览器版：数据在当前浏览器的 localStorage 中
- Electron 版：数据在应用专属目录的 leveldb 中（见上方路径）
- **备份建议**：定期使用「导出 HTML」功能备份重要笔记

---

## 已修复的问题

### Bug 1 — 新建备忘点击「创建」无反应

**原因**：`confirmModal()` 先调用 `closeModal()`（将 `modalCb` 置为 `null`），再检查 `if (modalCb)` 导致回调永远不执行。

```js
// ❌ 修复前
function confirmModal() {
  closeModal()           // modalCb 被清为 null
  if (modalCb) modalCb() // 永远不执行
}

// ✅ 修复后
function confirmModal() {
  const cb = modalCb     // 先保存
  closeModal()
  if (cb) cb(val)        // 正常执行
}
```

---

### Bug 2 — 导出按钮无效（Firefox 等浏览器）

**原因**：动态创建的 `<a>` 元素未挂载到 DOM 直接调用 `.click()`，Firefox 等浏览器会静默忽略。

```js
// ❌ 修复前
const a = document.createElement('a')
a.href = url
a.click()  // Firefox 忽略

// ✅ 修复后
document.body.appendChild(a)
a.click()
document.body.removeChild(a)
setTimeout(() => URL.revokeObjectURL(url), 1000)
```

---

### Bug 3 — 图片/长图导出报 `Uncaught Error: Script error.`

**原因**：Chrome 在 `file://` 协议下通过 `URL.createObjectURL()` 加载含 `<foreignObject>` 的 SVG 时，会触发全局 `window` 错误事件，消息固定为 `"Script error."`。这是 Chrome 的安全沙箱限制。

```js
// ❌ 修复前（blob URL → 触发全局 Script error.）
const url = URL.createObjectURL(new Blob([svgSrc], { type: 'image/svg+xml' }))
img.src = url

// ✅ 修复后（base64 data URL → 同源内联，无限制）
img.src = 'data:image/svg+xml;base64,' + btoa(unescape(encodeURIComponent(svgSrc)))
```

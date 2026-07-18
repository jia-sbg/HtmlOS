# 🖥️ HTMLOS · 网页操作系统

<div align="center">

![版本](https://img.shields.io/badge/版本-v4.3.0-0a84ff?style=flat-square)
![许可](https://img.shields.io/badge/许可-MIT-30d158?style=flat-square)
![技术栈](https://img.shields.io/badge/技术栈-HTML%2FCSS%2FJS-ffb900?style=flat-square)
![PWA](https://img.shields.io/badge/PWA-支持-5e5ce6?style=flat-square)

**一个完全运行在浏览器中的 Web 桌面操作系统 · Windows 8.1 磁贴风格 · 支持离线使用**

[🌐 在线体验](https://jia-sbg.github.io/HtmlOS) · 
[📦 Cloudflare 镜像](https://htmlos.pages.dev) · 
[⭐ Star 支持](https://github.com/jia-sbg/HtmlOS)

</div>

---

## ✨ 特性亮点

| 类别 | 功能 |
|------|------|
| 🎨 **桌面体验** | Windows 8.1 风格磁贴（5 种尺寸）、多页面桌面、实时搜索高亮、滑动翻页、页面指示器 |
| 📱 **应用管理** | HTML 文件安装、**拖拽安装**、批量/文件夹导入、应用隐藏/锁定、图标/颜色/大小自定义、应用信息全屏查看 |
| 📁 **数据持久化** | IndexedDB 存储引擎、一键备份/恢复（支持合并导入）、应用使用统计 |
| 🔧 **系统设置** | 背景壁纸（预设+本地上传，**支持一键清除地址**）、三套主题（直角/玻璃/暗黑）、列数调节、启动动画、触摸震动 |
| 🚀 **开发者功能** | FPS 监控（自适应刷新率）、基础/高级内存自动回收、系统日志导出/清空、沙箱控制、DOMGuard 界面防护 |
| 📱 **移动优化** | 触摸手势、长按菜单、滑动翻页、震动反馈、PWA 支持、安全区域适配、双击顶部返回、**拖拽安装** |
| 🌐 **离线能力** | PWA 离线缓存、离线提示、断网可用 |
| 🛡️ **安全防护** | DOMGuard 界面防护系统、紧急退出机制（Esc/F12）、应用沙箱隔离、密码保护（恢复默认/格式化）、应用防伪装校验、高危操作黑名单拦截 |
| 📢 **通知系统** | Toast 通知（限流队列）、通知中心（分类过滤、持久化）、通知声音；**玻璃主题下通知面板也支持毛玻璃效果** |
| 👤 **用户系统** | 自定义用户名、Emoji 头像选择、系统密码管理（AES-GCM 加密存储） |
| 🔋 **硬件集成** | 电池状态实时显示、摄像头/麦克风硬件检测（安全中心） |

---

## 🎯 快速开始

### 在线体验
直接访问：[https://jia-sbg.github.io/HtmlOS](https://jia-sbg.github.io/HtmlOS)

### 本地运行
```bash
# 克隆仓库
git clone https://github.com/jia-sbg/HtmlOS.git

# 使用任意 HTTP 服务器启动（如 Python）
python -m http.server 8080

# 或使用 VS Code Live Server
```

### 安装为 PWA 应用
1. 使用 Chrome/Edge 访问在线地址
2. 点击地址栏右侧的「安装」图标
3. 即可像原生 App 一样离线使用

---

## 🏗️ 技术架构

```
┌─────────────────────────────────────────────────┐
│              HTMLOS v4.3.0 主页面                 │
├─────────────────────────────────────────────────┤
│  IndexedDB ── 应用存储 / 设置 / 统计 / 通知       │
│  Service Worker ── 离线缓存 / PWA 支持            │
│  postMessage ── 主页面 ↔ 应用通信（限流防刷）      │
│  DOMGuard ── 界面防护 / 防恶意篡改 / 背景防篡改    │
│  iframe 沙箱 ── 应用隔离运行（可开关）              │
├─────────────────────────────────────────────────┤
│           应用运行容器 (iframe 沙箱)                │
│  ┌───────────────────────────────────────────┐  │
│  │  用户安装的 .html 应用                      │  │
│  │  (可调用系统 API：通知/存储/震动/标题等)    │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

### 核心技术栈

| 技术 | 用途 |
|------|------|
| **IndexedDB** | 应用代码持久化、用户数据存储、设置、统计、通知 |
| **iframe + sandbox** | 应用隔离运行、安全执行（支持关闭沙箱的开发者选项） |
| **postMessage** | 系统与应用双向通信（限流：每秒最多 30 条，防消息洪水） |
| **Service Worker** | 离线缓存、PWA 支持 |
| **MutationObserver** | DOMGuard 界面防护系统（防移除、防隐藏、防 head 注入、防主题篡改、核心函数防篡改） |
| **Web Crypto API** | 系统密码 AES-GCM 加密存储 |
| **Battery Status API** | 电量实时显示 |
| **Vibration API** | 触摸反馈 |
| **File System Access / Drag & Drop** | 批量/文件夹/拖拽应用安装 |
| **Intl.DateTimeFormat** | 高性能日期时间格式化（缓存复用） |

---

## 📦 应用开发

任何 HTML 文件都可以作为应用安装，并可通过 `postMessage` 与系统交互。

### 最小示例

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"></head>
<body>
  <h1>我的 HTMLOS 应用</h1>
  <button onclick="sendMessage()">发送通知</button>
  <script>
    function sendMessage() {
      if (window.parent !== window) {
        window.parent.postMessage({
          from: 'htmlos-app',
          type: 'message',
          action: 'toast',
          data: { message: 'Hello HTMLOS!', type: 'success' }
        }, '*');
      }
    }
  <\/script>
</body>
</html>
```

### 可用 API 列表

| 动作 | 说明 |
|------|------|
| `getSystemInfo` | 获取系统信息（版本/主题/应用数/在线状态/沙箱状态/DOMGuard 状态） |
| `setTitle` | 修改应用标题栏显示文字 |
| `toast` | 发送系统 Toast 通知（支持类型、时长） |
| `vibrate` | 触发震动反馈（需用户在设置中开启） |
| `saveData` / `getData` | 存储/读取持久化数据（按应用隔离） |
| `close` | 关闭应用返回桌面 |
| `openUrl` | 请求打开外部链接（需用户确认） |

---

## 🛠️ 高级功能

### 开发者模式（隐藏彩蛋）

- **激活方式**：在「系统设置 → 关于」中连续点击版本号 **7 次**
- **解锁功能**：
  - FPS 实时监控（自适应屏幕刷新率上限，显示当前/上限帧率）
  - 高级内存优化（自动清理缓存、旧数据）
  - 沙箱开关控制（危险操作，需密码确认）
  - 系统日志导出/清空
  - 强制刷新所有应用、修复磁贴布局

### 安全中心（系统核心组件）

- 入口：设置 → 系统 → 系统安全
- 功能：
  - 实时查看沙箱隔离状态、DOMGuard 运行状态
  - 摄像头/麦克风/震动硬件检测（验证应用硬件调用权限）
- **特性**：内置于系统代码，**无法卸载、无法隐藏、无法篡改**

### 数据管理

| 功能 | 说明 |
|------|------|
| **导出备份** | 保存所有应用代码、设置、统计、通知到 JSON 文件 |
| **导入备份** | 支持「合并」（保留现有数据）和「覆盖」两种模式 |
| **恢复默认** | 输入系统密码确认后重置所有设置（保留应用数据） |
| **格式化系统** | 输入系统密码确认后清空所有数据（不可逆） |

### 主题系统

| 主题 | 特点 |
|------|------|
| **直角无动画** | 经典 Windows 8 风格，零动画开销，极致性能 |
| **玻璃质感** | 毛玻璃效果、大圆角、丝滑动画、阴影层次；**通知中心与 Toast 也支持 backdrop-filter 实时模糊** |
| **纯黑夜间** | 深色模式、护眼、低功耗、OLED 友好 |

### 磁贴尺寸

支持 5 种磁贴尺寸，自由搭配布局：
- **小** (1×1) · **中** (2×1) · **大** (2×2) · **宽** (3×1) · **超大** (3×2)

---

## 📁 项目结构

```
HtmlOS/
├── index.html              # 单文件完整系统（v4.3.0）
├── README.md               # 项目说明
└── .github/                # GitHub 配置
```

> **单文件设计**：所有功能（UI、逻辑、样式、PWA、IndexedDB 封装、DOMGuard、安全中心）集成在一个 HTML 文件中，无需构建工具，直接部署。

---

## 🤝 参与贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

---

## 📜 声明

- **AI 辅助开发**：本项目由多个 AI（DeepSeek、Claude、Kimi、豆包等）协助完成
- **原创声明**：GitHub 上存在同名项目，但本项目的代码和设计均为独立原创，绝非抄袭
- **开源许可**：MIT License

---

## 👤 作者

- GitHub：[jia-sbg](https://github.com/jia-sbg)
- B站：[GoYi-1](https://space.bilibili.com/3546866897651966)（欢迎关注！）

---

## 🙏 致谢

感谢所有 Star 和支持这个项目的朋友！

如果觉得不错，别忘了点个 ⭐ Star

🔗 [GitHub 仓库](https://github.com/jia-sbg/HtmlOS) · 
🎬 [B站主页](https://space.bilibili.com/3546866897651966)

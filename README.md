# 🖥️ HtmlOS · 网页操作系统

<div align="center">

![版本](https://img.shields.io/badge/版本-v3.7.1-0a84ff?style=flat-square)
![许可](https://img.shields.io/badge/许可-MIT-30d158?style=flat-square)
![技术栈](https://img.shields.io/badge/技术栈-HTML%2FCSS%2FJS-ffb900?style=flat-square)
![PWA](https://img.shields.io/badge/PWA-支持-5e5ce6?style=flat-square)

**一个完全运行在浏览器中的 Web 桌面操作系统 · Windows 8.1 风格 · 支持离线使用**

[🌐 在线体验](https://jia-sbg.github.io/HtmlOS) · 
[📦 Cloudflare 镜像](https://htmlos.pages.dev) · 
[⭐ Star 支持](https://github.com/jia-sbg/HtmlOS)

</div>

---

## ✨ 特性亮点

| 类别 | 功能 |
|------|------|
| 🎨 **桌面体验** | Windows 8.1 风格磁贴、多页面桌面、实时搜索、滑动翻页 |
| 📱 **应用管理** | HTML 文件安装、批量/文件夹导入、应用隐藏/锁定、图标/颜色/大小自定义 |
| 📁 **文件夹系统** | 新建分组文件夹、多选应用收纳、文件夹内启动应用、属性查看、跨文件夹移动 |
| 💾 **数据持久化** | IndexedDB 存储引擎、一键备份/恢复、数据合并导入 |
| 🔧 **系统设置** | 背景壁纸、三套主题（直角/玻璃/暗黑）、列数调节、启动动画 |
| 🚀 **开发者功能** | FPS 监控、内存自动回收、系统日志导出、应用缓存清理、沙箱控制 |
| 📱 **移动优化** | 触摸手势、长按菜单、滑动翻页、震动反馈、PWA 支持、安全区域适配 |
| 🌐 **离线能力** | Service Worker 缓存、离线提示、断网可用 |
| 🛡️ **安全防护** | DOM 防护系统、紧急退出机制、应用沙箱隔离、密码保护 |

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

安装为 PWA 应用
1. 使用 Chrome/Edge 访问在线地址
2. 点击地址栏右侧的「安装」图标
3. 即可像原生 App 一样使用

---

🏗️ 技术架构

```
┌─────────────────────────────────────────────────┐
│                   HtmlOS v3.8 主页面              │
├─────────────────────────────────────────────────┤
│  IndexedDB ── 应用存储 / 设置 / 布局 / 统计       │
│  Service Worker ── 离线缓存 / PWA 支持            │
│  postMessage ── 主页面 ↔ 应用通信                 │
│  DOMGuard ── 界面防护 / 防恶意篡改                │
├─────────────────────────────────────────────────┤
│           应用运行容器 (iframe 沙箱)                │
│  ┌───────────────────────────────────────────┐  │
│  │  用户安装的 .html 应用                      │  │
│  │  (可调用系统 API：通知/存储/震动/等)        │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

核心技术栈

技术	用途	
IndexedDB	应用代码持久化、用户数据存储、文件夹系统	
iframe 沙箱	应用隔离运行、安全执行	
postMessage	系统与应用双向通信	
Service Worker	离线缓存、PWA 支持	
Battery Status API	电量显示	
Vibration API	触摸反馈	
MutationObserver	DOM 防护系统	

---

📦 应用开发

为 HtmlOS 开发应用

任何 HTML 文件都可以作为应用安装，并可选择与系统交互：

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"></head>
<body>
  <h1>我的 HtmlOS 应用</h1>
  <button onclick="sendMessage()">发送通知</button>
  <script>
    function sendMessage() {
      if (window.parent !== window) {
        window.parent.postMessage({
          from: 'htmlos-app',
          type: 'message',
          action: 'toast',
          data: { message: 'Hello HtmlOS!', type: 'success' }
        }, '*');
      }
    }
  </script>
</body>
</html>
```

可用 API

动作	说明	
`toast`	发送系统通知	
`getSystemInfo`	获取系统信息（版本/主题/应用数等）	
`setTitle`	修改应用标题栏	
`saveData` / `getData`	存储/读取持久化数据	
`vibrate`	触发震动反馈（需开启设置）	
`close`	关闭应用返回桌面	
`openUrl`	请求打开外部链接（需用户确认）	

---

🛠️ 高级功能

开发者模式（隐藏彩蛋）

- 激活方式：在「系统设置 → 关于」中连续点击版本号 7 次
- 功能：FPS 监控、高级内存优化、沙箱控制、系统日志导出

数据管理

功能	说明	
导出备份	保存所有应用代码、设置、统计、布局、文件夹结构	
导入备份	支持合并/覆盖两种模式，保留文件夹关系	
恢复默认	输入密码确认后重置系统设置（保留应用数据）	
格式化系统	输入密码确认后清空所有数据	

主题系统

主题	特点	
直角无动画	经典 Windows 8 风格，零动画开销	
玻璃质感	毛玻璃效果、圆角、丝滑动画	
纯黑夜间	深色模式、护眼、低功耗	

---

📁 项目结构

```
HtmlOS/
├── index.html              # 单文件完整系统（v3.8）
├── README.md               # 项目说明
└── .github/                # GitHub 配置
```

> 单文件设计：所有功能（UI、逻辑、样式、PWA）集成在一个 HTML 文件中，无需构建工具，直接部署。


---

🤝 参与贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

---

📜 声明

- AI 辅助开发：本项目由多个 AI（DeepSeek、豆包、Kimi 等）协助完成
- 原创声明：GitHub 上存在同名项目，但本项目的代码和设计均为独立原创，绝非抄袭
- 开源许可：MIT License

---

👤 作者

- GitHub：[jia-sbg](https://github.com/jia-sbg)
- B站：[GoYi-1](https://space.bilibili.com/3546866897651966)（欢迎关注！）

---

🙏 致谢

感谢所有 Star 和支持这个项目的朋友！

如果觉得不错，别忘了点个 ⭐ Star

🔗 [GitHub 仓库](https://github.com/jia-sbg/HtmlOS) · 
🎬 [B站主页](https://space.bilibili.com/GoYi-1)

DeepSeek & Kimi 帮我写的 😋

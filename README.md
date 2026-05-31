# 🖥️ HtmlOS · 网页操作系统

<div align="center">

![许可](https://img.shields.io/badge/许可-MIT-30d158?style=flat-square)
![技术栈](https://img.shields.io/badge/技术栈-HTML%2FCSS%2FJS-ffb900?style=flat-square)
![PWA](https://img.shields.io/badge/PWA-支持-5e5ce6?style=flat-square)

**一个完全运行在浏览器中的Web桌面操作系统 · Windows 8.1风格 · 支持离线使用**

[🌐 在线体验](https://jia-sbg.github.io/HtmlOS) · 
[📦 Cloudflare镜像](https://htmlos.pages.dev) · 
[⭐ Star支持](https://github.com/jia-sbg/HtmlOS)

</div>

---

## ✨ 特性亮点

| 类别 | 功能 |
|------|------|
| 🎨 **桌面体验** | Windows 8.1风格磁贴、拖拽排列、多页面桌面、实时搜索 |
| 📱 **应用管理** | HTML文件安装、批量导入、应用隐藏/锁定、图标/颜色/大小自定义 |
| 💾 **数据持久化** | IndexedDB存储引擎、一键备份/恢复、数据合并导入 |
| 🔧 **系统设置** | 背景壁纸、三套主题（直角/玻璃/暗黑）、列数调节、启动动画 |
| 🚀 **开发者功能** | FPS监控、内存自动回收、系统日志导出、应用缓存清理 |
| 📱 **移动优化** | 触摸手势、长按菜单、滑动翻页、震动反馈、PWA支持 |
| 🌐 **离线能力** | Service Worker缓存、离线提示、断网可用 |

## 🎯 快速开始

### 在线体验
直接访问：[https://jia-sbg.github.io/HtmlOS](https://jia-sbg.github.io/HtmlOS)

### 本地运行
```bash
# 克隆仓库
git clone https://github.com/jia-sbg/HtmlOS.git

# 使用任意HTTP服务器启动（如Python）
python -m http.server 8080

# 或使用VS Code Live Server
```

安装为PWA应用

1. 使用Chrome/Edge访问在线地址
2. 点击地址栏右侧的「安装」图标
3. 即可像原生App一样使用

🏗️ 技术架构

```
┌─────────────────────────────────────────────────┐
│                   HtmlOS 主页面                  │
├─────────────────────────────────────────────────┤
│  IndexedDB ── 应用存储 / 设置 / 布局 / 统计      │
│  Service Worker ── 离线缓存 / PWA支持            │
│  postMessage ── 主页面 ↔ 应用通信               │
├─────────────────────────────────────────────────┤
│           应用运行容器 (iframe沙箱)              │
│  ┌───────────────────────────────────────────┐  │
│  │  用户安装的 .html 应用                     │  │
│  │  (可调用系统API：通知/存储/震动/等)        │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

核心技术栈

技术 用途
IndexedDB 应用代码持久化、用户数据存储
iframe沙箱 应用隔离运行、安全执行
postMessage 系统与应用双向通信
Service Worker 离线缓存、PWA支持
Battery Status API 电量显示
Vibration API 触摸反馈

📦 应用开发

为HtmlOS开发应用

任何HTML文件都可以作为应用安装，并可选择与系统交互：

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"></head>
<body>
  <h1>我的HtmlOS应用</h1>
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

可用API

动作 说明
toast 发送系统通知
getSystemInfo 获取系统信息（版本/主题/应用数等）
setTitle 修改应用标题栏
saveData / getData 存储/读取持久化数据
vibrate 触发震动反馈（需开启设置）
close 关闭应用返回桌面

🛠️ 高级功能

开发者模式（隐藏彩蛋）

· 激活方式：在「系统信息」卡片中连续点击版本号 7次

数据管理

· 导出备份：保存所有应用代码、设置、统计、布局
· 导入备份：支持合并/覆盖两种模式
· 格式重置：输入密码1234恢复出厂设置

📁 项目结构

```
HtmlOS/
├── index.html              # 单文件完整系统
├── README.md               # 项目说明
└── .github/                # GitHub配置
```

🤝 参与贡献

1. Fork 本仓库
2. 创建特性分支 (git checkout -b feature/AmazingFeature)
3. 提交更改 (git commit -m 'Add some AmazingFeature')
4. 推送到分支 (git push origin feature/AmazingFeature)
5. 提交 Pull Request

📜 声明

· AI辅助开发：本项目由多个AI（DeepSeek、豆包等）协助完成
· 原创声明：GitHub上存在同名项目，但本项目的代码和设计均为独立原创，绝非抄袭
· 开源许可：MIT License

👤 作者

· GitHub：jia-sbg
· B站：GoYi-1（欢迎关注！）

🙏 致谢

感谢所有Star和支持这个项目的朋友！

<div align="center">

如果觉得不错，别忘了点个Star ⭐

🔗 GitHub仓库 · 
🎬 B站主页
Deepseek帮我写的😋
</div>
```
